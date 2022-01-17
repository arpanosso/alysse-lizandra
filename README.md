
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
macro <- macro |> 
  filter(nome != 18)
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
micro <- micro |> 
  filter(nome != 18)
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
#> Tratamento  1 424.92 424.92 73.733 6.3509e-10
#> Residuo    33 190.18   5.76                  
#> Total      34 615.10                         
#> ------------------------------------------------------------------------
#> CV = 24.75 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.07732946 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.8806456 
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
#>            GL     SQ      QM     Fc    Pr>Fc
#> Tratamento  1 11.633 11.6325 5.7314 0.022505
#> Residuo    33 66.977  2.0296                
#> Total      34 78.610                        
#> ------------------------------------------------------------------------
#> CV = 15.68 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.2231867 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.2667449 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> Teste de Tukey
#> ------------------------------------------------------------------------
#> Grupos Tratamentos Medias
#> a     0   9.259375 
#>  b    1   7.2 
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: altura_test"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL     SQ     QM     Fc    Pr>Fc
#> Tratamento  1  7.280 7.2800 5.7554 0.022245
#> Residuo    33 41.742 1.2649                
#> Total      34 49.022                       
#> ------------------------------------------------------------------------
#> CV = 18.37 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.6342936 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.8807381 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> Teste de Tukey
#> ------------------------------------------------------------------------
#> Grupos Tratamentos Medias
#> a     0   6.2625 
#>  b    1   4.633333 
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: espessura_test"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL     SQ     QM     Fc   Pr>Fc
#> Tratamento  1  6.753 6.7528 4.9154 0.03362
#> Residuo    33 45.336 1.3738               
#> Total      34 52.089                      
#> ------------------------------------------------------------------------
#> CV = 22.39 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.1926213 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.4235565 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> Teste de Tukey
#> ------------------------------------------------------------------------
#> Grupos Tratamentos Medias
#> a     0   5.369063 
#>  b    1   3.8 
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: peso_ep"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL     SQ     QM     Fc   Pr>Fc
#> Tratamento  1  201.1 201.09 1.1609 0.28887
#> Residuo    34 5889.5 173.22               
#> Total      35 6090.6                      
#> ------------------------------------------------------------------------
#> CV = 48.52 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.0001593179 
#> ATENCAO: a 5% de significancia, os residuos nao podem ser considerados normais!
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.1197531 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> De acordo com o teste F, as medias nao podem ser consideradas diferentes.
#> ------------------------------------------------------------------------
#>   Niveis   Medias
#> 1      0 26.29219
#> 2      1 33.81250
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: peso_test"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL     SQ    QM     Fc      Pr>Fc
#> Tratamento  1  34420 34420 13.322 0.00087214
#> Residuo    34  87848  2584                  
#> Total      35 122267                        
#> ------------------------------------------------------------------------
#> CV = 39.72 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.4650483 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.6063952 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> Teste de Tukey
#> ------------------------------------------------------------------------
#> Grupos Tratamentos Medias
#> a     0   138.9097 
#>  b    1   40.52 
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: comp_ep"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL     SQ     QM     Fc    Pr>Fc
#> Tratamento  1  32.85 32.852 3.3421 0.076867
#> Residuo    32 314.55  9.830                
#> Total      33 347.41                       
#> ------------------------------------------------------------------------
#> CV = 18.36 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.000299192 
#> ATENCAO: a 5% de significancia, os residuos nao podem ser considerados normais!
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.8234074 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> De acordo com o teste F, as medias nao podem ser consideradas diferentes.
#> ------------------------------------------------------------------------
#>   Niveis   Medias
#> 1      0 16.76774
#> 2      1 20.23333
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: idade"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL      SQ     QM         Fc   Pr>Fc
#> Tratamento  1   0.004 0.0039 0.00046057 0.98301
#> Residuo    32 272.467 8.5146                   
#> Total      33 272.471                          
#> ------------------------------------------------------------------------
#> CV = 52.77 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  9.19745e-06 
#> ATENCAO: a 5% de significancia, os residuos nao podem ser considerados normais!
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.01363117 
#> ATENCAO: a 5% de significancia, as variancias nao podem ser consideradas homogeneas!
#> ------------------------------------------------------------------------
#> 
#> De acordo com o teste F, as medias nao podem ser consideradas diferentes.
#> ------------------------------------------------------------------------
#>   Niveis   Medias
#> 1      0 5.533333
#> 2      1 5.500000
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: peso"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL    SQ     QM     Fc   Pr>Fc
#> Tratamento  1  6592 6591.8 2.4141 0.13008
#> Residuo    32 87376 2730.5               
#> Total      33 93968                      
#> ------------------------------------------------------------------------
#> CV = 12.35 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.5303557 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.1185955 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> De acordo com o teste F, as medias nao podem ser consideradas diferentes.
#> ------------------------------------------------------------------------
#>   Niveis   Medias
#> 1      0 418.0333
#> 2      1 461.2500
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
#> Tratamento  1  622705 622705 1.4677 0.24057
#> Residuo    19 8061298 424279               
#> Total      20 8684003                      
#> ------------------------------------------------------------------------
#> CV = 42.46 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.2697686 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.03563095 
#> ATENCAO: a 5% de significancia, as variancias nao podem ser consideradas homogeneas!
#> ------------------------------------------------------------------------
#> 
#> De acordo com o teste F, as medias nao podem ser consideradas diferentes.
#> ------------------------------------------------------------------------
#>   Niveis   Medias
#> 1      0 1617.692
#> 2      1 1179.165
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: diam_ts_test"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL    SQ      QM     Fc      Pr>Fc
#> Tratamento  1 22101 22101.4 19.678 0.00025397
#> Residuo    20 22463  1123.2                  
#> Total      21 44564                          
#> ------------------------------------------------------------------------
#> CV = 20.67 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.6089511 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.240485 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> Teste de Tukey
#> ------------------------------------------------------------------------
#> Grupos Tratamentos Medias
#> a     0   177.0589 
#>  b    1   94.88105 
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: ept_ts_test"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL     SQ      QM     Fc      Pr>Fc
#> Tratamento  1 2826.5 2826.48 40.373 3.3568e-06
#> Residuo    20 1400.2   70.01                  
#> Total      21 4226.7                          
#> ------------------------------------------------------------------------
#> CV = 25.03 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.8311935 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.82456 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> Teste de Tukey
#> ------------------------------------------------------------------------
#> Grupos Tratamentos Medias
#> a     0   38.76549 
#>  b    1   9.37761 
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: diam_co_ep"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL     SQ     QM     Fc      Pr>Fc
#> Tratamento  1 124633 124633 17.454 0.00046419
#> Residuo    20 142813   7141                  
#> Total      21 267446                         
#> ------------------------------------------------------------------------
#> CV = 22.78 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.2418391 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.8480155 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> Teste de Tukey
#> ------------------------------------------------------------------------
#> Grupos Tratamentos Medias
#> a     0   406.4212 
#>  b    1   211.274 
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: ept_co_ep"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL     SQ     QM     Fc     Pr>Fc
#> Tratamento  1 1055.6 1055.6 14.662 0.0010488
#> Residuo    20 1440.0   72.0                 
#> Total      21 2495.6                        
#> ------------------------------------------------------------------------
#> CV = 16.71 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.6816574 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.8345766 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> Teste de Tukey
#> ------------------------------------------------------------------------
#> Grupos Tratamentos Medias
#> a     0   54.03038 
#>  b    1   36.0705 
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: diam_ca_ep"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL      SQ     QM     Fc    Pr>Fc
#> Tratamento  1  696784 696784 5.1099 0.035721
#> Residuo    19 2590814 136359                
#> Total      20 3287597                       
#> ------------------------------------------------------------------------
#> CV = 33.94 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.2454715 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.4893386 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> Teste de Tukey
#> ------------------------------------------------------------------------
#> Grupos Tratamentos Medias
#> a     0   1162.229 
#>  b    1   641.6803 
#> ------------------------------------------------------------------------
#> [1] "######################################"
#> [1] "Análise para: ept_ca_ep"
#> [1] "######################################"
#> ------------------------------------------------------------------------
#> Quadro da analise de variancia
#> ------------------------------------------------------------------------
#>            GL     SQ      QM        Fc   Pr>Fc
#> Tratamento  1   0.19  0.1903 0.0069835 0.93427
#> Residuo    19 517.74 27.2493                  
#> Total      20 517.93                          
#> ------------------------------------------------------------------------
#> CV = 28.14 %
#> 
#> ------------------------------------------------------------------------
#> Teste de normalidade dos residuos ( Shapiro-Wilk ) 
#> Valor-p:  0.5866484 
#> De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
#> ------------------------------------------------------------------------
#> 
#> ------------------------------------------------------------------------
#> Teste de homogeneidade de variancia 
#> valor-p:  0.3244819 
#> De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
#> ------------------------------------------------------------------------
#> 
#> De acordo com o teste F, as medias nao podem ser consideradas diferentes.
#> ------------------------------------------------------------------------
#>   Niveis   Medias
#> 1      0 18.58904
#> 2      1 18.31700
#> ------------------------------------------------------------------------
```
