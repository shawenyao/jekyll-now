---
layout: post
title: R Cheatsheet
tag:
  - r
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
