---
layout: post
title: R Cheatsheet
---

The R commands that has made my life easier.

#### Fast copying-and-pasting to excel

`%>% write.table("clipboard-128", row.names = FALSE, sep = "\t")`

#### Globally disable string as factors

`options(stringsAsFactors = FALSE)`

#### Remove leading zeros in a character vector

```
remove_leading_zeros <- function(character_vector){
  character_vector %>% 
    as.character() %>%
    # extract character from the first non-zero element to the end
    substr(.,regexpr("[^0]",.),nchar(.))
}
```
