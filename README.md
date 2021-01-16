# Grafico-de-Araña-o-de-Radar-Basico

---
title: "Gráfico de Radar Básico o Araña"
author: "Naren Castellón"
date: "01/16/2021"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

El gráfico de radar también se denominan gráfico de araña o web o polares. Se dibujan utilizando la `library (fmsb)` .

El formato de los datos de entrada es muy específico. Cada fila debe ser una entidad. Cada columna es una variable cuantitativa. Las primeras 2 filas proporcionan el mínimo y el máximo que se utilizarán para cada variable.

Una vez que tenga este formato, la función `radarchart()` hará todo el trabajo por usted.

![](imagenes/radar.jpg)

## **Ejemplo 1**

```{r}
#install.packages("fmsb")
library(fmsb)
 
# Crear datos: nota en la escuela secundaria para Mateo:
data <- as.data.frame(matrix( sample( 2:20 , 10 , replace=T) , ncol=10))
colnames(data) <- c("math" , "english" , "Python" , "music" , "R-coding", "data-viz" , "french" , "physic", "statistic", "sport" )
 
# Para usar el paquete fmsb, tengo que agregar 2 líneas al marco de datos: el máximo y el mínimo de cada tema para mostrar en el gráfico!
data <- rbind(rep(20,10) , rep(0,10) , data)
 
# Check your data, it has to look like this!
# head(data)

# El gráfico de radar predeterminado 
radarchart(data,title="Gráfico de araña o de radar")
```

## **Ejemplo 2**

```{r}
# Library
library(fmsb)
 
# Crear datos: nota en la escuela secundaria para varios estudiantes
set.seed(99)
data <- as.data.frame(matrix( sample( 0:20 , 15 , replace=F) , ncol=5))
colnames(data) <- c("math" , "english" , "Python" , "music" , "R-coding" )
rownames(data) <- paste("mister" , letters[1:3] , sep="-")
 
# Para usar el paquete fmsb, tengo que agregar 2 líneas al marco de datos: el máximo y el mínimo de cada variable para mostrar en el gráfico!
data <- rbind(rep(20,5) , rep(0,5) , data)
 
# gráfico determinado:
radarchart(data,title="Gráfico de araña o de radar")
```

## **Personalización**

La función `radarchart()` ofrece varias opciones para personalizar el gráfico, mencionaremos que son las más básicas:

**Sintaxis**
```{r eval=FALSE}
radarchart(df, axistype, seg, pty, pcol, plty, plwd, pdensity, pangle, pfcol, 
 cglty, cglwd, cglcol, axislabcol, title, maxmin, na.itp, centerzero, 
 vlabels, vlcex, caxislabels, calcex, paxislabels, palcex, ...)
```


1. **Características del polígono:**

* **pcol** → color de línea
* **pfcol** → color de relleno
* **plwd** → ancho de línea

2. **Características de la cuadrícula:**

* **cglcol** → color de la red
* **cglty**→ tipo de línea neta (ver posibilidades )
* **axislabcol** → color de las etiquetas de los ejes
* **caxislabels** → vector de etiquetas de eje para mostrar
**cglwd** → ancho neto

3. **Etiquetas:**

* **vlcex** → tamaño de etiquetas de grupo

## **Ejemplo 1**

```{r}
# Library
library(fmsb)
 
# Crear datos: nota en la escuela secundaria para Jans:
data <- as.data.frame(matrix( sample( 2:20 , 10 , replace=T) , ncol=10))
colnames(data) <- c("matematática" , "english" , "biologia" , "music" , "R-coding", "Python" , "french" , "physic", "statistic", "sport" )
 
# Para usar el paquete fmsb, tengo que agregar 2 líneas al marco de datos: ¡el máximo y el mínimo de cada tema para mostrar en el gráfico!
data <- rbind(rep(20,10) , rep(0,10) , data)
 
# Comprueba tus datos, ¡tiene que verse así!
# head(data)

# Personalizar el gráfico de radar !
radarchart( data  , axistype=1 , title="Gráfico de araña o de radar",
 
    #polígono personalizado
    pcol=rgb(0.2,0.5,0.5,0.9) , pfcol=rgb(0.2,0.5,0.5,0.5) , plwd=2 , 
 
    #personalizar la cuadrícula
    cglcol="blue", cglty=1, axislabcol="red", caxislabels=seq(0,20,5), cglwd=1,
 
    #etiquetas personalizadas
    vlcex=1
    )
```
## **Ejemplo 2**

