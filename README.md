# Project_01_Videojuegos

Link base de datos: https://docs.google.com/spreadsheets/d/1pUjyNvfE7EArTESvpm94vk1OVitPBWFRTBVT4wWa8AA/edit?usp=sharing

Link documento Word: https://docs.google.com/document/d/1oOG8yiG67QXCRPf4jFNlem2M2DgLApcRz7QepoSA9sQ/edit?usp=sharing


## Dia 1 (24/03/2025)
- Crear proyecto (Ruta de proyecto)

- Data Profiling.

El archivo que contiene los datos en bruto es un documento CSV (valores separados por comas) llamado "Video_games.csv". Su importación a Google Sheets se realizó sin inconvenientes.

  Al examinar el documento, observamos que incluye las siguientes columnas: Nombre del videojuego (Name). Plataforma (Platform). Año de lanzamiento (Year_of_Release). Género (Genre). Distribuidor (Publisher). Ventas en América del Norte (NA_Sales). Ventas en Europa (EU_Sales). Ventas en Japón (JP_Sales). Ventas en otras regiones (Other_Sales). Ventas globales (Global_Sales). Puntuación de los críticos (Critic_Score). Cantidad de críticas profesionales (Critic_Count). Puntuación de los usuarios (User_Score). Cantidad de críticas de usuarios (User_Count). Desarrollador (Developer). Clasificación ESRB (Rating).

Para comprender mejor algunos datos, realizamos un breve análisis. Consultamos a ChatGPT para esclarecer el significado de las columnas NA_Sales, Critic_Count y User_Count.
En el caso de Other_Sales, dimos por hecho que representaba las ventas en regiones fuera de América del Norte, Europa y Japón. Para comprobarlo, restamos el valor de NA_Sales, EU_Sales y JP_Sales a Global_Sales, obteniendo como resultado el valor de Other_Sales, lo que confirmó nuestra hipótesis.
Finalmente, para la columna Rating, también realizamos una consulta a ChatGPT y determinamos que representa la clasificación ESRB (Entertainment Software Rating Board).

- Data cleaning.

Hemos añadido una columna id. También hemos realizado una identificación de los duplicados, no encontrando ninguno. Para hacer un ánalisis exploratorio del datasheet dividimos entre variables categóricas y variables numéricas. Se comprueba que los valores de la columna rating correspondan con las categorías del ESRB.

