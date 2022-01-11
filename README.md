
<!-- README.md is generated from README.Rmd. Please edit that file -->

# Análise Álysse e Lizandra

## Citação do R

``` r
citation()
#> 
#> To cite R in publications use:
#> 
#>   R Core Team (2021). R: A language and environment for statistical
#>   computing. R Foundation for Statistical Computing, Vienna, Austria.
#>   URL https://www.R-project.org/.
#> 
#> A BibTeX entry for LaTeX users is
#> 
#>   @Manual{,
#>     title = {R: A Language and Environment for Statistical Computing},
#>     author = {{R Core Team}},
#>     organization = {R Foundation for Statistical Computing},
#>     address = {Vienna, Austria},
#>     year = {2021},
#>     url = {https://www.R-project.org/},
#>   }
#> 
#> We have invested a lot of time and effort in creating R, please cite it
#> when using it for data analysis. See also 'citation("pkgname")' for
#> citing R packages.
```

## Carregando pacotes

``` r
library(readxl)
library(tidyverse)
library(ExpDes.pt)
```

## Entrada de dados

``` r
macro<- read_excel("data/Analise morfo macro.xlsx",na = "NA") |> 
  janitor::clean_names()
glimpse(macro)
#> Rows: 38
#> Columns: 12
#> $ nome               <dbl> 1, 1, 2, 2, 3, 3, 4, 4, 5, 5, 6, 6, 7, 7, 8, 8, 9, ~
#> $ criptorquida       <dbl> 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, ~
#> $ test               <chr> "D", "E", "D", "E", "D", "E", "D", "E", "D", "E", "~
#> $ larg_saco_escrotal <dbl> 8.0, 8.0, 15.0, 15.0, 8.0, 0.0, 10.0, 10.0, 10.0, 1~
#> $ comp_test          <dbl> 7.0, 7.4, 10.0, 11.0, 10.0, NA, 7.2, 8.0, 9.0, 8.0,~
#> $ altura_test        <dbl> 5.0, 5.0, 7.0, 8.0, 7.0, NA, 4.0, 5.0, 6.0, 5.5, 6.~
#> $ espessura_test     <dbl> 3.849, 2.973, 5.439, 5.696, 4.895, NA, 3.634, 3.894~
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

## Análise para MACRO

``` r
for(i in 4:length(macro)){
  y <- macro[i] |>  pull()
  print("######################################")
  print(paste0("Análise para: ",names(macro[i])))
  print("######################################")
  criptorquida <- macro[2] |>  pull() |> as.factor()
  dic(criptorquida[!is.na(y)], y[!is.na(y)])
  }
