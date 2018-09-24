---
layout: post
title: R Cheatsheet
---

The R commands that has made my life easier.

#### Fast copying-and-pasting into Microsoft Excel

```r
%>% write.table("clipboard-128", row.names = FALSE, sep = "\t")
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