<details>
  <summary>📸 Haz clic para ver la imagen de la distribución categórica </summary>
  ![CategoricalData](https://github.com/user-attachments/assets/4e9562b7-22b6-4210-b1e2-ef12ff21f5c6)

</details>

<details>
  <summary>📸 Haz clic para ver la imagen de la distribución numérica </summary>
  ![Numerical Data](https://github.com/user-attachments/assets/a2af12c2-4e1d-4745-be07-113207f875b8)

</details>



## Dia 2 (25/03/2025)
- Data cleaning.

Continuando con el proceso de data cleaning, se hace una búsqueda de mayúsculas y minúsculas. Se investiga qué significa el valor tbd en la columna User_Score.

Como parte del proceso de normalización, en JP_Sales se cambió un registro con un valor categórico llamado "Excel". Nos dimos cuenta de que, realizando una resta de los valores de otras columnas relacionadas podíamos llegar encontrar el valor de ese registro, siendo ese valor consistente.

En la columna Developer encontramos un registro con un valor numérico llamado "2015". Al realizar una busqueda concluimos que no existe ningún desarrollador con ese nombre, por lo que lo borramos.

Se borran dos registros porque no aparecían nombre ni género. Nos planteamos realizar una busqueda para intentar averiguar esa información a partir de la información de las restantes celdas, pero nos dimos cuenta de que era materialmente imposible encontrar esa información con los datos disponibles. 

Normalizar la columna Critic_Score en base a la columna User_Score y añadir decimales en ambas.

Se cambia el formato de las columnas Sales para que los ceros se muestren con decimales.

Encontramos que en la columna Developer hay más de 500 registros en donde aparecen varios desarroladores para un mismo videojuego. Esto presenta un problema a la hora de normalizar, ya que el cliente especifica que quiere detectar a los desarrolladores más exitosos. Es por esto que el procedimiento que se ha usado para normalizar esta columna ha consistido en dividir en diferentes columnas esos registros que contienen varios desarrolladores en una misma celda con un proceso automatizado, realizar un conteo de los valores resultantes del paso anterior que esten repetidos, y buscar cuáles son los que más se repiten, lo que equivale a encontrar cuáles son los desarrolladores que más se repiten.. En esa misma columna que sustituimos los valores que terminan en ",Inc", ",Ltd" y "S,r,I" por "Inc", "Ltd" y "SrI"; para poder separar correctamente los valores en los que hay varios desarolladores que han participado en un mismo juego. El cambio no se automatizó porque eran pocos registros.

Con el objetivo de identificar al desarrollador más destacado, como se mencionó previamente, se procedió a dividir el contenido de la celda utilizando la función TRIM(INDEX(SPLIT)). Asimismo, se empleó la función IF.ERROR para manejar los casos en los que la celda se encuentra vacía.

Posteriormente, en una hoja diferente, se elaboró una tabla que contiene los valores únicos de los desarrolladores y la frecuencia con la que cada uno aparece en el conjunto de datos. Una vez completada esta tabla, se regresó al dataset original, donde se crearon cuatro columnas adicionales (dado que, como máximo, se registran cuatro desarrolladores por celda). Estas columnas relacionan a cada desarrollador con la cantidad de veces que aparece, de acuerdo con la tabla de valores únicos, reflejando dicho número en la celda correspondiente.

A continuación, se añadió una nueva columna en la que se aplicó la siguiente fórmula:

=IF.ERROR(CHOOSE(MATCH(MAX(V2:Y2);V2:Y2;0);Q2;R2;S2;T2);"")

. Se calcula el valor máximo (MAX) entre las cuatro columnas correspondientes a los desarrolladores.
. Mediante MATCH, se determina la posición (entre cuatro posibles) del valor máximo obtenido.
. Con CHOOSE, se selecciona el nombre del desarrollador correspondiente a dicha posición entre los previamente separados mediante SPLIT.
. Finalmente, se utiliza IF.ERROR para que, en caso de que la celda esté vacía o se genere un error, la celda permanezca vacía.

Para normalizar las celdas con valores categóricos por mayúsculas y minúsculas se ha seguido el criterio de normalizar únicamente las palabras que empiecen por minúscula, automatizando la tarea con una fórmula, y sustituir esa primera letra minúscula por una mayúscula.

Se observó que la columna Rating tiene clasificaciones obsoletas (K-A y EC). Estas clasificaciones las hemos transformado a las utilizadas en la actualidad, que en este caso para ambas al cambio se convierten en "E".

En cuanto a los missing values, las variables con las que hemos tratado esta condición, son la de Year (0.3 %)  y Publisher (1.6%). Para este caso, y debido a su insignificancia, hemos decidido eliminarlos. 

Incluir los gráficos en el día 1 del README.

## Dia 3 (26/03/2025)
- Data cleaning

Una vez finalizado el primer conjunto de datos, se procedió a la conceptualización del segundo dataset. Este nuevo conjunto se basa en el primero, aunque presenta un sesgo derivado de la cantidad de valores faltantes (missing values) en determinadas categorías. Las variables de mayor relevancia en este contexto son: "Developers", "Critic_Score" y "User_Score".

Para abordar esta situación, se eliminarán de manera individual los valores nulos de cada una de estas categorías, y se evaluará el impacto de dicha eliminación sobre las otras dos variables. A partir de este análisis, se determinará cuál de los tres posibles subconjuntos de datos resultantes es el más adecuado para continuar con el trabajo.

En un análisis preliminar, se consideró eliminar los valores nulos correspondientes a la variable categórica "Developer", dado que presenta una menor proporción de datos faltantes. Posteriormente, en función del número de valores nulos presentes en las otras dos variables ("Critic_Score" y "User_Score"), se evaluará la posibilidad de imputarlos utilizando medidas estadísticas como la media o la mediana, o bien mediante la aplicación de algún modelo predictivo.

## Dia 4 (27/03/2025)
- 

## Dia 5 (28/03/2025)
- 

## Dia 6 (31/03/2025)
- 

## Dia 7 (01/04/2025)
- 