#> [1] "######################################"
#> [1] "Análise para: larg_saco_escrotal"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL     SQ     QM     Fc      Pr>Fc
#> Tratamento  1 516.40 516.40 92.322 3.2118e-11
#> Residuo    34 190.18   5.59                  
#> Total      35 706.58                         
#> ------------------------------------------------------------------------
#> CV = 25.08 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.0821135 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.6764021 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> Teste de Tukey
#> ------------------------------------------------------------------------
#> Grupos Tratamentos Medias
#> a     0   10.95161 
#>  b    1   0 
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: comp_test"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL     SQ     QM     Fc    Pr>Fc
#> Tratamento  1 20.666 20.666 10.517 0.002601
#> Residuo    35 68.777  1.965                
#> Total      36 89.443                       
#> ------------------------------------------------------------------------
#> CV = 15.54 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.3559967 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.5279812 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> Teste de Tukey
#> ------------------------------------------------------------------------
#> Grupos Tratamentos Medias
#> a     0   9.281818 
#>  b    1   6.875 
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: altura_test"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL    SQ      QM     Fc     Pr>Fc
#> Tratamento  1 12.08 12.0803 9.4021 0.0041612
#> Residuo    35 44.97  1.2849                 
#> Total      36 57.05                         
#> ------------------------------------------------------------------------
#> CV = 18.53 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.4291656 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.34355 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> Teste de Tukey
#> ------------------------------------------------------------------------
#> Grupos Tratamentos Medias
#> a     0   6.315152 
#>  b    1   4.475 
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: espessura_test"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL     SQ     QM     Fc    Pr>Fc
#> Tratamento  1  9.380 9.3802 6.8056 0.013276
#> Residuo    35 48.241 1.3783                
#> Total      36 57.621                       
#> ------------------------------------------------------------------------
#> CV = 22.38 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.1312682 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.6581505 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> Teste de Tukey
#> ------------------------------------------------------------------------
#> Grupos Tratamentos Medias
#> a     0   5.421515 
#>  b    1   3.8 
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: peso_ep"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL     SQ      QM      Fc   Pr>Fc
#> Tratamento  1   53.5  53.545 0.30976 0.58127
#> Residuo    36 6223.0 172.861                
#> Total      37 6276.6                        
#> ------------------------------------------------------------------------
#> CV = 48.77 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  1.872858e-05 
#> ATENCAO: a 5% de significancia, os residuos nao podem ser considerados normais!
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.2396317 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> De acordo com o teste F, as medias nao podem ser consideradas diferentes.
#> ------------------------------------------------------------------------
#>   Niveis   Medias
#> 1      0 26.49636
#> 2      1 30.00800
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: peso_test"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL     SQ    QM    Fc      Pr>Fc
#> Tratamento  1  44980 44980 17.13 0.00020061
#> Residuo    36  94527  2626                 
#> Total      37 139508                       
#> ------------------------------------------------------------------------
#> CV = 40.02 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.3803484 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.5142245 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> Teste de Tukey
#> ------------------------------------------------------------------------
#> Grupos Tratamentos Medias
#> a     0   141.4218 
#>  b    1   39.642 
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: comp_ep"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL     SQ     QM     Fc   Pr>Fc
#> Tratamento  1  21.51 21.506 2.2139 0.14599
#> Residuo    34 330.28  9.714               
#> Total      35 351.78                      
#> ------------------------------------------------------------------------
#> CV = 18.21 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.001846333 
#> ATENCAO: a 5% de significancia, os residuos nao podem ser considerados normais!
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.6765447 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> De acordo com o teste F, as medias nao podem ser consideradas diferentes.
#> ------------------------------------------------------------------------
#>   Niveis   Medias
#> 1      0 16.84062
#> 2      1 19.30000
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: idade"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL      SQ     QM       Fc   Pr>Fc
#> Tratamento  1   0.645 0.6452 0.077413 0.78252
#> Residuo    34 283.355 8.3340                 
#> Total      35 284.000                        
#> ------------------------------------------------------------------------
#> CV = 50.94 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  2.601132e-05 
#> ATENCAO: a 5% de significancia, os residuos nao podem ser considerados normais!
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.6252111 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> De acordo com o teste F, as medias nao podem ser consideradas diferentes.
#> ------------------------------------------------------------------------
#>   Niveis   Medias
#> 1      0 5.612903
#> 2      1 6.000000
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: peso"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL    SQ     QM     Fc   Pr>Fc
#> Tratamento  1  4061 4060.5 1.5105 0.22751
#> Residuo    34 91400 2688.2               
#> Total      35 95461                      
#> ------------------------------------------------------------------------
#> CV = 12.3 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.7198604 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.3998317 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> De acordo com o teste F, as medias nao podem ser consideradas diferentes.
#> ------------------------------------------------------------------------
#>   Niveis   Medias
#> 1      0 417.2903
#> 2      1 448.0000
#> ------------------------------------------------------------------------
```

## Análise para MICRO

``` r
micro_aux <- micro |> 
  group_by(nome, criptorquida) |> 
  summarise(
    al_ta_test = mean(al_ta_test, na.rm=TRUE),
    diam_ts_test = mean(diam_ts_test, na.rm=TRUE),
    ept_ts_test = mean(ept_ts_test, na.rm=TRUE),
    diam_co_ep = mean(diam_co_ep, na.rm=TRUE),
    ept_co_ep = mean(ept_co_ep, na.rm=TRUE),
    diam_ca_ep = mean(diam_ca_ep, na.rm=TRUE),
    ept_ca_ep = mean(ept_ca_ep, na.rm=TRUE)
  )