```{r}
# Library
library(fmsb)
 
# Crear datos: nota en la escuela secundaria para varios estudiantes
set.seed(99)
data <- as.data.frame(matrix( sample( 0:20 , 15 , replace=F) , ncol=5))
colnames(data) <- c("math" , "english" , "Python" , "music" , "R-coding" )
rownames(data) <- paste("mister" , letters[1:3] , sep="-")
 
# Para usar el paquete fmsb, tengo que agregar 2 líneas al marco de datos: el máximo y el mínimo de cada variable para mostrar en el gráfico!
data <- rbind(rep(20,5) , rep(0,5) , data)

# Color vector
colors_border=c( rgb(0.2,0.5,0.5,0.9), rgb(0.8,0.2,0.5,0.9) , rgb(0.7,0.5,0.1,0.9) )
colors_in=c( rgb(0.2,0.5,0.5,0.4), rgb(0.8,0.2,0.5,0.4) , rgb(0.7,0.5,0.1,0.4) )

# trazar con opciones predeterminadas:
radarchart( data  , axistype=1 , title="Gráfico de araña o de radar",
    #Poligono personalizado
    pcol=colors_border , pfcol=colors_in , plwd=4 , plty=1,
    #custom the grid
    cglcol="grey", cglty=1, axislabcol="grey", caxislabels=seq(0,20,5), cglwd=0.8,
    #Estiquetas personalizada
    vlcex=0.8 
    )

# Agregar leyendas
legend(x=0.7, y=1, legend = rownames(data[-c(1,2),]), bty = "n", pch=20 , col=colors_in , text.col = "grey", cex=1.2, pt.cex=3)
```

## **Limites de ejes**

En los ejemplos anteriores, los límites de los ejes se establecieron en las 2 primeras filas del conjunto de datos de entrada.

Si no especifica estos valores, los límites del eje se calcularán automáticamente, como se muestra a continuación.

```{r}
# Library
library(fmsb)
 
# Crear datos: nota en la escuela secundaria para varios estudiantes
set.seed(99)
data <- as.data.frame(matrix( sample( 0:20 , 15 , replace=F) , ncol=5))
colnames(data) <- c("math" , "english" , "Python" , "music" , "R-coding" )
rownames(data) <- paste("mister" , letters[1:3] , sep="-")
 
# Para usar el paquete fmsb, tengo que agregar 2 líneas al marco de datos: el máximo y el mínimo de cada variable para mostrar en el gráfico!
data <- rbind(rep(20,5) , rep(0,5) , data)
 
# Establecer colores gráficos
library(RColorBrewer)
coul <- brewer.pal(3, "BuPu")
colors_border <- coul
library(scales)
colors_in <- alpha(coul,0.3)

# Si elimina las 2 primeras líneas, la función calcula el máximo y el mínimo de cada variable con los datos disponibles:
radarchart( data[-c(1,2),]  , axistype=0 , maxmin=F,title="Gráfico de araña o de radar",
    #polígono personalizado
    pcol=colors_border , pfcol=colors_in , plwd=4 , plty=1,
    #personalizar la cuadrícula
    cglcol="grey", cglty=1, axislabcol="black", cglwd=0.8, 
    #estiquetas personalizadas
    vlcex=0.8 
    )

# Agregar una leyenda
legend(x=0.7, y=1, legend = rownames(data[-c(1,2),]), bty = "n", pch=20 , col=colors_in , text.col = "grey", cex=1.2, pt.cex=3)
```
