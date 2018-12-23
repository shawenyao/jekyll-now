---
layout: post
title: Productionize R Scripts with Batch Mode
tag:
  - windows
  - r
comments: true
---

Sometimes R is better off without RStudio.

<p align="center">
  <img src="https://shawenyao.github.io/R/images/cmd_example.png" />
</p>

## Objective: Running R Scripts in Batch Mode
R supports batch mode out of the box. All it takes is to launch R script with `rscript.exe` in command line.
```bash
set rscript=full-path-to-rscript.exe
start %rscript% cmd_example.R -arg1 job1 -arg2 value1 -arg3 value1
start %rscript% cmd_example.R -arg1 job2 -arg2 value2 -arg3 value2
start %rscript% cmd_example.R -arg1 job3 -arg2 value3 -arg3 value3
pause
```
Note that Windows' `start` command enables each subsequent command to be executed in a parallel fashion. Without `start`, sequential execution would be assumed instead.

This is working *already*, but there are a few more things that would make the experience smoother.

## Parsing Arguments
Parsing arguments in R mainly revolves around using the `commandArgs` function. It does one simple job: converting all (space-delimited) arguments specified in the batch call into a character vector, and it's up to the users to decide what to do with them.
```r
args <- commandArgs(trailingOnly = TRUE)
```

For example, suppose all arguments come in the form of "`-arg value`" pairs, i.e., odd elements stand for argument names and even ones are the values.
```r
# odd elements are the names of the arguments (without the leading "-")
args_names <- gsub("-", "", args[c(TRUE, FALSE)])
# even elements are the values of the arguments
args_values <- args[c(FALSE, TRUE)]
```

The `assign` function can then be used for dynamic variable declaration. It's also important to explicitly assign them in the global environment if you plan to wrap the whole argument processing chunk into a function.
```r
for(i in seq_along(args_names)){
  assign(x = args_names[i], value = args_values[i], envir = .GlobalEnv)
}
```
  
## Compatability with RStudio/Interactive Mode
Batch mode is practically useless when it comes to debugging. In order not to lose the compatability with RStudio/interactive mode, a conditional statement can be put in the very beginning to differentiate the two approaches.
```r
# detect if whether R script is launched in batch mode or RStudio mode
batch_mode_on <- is.na(Sys.getenv("RSTUDIO", unset = NA))

if(batch_mode_on){
  cat("Running in batch mode\r\n")
  
  # assign args passed from batch call
  # or wrap it into a function
  parse_args()
}else{
  cat("Running in iteractive mode\r\n")
  
  # assign args manually
  arg1 <- "some value"
  arg2 <- "some value"
  arg3 <- "some value"
}

# start your job here
```

## Preventing Auto-Exit
To prevent the command line window from automatically closing itself upon completion, put a blocking operation at the end of the script.
```r
if(batch_mode_on){
  cat("Job finished. Press CTRL + C to exit.\r\n")
  readLines(con = "stdin", n = 1)
}
```

And the window will remain open indefinitely, until user presses `CTRL + C` on the keyboard.

## Putting It All Together
For non-interactive/production use of R scripts:
* call `rscript` from command line to run them in batch mode, either sequentially (without `start`) or parallelly (with `start`)
* use the `commandArgs` function in R to parse the arguments into a character vector, and you get to choose how to use it
* distinguish between batch and interactive mode in the beginning of the script to retain compatability with RStudio
* put a blocking operation at the end to avoid auto-exit
