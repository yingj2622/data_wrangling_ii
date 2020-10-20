Reading Data from the Web
================
Ying Jin
2020/10/20

## Scrape a table

I want the first table from [this
page](http://samhda.s3-us-gov-west-1.amazonaws.com/s3fs-public/field-uploads/2k15StateFiles/NSDUHsaeShortTermCHG2015.htm)

read in the html

``` r
url = "http://samhda.s3-us-gov-west-1.amazonaws.com/s3fs-public/field-uploads/2k15StateFiles/NSDUHsaeShortTermCHG2015.htm"

drug_use_html = read_html(url)
```

extract the table(s); focus on the first one

``` r
table_marj = 
drug_use_html %>% 
  html_nodes(css = "table") %>% 
  first() %>% 
  html_table() %>% 
  slice(-1) %>% 
  as_tibble()
```

## Star Wars Movies info

I want the data from [here](https://www.imdb.com/list/ls070150896/)

``` r
url = "https://www.imdb.com/list/ls070150896/"

swm_html = read_html(url)
```

Grab elements that I want.

``` r
title_vec = 
  swm_html %>% 
  html_nodes(css = '.lister-item-header a') %>% 
  html_text()

gross_rev_vec = 
   swm_html %>% 
  html_nodes(css = '.text-muted .ghost~ .text-muted+ span') %>% 
  html_text()

run_time_vec = 
  swm_html %>% 
  html_nodes(css = '.runtime') %>% 
  html_text()

swm_df = 
  tibble(
    title = title_vec,
    gross_rev = gross_rev_vec,
    runtime = run_time_vec
  )
```
