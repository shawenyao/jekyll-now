---
layout: post
title: Productionizing R Scripts with Batch Mode
tag:
  - r
  - windows
comments: true
---

And parse argument at the same time.


### Objective

```bash
:: set path for the executable file
set rscript=path-to-rscript.exe
:: run rscripts in parallel
start %rscript% cmd_example.R -arg1 job1 -arg2 value1 -arg3 value1
start %rscript% cmd_example.R -arg1 job2 -arg2 value2 -arg3 value2
start %rscript% cmd_example.R -arg1 job3 -arg2 value3 -arg3 value3
:: prevent the main batch window from auto-exit
pause
```
Note that `start` command enables all R script to be executed in a parallel fashion.

### Running R Script with Arguments
Parsing arguments in R mainly revolves around the use of `commandArgs` function. It simply converts all arguments (space-delimited) specified in the batch call to a character vector, and it's up to the users to decide what to do with them.
```r
args <- commandArgs(trailingOnly = TRUE)
```

For example, suppose all arguments follow the "-arg value" format. As a result, odd elements stand for argument names, whereas even elements are the values.
```r
# odd elements are the names of the arguments (without the leading "-")
args_names <- gsub("-", "", args[c(TRUE, FALSE)])
# even elements are the values of the arguments
args_values <- args[c(FALSE, TRUE)]
```

The. It's also important to assign them in the global environment if 
```r
# loop over the arguments to assign values
for(i in seq_along(args_names)){
  assign(x = args_names[i], value = args_values[i], envir = .GlobalEnv)
}
```
  
### Compatability with RStudio/Interactive Mode
In order not to lose the compatability with RStudio/interactive mode,
```r
# detect if whether R script is launched in batch mode or RStudio mode
batch_mode_on <- is.na(Sys.getenv("RSTUDIO", unset = NA))

# assign args values accordingly
if(batch_mode_on){
  cat("Running in batch mode\r\n")
  
  # assign args passed from batch call
  parse_args()  
  
}else{
  cat("Running in RStudio mode\r\n")
  
  # assign args manually
  arg1 <- "m1"
  arg2 <- "m2"
  arg3 <- "m3"
}

# start your job
```

### Prevent Auto-Exit
To prevent the command line window from auto-exit, put a blocking operation at the end of the script.
```r
if(batch_mode_on){
  cat("Job finished. Press CTRL + C to exit\r\n")
  invisible(readLines(file("stdin"), 1))
}
```

