---
title: "Actividad: PRA2: Limpieza y análisis de datos"
author: "Reison A. Torres Urina"
date: "Diciembre 2019"
header-includes:
  - \usepackage[spanish]{babel}
output: 
  pdf_document:
    number_sections: yes
    highlight: zenburn
    toc: yes
    toc_depth: 2
  html_document:
    includes:
      in_header: PRA2-header.html
    number_sections: yes
    theme: cosmo
    toc: yes
    toc_depth: 2
  word_document: default
    
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

# Detalles de la actividad  

## Descripción  

En esta practica se elabora un caso práctico orientado a aprender a identificar los datos relevantes para un proyecto analítico y usar las herramientas de integración, limpieza, validación y análisis de las mismas.  

## Objetivos

Los objetivos concretos de esta práctica son:  

* Aprender a aplicar los conocimientos adquiridos y su capacidad de resolución de
problemas en entornos nuevos o poco conocidos dentro de contextos más amplios o
multidisciplinares.  

* Saber identificar los datos relevantes y los tratamientos necesarios (integración, limpieza
y validación) para llevar a cabo un proyecto analítico.  

* Aprender a analizar los datos adecuadamente para abordar la información contenida en
los datos.  

* Identificar la mejor representación de los resultados para aportar conclusiones sobre el
problema planteado en el proceso analítico.  

* Actuar con los principios éticos y legales relacionados con la manipulación de datos en función del ámbito de aplicación.  

* Desarrollar las habilidades de aprendizaje que les permitan continuar estudiando de un modo que tendrá que ser en gran medida autodirigido o autónomo.  

* Desarrollar la capacidad de búsqueda, gestión y uso de información y recursos en el ámbito de la ciencia de datos.

## Competencias

En esta práctica se desarrollan las siguientes competencias del Máster de Data Science:  

* Capacidad de analizar un problema en el nivel de abstracción adecuado a cada situación
y aplicar las habilidades y conocimientos adquiridos para abordarlo y resolverlo.  

* Capacidad para aplicar las técnicas específicas de tratamiento de datos (integración,
transformación, limpieza y validación) para su posterior análisis.  

# Solución

## Descripción del dataset  

### Descripción

