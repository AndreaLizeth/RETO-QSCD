# RETO-QSCD
Reto Quiero Ser Científico de Datos


Este trabajo forma parte del desafío "Reto Quiero Ser Científico de Datos".
Sigue las instrucciones:

 

1. Realizar un gráfico de barras considerando las empresas de la región SIERRA

  ![](unnamed-chunk-4-1.png)
  
2. Realiza una regresión simple que explique el ingreso en función de la cantidad de empleados. Para efectos del ejercicio, se debe filtrar los casos cuyo ingreso y cantidad de empleados sea igual a 0. La regresión sólo debe construirse usando la provincia del Guayas. Se debe reportar los resultados, la interpretación de los coeficientes, las pruebas de autocorrelación, heterocedasticidad.


## 
## Call:
## lm(formula = INGRESOS ~ CANT..EMPLEADOS, data = datos)
## 
## Residuals:
##      Min       1Q   Median       3Q      Max 
## -1221454  -190986   -67949   135604  2635552 
## 
## Coefficients:
##                  Estimate Std. Error t value Pr(>|t|)    
## (Intercept)     352108.24    3068.54  114.75  < 2e-16 ***
## CANT..EMPLEADOS    483.54      68.68    7.04 2.12e-12 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 237500 on 6321 degrees of freedom
## Multiple R-squared:  0.007781,   Adjusted R-squared:  0.007624 
## F-statistic: 49.57 on 1 and 6321 DF,  p-value: 2.12e-12

3. Realiza el mismo ejercicio del enunciado anterior, pero para pichincha. En este caso, sólo reporta los resultados y la explicación de los coeficiente.
 

