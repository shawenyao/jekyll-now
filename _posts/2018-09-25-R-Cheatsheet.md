---
layout: post
title: R Cheatsheet
tag:
  - r
comments: true
ads: true
keyboard: true
---

The R commands that have made my life easier.

#### Hassle-free data.frame copy and paste (into or from Microsoft Excel)

```r
# copy
%>% write.table("clipboard-128", sep = "\t", row.names = FALSE)
# paste
read.table("clipboard-128", sep = "\t", header = TRUE)
```

#### Set working directory to where the source file is located

```r
setwd(dirname(sys.frame(1)$ofile))
```

#### Instantly convert Windows-style path to R-compliant format

Copy the path from File Explorer and

```r
path <- readClipboard()
```

#### Globally disable string as factors

```r
options(stringsAsFactors = FALSE)
```

Note that this has become the default behaviour since R 4.0.0.

#### Save a copy of console output to file
```r
sink("log.txt", split = TRUE)
# your original script here
sink()
```

#### Remove leading zeros in a character vector

```r
remove_leading_zeros <- function(character_vector){
  character_vector %>% 
    as.character() %>%
    # extract character from the first non-zero element to the end
    # unless it's all 0s, in which case return the character unchanged
    substr(start = regexpr(pattern = "[^0]", text = .), stop = nchar(.))
}
```
#### Fix the "unable to move temporary installation" issue

```r
trace(utils:::unpackPkgZip, edit = TRUE)
```
Replace `Sys.sleep(0.5)` with `Sys.sleep(2.5)` on line 142.