Los datos seleccionados, fueron obtenidos del sitio de data science, [__www.Kaggle.com__](https://www.kaggle.com), en el encontramos una variedad de dataset Open Data. El conjunto de datos seleccionados para desarrollar esta actividad es [__Titanic: Machine Learning from Disaster__](https://www.kaggle.com/c/titanic), en este dataset encontramos, los datos de los pasajeros, que abordaron el Titanic en su viaje inaugural.

Los datos de este dataset se encuentran divididos en dos archivos train.csv con 891 observaciones y test.cvs con 418 observaciones. El conjunto de datos esta descripto por un conjunto de 12 variables. Las característica presenten en este dataset, nos permitirá cumplir los objetivos propuestos en esta actividad. 

A continuación describimos el conjunto de variables que conforman este dataset:  

* __PassengerId:__ Número consecutivo que identifica al pasajero.    
* __pclass:__ Nivel socioeconómico del pasajero (1st = Upper, 2nd = Middle, 3rd = Lower).  
* __age:__ Edad del pasajero en años.  
* __sibsp:__ Familiar abordo del Titanic. Define la relación familiar de la siguiente forma:  
 : Hermanos => 1 = hermana, 2 = hermano, 3 = hermanastro, 4 = hermanastra  
 : Esposos => 5 = esposo, 6 = esposa, 7 = amantes y 8 = novio  
* __parch:__ Familiar abordo del Titanic. Define la relación familiar de la siguiente forma:  
 : Padres => 1 = madre, 2 = padre  
 : Hijos => 3 = hija, 4 = hijo, 5 = hijastra, 6 = hijastro  
* __ticket:__ Número del boleto de abordaje.  
* __fare:__ Precio del boleto.  
* __cabin:__ Número de la cabina.  
* __embarked:__ Puerto de embarque (C = Cherbourg, Q = Queenstown, S = Southampton).  
* __survival:__ Pasajero superviviente (0 = No, 1 = Yes)


### Importancia y objetivos de los análisis


A partir de este conjunto de datos se plantea la problemática de determinar qué variables influyen más en la supervivencia de un pasajero en el naufragio del Titanic. Además, se podrá proceder a crear modelos de regresión  que permitan predecir si un pasajero sobrevive o no en función de sus características y contrastes de hipótesis que ayuden a identificar propiedades interesantes en las muestras que puedan ser inferidas con respecto a la población.  

Este tipo de análisis pueden ser utilizados por las aseguradoras del sector turístico, para determinar el riesgo que puede tener un turista al viajar en los trasatlánticos. Y asi poder ofreser las cobertura del seguro.

## Integración y selección de los datos de interés a analizar
```{r echo=TRUE, message=FALSE, warning=FALSE}
  # cargamos paquetes R que vamos a utilizar
  library(ggplot2)
  library(ggpubr)
  library(dplyr)
  library(Hmisc)
  library(corrplot)

if(!require(ggplot2)){
    install.packages('ggplot2', repos='http://cran.us.r-project.org')
    library(ggplot2)
}
```
### Integración

En esta practica unificaremos los datos contenido en el dataset train.csv y test.cvs. Para el dataset train.csv agregaremos la variable __survival__ extrayendo su valor del dataset gender_submission.csv.

```{r echo=TRUE, message=FALSE, warning=FALSE}
black_friday.data<-read.csv("/home/datamining/Documents/PRAC1/Datos/BlackFriday.csv",stringsAsFactors = FALSE, header=T, sep=",")

# calculamos el numero de registros cargados en el dataset
filas=dim(black_friday.data)[1]
```



### Selección de los datos

La gran mayoría de las variables contenidas en el conjunto de datos corresponde con características de los pasajeros que abordaron el Titanic, por lo que serán tenidas en cuenta para realizar nuestro análisis. Sin embargo, podremos prescindir de la variable __PassengerId__ dado que este atributo no aporta una descripción al pasajero, y no influye en la resolución de nuestro problema.

## Limpieza de los datos

### ¿Los datos contienen ceros o elementos vacíos?
### ¿Cómo gestionarías cada uno de estos casos?

### Identificación y tratamiento de valores extremos

## Inspiración

El presente conjunto de datos podría utilizarse en el ámbito comercial, donde se podría elaborar modelos predictivos, que nos ayuden a predecir el precio del producto en el futuro, y con esto poder preparar estrategias de markiting.

También podría ser de gran utilidad en el campo de la *Agricultura*, para informar al pequeño productor de las temporadas de mayor de manda de sus productos en el mercado nacional, para que puedan preparar sus cosechas para suplir esta demanda.

## Licencia

Para la publicación de este conjunto de datos se seleccionó la licencia **CC BY-SA 4.0 License**. Los motivos por los cual se selecciono esta licencia son:

* _Los trabajos derivadas del conjunto de datos generado, su distribución se debe hacer con una licencia igual a la que regula el trabajo original_. Con esto garantizamos que los trabajos derivados del trabajo original, seguirán distribuyéndose bajo los mismo términos que el autor original planteo.

* _Se debe dar crédito de manera adecuada al creador del conjunto de datos generado, e indicar si se han realizado cambios_. De esta manera damos crédito del trabajo del autor original, y mantenemos una transparencia en la medida que se indican las aportaciones/cambios realizados al trabajo original.

* _Explotación de los datos generados, incluyendo una finalidad comercial_. Con esto garantizamos que la utilización de los datos generados, no serán de uso privativo, dando la posibilidad que otras empresas utilicen los datos generados y realicen trabajos de calidad que mantenga su competitividad en el mercado.


## Código fuente y dataset

* En la siguiente ruta (**[src/foodPriceCorabasto.py](https://github.com/reison-torres/webscraping/blob/master/src/foodPriceCorabastos.py)**) encontraras el código Python desarrollado. 
* En la siguiente ruta(**[src/foodPriceCorabasto.ipynb](https://github.com/reison-torres/webscraping/blob/master/src/foodPriceCorabastos.ipynb)**) encontraras el código Python desarrollado en formato Jupyter Notebook.
* En la siguiente ruta(**[data/](https://github.com/reison-torres/webscraping/tree/master/data)**) encontraras los dataset generados en formato CSV.

  
# Recursos

1. Subirats, L., Calvo, M. (2018). Web Scraping. Editorial UOC.  
2. Creative Commons. (2016). "Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)". Creative Commons public licenses [artículo en línea]. [Fecha de consulta: 22 de octubre del 2019]. <https://creativecommons.org/licenses/by-sa/4.0/legalcode>.  
3. Lawson, R. (2015). Web Scraping with Python. Packt Publishing Ltd.  
4. Masip, D. El lenguaje Python. Editorial UOC.  
5. Willems, Karlijn. (19 Marzo 2019). "Python Numpy Array Tutorial". DataCamp [artículo en línea]. [Fecha de consulta: 26 de octubre del 2019]. <https://www.datacamp.com/community/tutorials/python-numpy-tutorial#make>.  
6. Willems, Karlijn. (17 Enero 2019). "Pandas Tutorial: DataFrames in Python". DataCamp [artículo en línea]. [Fecha de consulta: 27 de octubre del 2019].  <https://www.datacamp.com/community/tutorials/pandas-tutorial-dataframe-python#question3>.  
