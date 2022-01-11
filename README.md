
<!-- README.md is generated from README.Rmd. Please edit that file -->

# Análise Álysse e Lizandra

## Carregando pacotes

``` r
library(readxl)
library(tidyverse)
```

## Entrada de dados

``` r
macro<- read_excel("data/Analise morfo macro.xlsx",na = "NA") |> 
  janitor::clean_names()
glimpse(macro)
#> Rows: 38
#> Columns: 14
#> $ nome               <dbl> 1, 1, 2, 2, 3, 3, 4, 4, 5, 5, 6, 6, 7, 7, 8, 8, 9, ~
#> $ criptorquida       <dbl> 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, ~
#> $ test               <chr> "D", "E", "D", "E", "D", "E", "D", "E", "D", "E", "~
#> $ larg_saco_escrotal <dbl> 8.0, 8.0, 15.0, 15.0, 8.0, 0.0, 10.0, 10.0, 10.0, 1~
#> $ comp_test          <dbl> 7.0, 7.4, 10.0, 11.0, 10.0, NA, 7.2, 8.0, 9.0, 8.0,~
#> $ altura_test        <dbl> 5.0, 5.0, 7.0, 8.0, 7.0, NA, 4.0, 5.0, 6.0, 5.5, 6.~
#> $ espessura_test     <dbl> 3.849, 2.973, 5.439, 5.696, 4.895, NA, 3.634, 3.894~
#> $ comp_lpt           <dbl> 1.800, 1.600, 0.971, 1.156, 0.843, NA, 1.200, 1.500~
#> $ comp_lcep          <dbl> 0.400, NA, 1.152, NA, 0.261, NA, NA, 1.000, 1.600, ~
#> $ peso_ep            <dbl> 22.85, 19.27, 25.79, 29.05, 22.41, 87.34, 24.06, 27~
#> $ peso_test          <dbl> 50.15, 48.85, 156.92, 183.88, 138.66, 25.36, 88.85,~
#> $ comp_ep            <dbl> 16.0, 16.0, 17.5, 16.0, NA, NA, 16.5, 13.0, 20.7, 2~
#> $ idade              <dbl> 10, 10, 10, 10, 3, 3, 3, 3, 3, 3, 4, 4, 7, 7, 11, 1~
#> $ peso               <dbl> 360, 360, 450, 450, 405, 405, 320, 320, 435, 435, 4~
```

``` r
micro<- read_excel("data/Analise morfo micro.xlsx",na = "NA")|> 
  janitor::clean_names()
glimpse(micro)
#> Rows: 720
#> Columns: 9
#> $ nome         <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, ~
#> $ criptorquida <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, ~
#> $ al_ta_test   <dbl> 709.1457, 720.2731, 710.9487, 699.5358, 696.3853, 683.621~
#> $ diam_ts_test <dbl> 241.0188, 237.2855, 190.0757, 199.3484, 256.1928, 218.271~
#> $ ept_ts_test  <dbl> 39.52562, 41.14578, 44.65416, 34.82315, 26.96330, 22.5138~
#> $ diam_co_ep   <dbl> 325.0583, 345.0599, 379.2505, 402.1954, 392.6365, 409.818~
#> $ ept_co_ep    <dbl> 70.60, 53.96, 73.13, 64.38, 58.33, 64.09, 59.59, 61.18, 5~
#> $ diam_ca_ep   <dbl> 1454.81, 1564.12, 1895.64, 1446.38, 1614.38, 1491.84, 169~
#> $ ept_ca_ep    <dbl> 11.66232, 12.29317, 16.87250, 18.43422, 11.16125, 15.9772~
```
