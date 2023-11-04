2.RegresiónSimple
================
Andrea Quishpe
2023-11-04

``` r
library(openxlsx)
```

    ## Warning: package 'openxlsx' was built under R version 4.3.2

``` r
library(dplyr)
```

    ## Warning: package 'dplyr' was built under R version 4.3.2

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library(fdth)
```

    ## Warning: package 'fdth' was built under R version 4.3.2

    ## 
    ## Attaching package: 'fdth'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     sd, var

``` r
library(ggplot2)
```

    ## Warning: package 'ggplot2' was built under R version 4.3.2

``` r
library(gridExtra)
```

    ## Warning: package 'gridExtra' was built under R version 4.3.2

    ## 
    ## Attaching package: 'gridExtra'

    ## The following object is masked from 'package:dplyr':
    ## 
    ##     combine

``` r
library(grid)
library(stargazer)
```

    ## 
    ## Please cite as:

    ##  Hlavac, Marek (2022). stargazer: Well-Formatted Regression and Summary Statistics Tables.

    ##  R package version 5.2.3. https://CRAN.R-project.org/package=stargazer

``` r
library(lmtest)
```

    ## Warning: package 'lmtest' was built under R version 4.3.2

    ## Loading required package: zoo

    ## Warning: package 'zoo' was built under R version 4.3.2

    ## 
    ## Attaching package: 'zoo'

    ## The following objects are masked from 'package:base':
    ## 
    ##     as.Date, as.Date.numeric

``` r
#CONEXIÓN XLSX
setwd("D:/Escritorio/Cdatos/")
datos <- read.xlsx("empresas_HEBM18.xlsx")

datos<- datos %>% 
 
  filter( INGRESOS !=0 & CANT..EMPLEADOS!=0 & PROVINCIA=="GUAYAS")


modelo <- lm(INGRESOS~ CANT..EMPLEADOS  #Igresos vs C
             ,data=datos)
summary(modelo)
```

    ## 
    ## Call:
    ## lm(formula = INGRESOS ~ CANT..EMPLEADOS, data = datos)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -439268 -193574  -76563  138947 4093811 
    ## 
    ## Coefficients:
    ##                  Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)     3.541e+05  3.028e+03  116.94   <2e-16 ***
    ## CANT..EMPLEADOS 1.852e+01  9.357e+00    1.98   0.0478 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 248200 on 6732 degrees of freedom
    ## Multiple R-squared:  0.0005818,  Adjusted R-squared:  0.0004333 
    ## F-statistic: 3.919 on 1 and 6732 DF,  p-value: 0.04779

``` r
stargazer(modelo, title = "Modelo de regresión simple", type = "text")
```

    ## 
    ## Modelo de regresión simple
    ## ===============================================
    ##                         Dependent variable:    
    ##                     ---------------------------
    ##                              INGRESOS          
    ## -----------------------------------------------
    ## CANT..EMPLEADOS              18.523**          
    ##                               (9.357)          
    ##                                                
    ## Constant                  354,145.900***       
    ##                             (3,028.393)        
    ##                                                
    ## -----------------------------------------------
    ## Observations                   6,734           
    ## R2                             0.001           
    ## Adjusted R2                   0.0004           
    ## Residual Std. Error   248,217.300 (df = 6732)  
    ## F Statistic           3.919** (df = 1; 6732)   
    ## ===============================================
    ## Note:               *p<0.1; **p<0.05; ***p<0.01

``` r
dwtest(modelo)
```

    ## 
    ##  Durbin-Watson test
    ## 
    ## data:  modelo
    ## DW = 1.6932, p-value < 2.2e-16
    ## alternative hypothesis: true autocorrelation is greater than 0

``` r
bptest(modelo)
```

    ## 
    ##  studentized Breusch-Pagan test
    ## 
    ## data:  modelo
    ## BP = 0.10759, df = 1, p-value = 0.7429

``` r
#QUEMAR EL MOTOR DE CÁLCULO
#MOTOR DE CÁLCULO -> algoritmo

nuevadata <- head(datos)
predict(modelo, nuevadata)
```

    ##        1        2        3        4        5        6 
    ## 354183.0 354220.0 354164.4 354331.2 354201.5 354220.0
