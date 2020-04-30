---
layout: post
title: R Cheatsheet
tag:
  - r
comments: false
ads: false
---

The R commands that have made my life easier.

#### Hassle-free data.frame copy-and-paste (into Microsoft Excel)

```r
%>% write.table("clipboard-128", row.names = FALSE, sep = "\t")
```

#### Set working directory to the place where the source file is saved

```r
setwd(dirname(sys.frame(1)$ofile))
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