#> `summarise()` has grouped output by 'nome'. You can override using the `.groups` argument.
for(i in 3:length(micro_aux)){
  y <- micro_aux[i] |>  pull()
  print("######################################")
  print(paste0("Análise para: ",names(micro_aux[i])))
  print("######################################")
  criptorquida <- micro_aux[2] |>  pull() |> as.factor()
  dic(criptorquida[!is.na(y)], y[!is.na(y)],mcomp = "tukey")
  }
#> [1] "######################################"
#> [1] "Análise para: al_ta_test"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL      SQ     QM     Fc   Pr>Fc
#> Tratamento  1  766662 766662 1.9448 0.17772
#> Residuo    21 8278348 394207               
#> Total      22 9045010                      
#> ------------------------------------------------------------------------
#> CV = 40.57 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.4530086 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.3214021 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> De acordo com o teste F, as medias nao podem ser consideradas diferentes.
#> ------------------------------------------------------------------------
#>   Niveis   Medias
#> 1      0 1643.728
#> 2      1 1201.094
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: diam_ts_test"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL    SQ      QM     Fc      Pr>Fc
#> Tratamento  1 25227 25227.4 24.333 6.2001e-05
#> Residuo    22 22809  1036.8                  
#> Total      23 48036                          
#> ------------------------------------------------------------------------
#> CV = 19.99 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.3668818 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.5697262 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> Teste de Tukey
#> ------------------------------------------------------------------------
#> Grupos Tratamentos Medias
#> a     0   177.747 
#>  b    1   97.9145 
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: ept_ts_test"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL     SQ      QM     Fc      Pr>Fc
#> Tratamento  1 2969.5 2969.45 42.153 1.5676e-06
#> Residuo    22 1549.8   70.44                  
#> Total      23 4519.2                          
#> ------------------------------------------------------------------------
#> CV = 25.83 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.804654 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.9519695 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> Teste de Tukey
#> ------------------------------------------------------------------------
#> Grupos Tratamentos Medias
#> a     0   38.20254 
#>  b    1   10.81317 
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: diam_co_ep"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL     SQ     QM     Fc      Pr>Fc
#> Tratamento  1 133220 133220 19.284 0.00025488
#> Residuo    21 145074   6908                  
#> Total      22 278294                         
#> ------------------------------------------------------------------------
#> CV = 22.69 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.2686289 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.9353295 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> Teste de Tukey
#> ------------------------------------------------------------------------
#> Grupos Tratamentos Medias
#> a     0   406.4212 
#>  b    1   221.908 
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: ept_co_ep"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL     SQ      QM     Fc      Pr>Fc
#> Tratamento  1 1270.8 1270.84 18.532 0.00031337
#> Residuo    21 1440.0   68.57                  
#> Total      22 2710.9                          
#> ------------------------------------------------------------------------
#> CV = 16.52 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.6354971 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.8912152 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> Teste de Tukey
#> ------------------------------------------------------------------------
#> Grupos Tratamentos Medias
#> a     0   54.03038 
#>  b    1   36.009 
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: diam_ca_ep"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL      SQ     QM    Fc   Pr>Fc
#> Tratamento  1  297750 297750 1.881 0.18542
#> Residuo    20 3165934 158297              
#> Total      21 3463684                     
#> ------------------------------------------------------------------------
#> CV = 35.93 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.2936929 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.6267435 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> De acordo com o teste F, as medias nao podem ser consideradas diferentes.
#> ------------------------------------------------------------------------
#>   Niveis    Medias
#> 1      0 1162.2294
#> 2      1  860.6019
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: ept_ca_ep"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL     SQ     QM      Fc   Pr>Fc
#> Tratamento  1  13.29 13.285 0.47945 0.49663
#> Residuo    20 554.18 27.709                
#> Total      21 567.47                       
#> ------------------------------------------------------------------------
#> CV = 28.89 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.6022127 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.3391196 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> De acordo com o teste F, as medias nao podem ser consideradas diferentes.
#> ------------------------------------------------------------------------
#>   Niveis   Medias
#> 1      0 18.58904
#> 2      1 16.57425
#> ------------------------------------------------------------------------
```
