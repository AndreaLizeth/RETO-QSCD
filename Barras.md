Barras
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
#CONEXIÓN XLSX

datos <- read.xlsx("D:/Escritorio/Cdatos/empresas_HEBM18.xlsx", na.strings = T)
datos <-  datos %>% filter(complete.cases(.)) #filtra la bdd para que quede con datos completos
```

``` r
#TABLA DE DATOS
nuevadata <- datos %>% 
  select(NOMBRE, REGIÓN,PROVINCIA,CIUDAD,INGRESOS,CANT..EMPLEADOS,UTILIDAD) %>% 
  filter(REGIÓN=="SIERRA",INGRESOS <=100000 & INGRESOS > 10000)
  
nuevadata$INGRESOS <- nuevadata$INGRESOS/1000
nuevadata$UTILIDAD <- nuevadata$UTILIDAD/1000  

tabla_frecuencia <- fdt(nuevadata$INGRESOS,start = 10,end = 100,h=10)
tabla_frecuencia1 <- data.frame(tabla_frecuencia$table)
tabla_frecuencia1$rango <- seq(20,100,10)
tabla_frecuencia1$cf... <- round(tabla_frecuencia1$cf..., 0)


View(tabla_frecuencia1)
```

``` r
#PLOT
g2 <- ggplot(data=tabla_frecuencia1, 
       aes(x=seq(10,90,10),
           y=cf...))+
  geom_bar(stat = "identity", fill="skyblue")+
  geom_text(aes(label=cf...), position = "identity",vjust=0,size=6)+
  geom_line()+geom_point()+
  theme(axis.text.x = element_text(size = 12, angle = 0))+
  labs(title = "Frecuencia relativa acumulada de los ingresos anuales", subtitle = "Pequeñas empresas Región Sierra del Ecuador")+
  xlab("Ingresos por rango en miles")+
  ylab("Distribución acumilada %")
g2 
```

![](unnamed-chunk-4-1.png)<!-- -->
