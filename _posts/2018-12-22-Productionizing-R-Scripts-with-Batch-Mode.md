---
layout: post
title: Productionizing R Scripts with Batch Mode
tag:
  - r
comments: true
---

And parse argument at the same time.

```r
# "-arg1 value1 -arg2 value2 -arg3 value3"
# will be equivalent to
# arg1 <- "value1"
# arg2 <- "value2"
# arg3 <- "value3"
parse_args <- function(print_on = TRUE){
  
  args <- commandArgs(trailingOnly = TRUE)
  
  # odd elements are the names of the arguments (without the leading "-")
  args_names <- gsub("-", "", args[c(TRUE, FALSE)])
  # even elements are the values of the arguments
  args_values <- args[c(FALSE, TRUE)]
  
  # loop over the arguments to assign values
  for(i in seq_along(args_names)){
    assign(x = args_names[i], value = args_values[i], envir = .GlobalEnv)
    
    if(isTRUE(print_on)){
      print(
        paste0(args_names[i], " = ", get(x = args_names[i], envir = .GlobalEnv))
      )
    }
  }
  
  invisible(args_names)
}
```

In order not to lose the compatability with RStudio/interactive mode,
```r
#detect if whether R script is launched in batch mode or RStudio mode
batch_mode_on <- is.na(Sys.getenv("RSTUDIO", unset = NA))

#assign args values accordingly
if(batch_mode_on){
  cat("Running in batch mode\r\n")
  
  # assign args passed from batch call
  parse_args(print_on = FALSE)  
  
}else{
  cat("Running in RStudio mode\r\n")
  
  # assign args manually
  arg1 <- "m1"
  arg2 <- "m2"
  arg3 <- "m3"
}

#validate args values
print(paste0("arg1 = ", arg1))
print(paste0("arg2 = ", arg2))
print(paste0("arg3 = ", arg3))
```

To prevent the command line window from auto-exit, put a blocking operation at the end of the script.
```r
if(batch_mode_on){
  cat("Job finished. Press CTRL + C to exit\r\n")
  invisible(readLines(file("stdin"), 1))
}
```

Note that `start` command enables all R script to be executed in a parallel fashion.
```bash
:: set path for the rscript.exe file
set rscript=path\to\rscript.exe
:: run rscripts in parallel
start %rscript% cmd_example.R -arg1 job1 -arg2 value1.2 -arg3 value1.3
start %rscript% cmd_example.R -arg1 job2 -arg2 value2.2 -arg3 value2.3
start %rscript% cmd_example.R -arg1 job3 -arg2 value3.2 -arg3 value3.3
:: prevent the main batch window from auto-exit
pause
```
