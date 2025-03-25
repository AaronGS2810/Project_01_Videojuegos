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

## Dia 2 (25/03/2025)
- Data cleaning.

Continuando con el proceso de data cleaning, se hace una búsqueda de mayúsculas y minúsculas. Se investiga qué significa el valor tbd en la columna User_Score.

Como parte del proceso de normalización, en JP_Sales se cambió un registro con un valor categórico llamado "Excel". Nos dimos cuenta de que, realizando una resta de los valores de otras columnas relacionadas podíamos llegar encontrar el valor de ese registro, siendo ese valor consistente.

En la columna Developer encontramos un registro con un valor numérico llamado "2015". Al realizar una busqueda concluimos que no existe ningún desarrollador con ese nombre, por lo que lo borremos.

Se borran dos registros porque no aparecían nombre ni género. Nos planteamos realizar una busqueda para intentar averiguar esa información a partir de la información de las restantes celdas, pero nos dimos cuenta de que era materialmente imposible encontrar esa información con los datos disponibles. 

Normalizar la columna Critic_Score en base a la columna User_Score y añadir decimales en ambas.

Se cambia el formato de las columnas Sales para que los ceros se muestren con decimales.

Encontramos que en la columna Developer hay más de 500 registros en donde aparecen varios desarroladores para un mismo videojuego. Esto presenta un problema a la hora de normalizar, ya que el cliente especifica que quiere detectar a los desarrolladores más exitosos. Es por esto que el procedimiento que se ha usado para normalizar esta columna ha consistido en dividir en diferentes columnas esos registros que contienen varios desarrolladores en una misma celda con un proceso automatizado, realizar un conteo de los valores resultantes del paso anterior que esten repetidos, y buscar cuáles son los que más se repiten, lo que equivale a encontrar cuáles son los desarrolladores que más se repiten.. En esa misma columna que sustituimos los valores que terminan en ",Inc", ",Ltd" y "S,r,I" por "Inc", "Ltd" y "SrI"; para poder separar correctamente los valores en los que hay varios desarolladores que han participado en un mismo juego. El cambio no se automatizó porque eran pocos registros.

Para normalizar las celdas con valores categóricos por mayúsculas y minúsculas se ha seguido el criterio de normalizar únicamente las palabras que empiecen por minúscula, automatizando la tarea con una fómula, y sustituir esa primera leta minúscula por una mayúscula.

Incluir los gráficos en el día 1 del README.

## Dia 3 (26/03/2025)
- 

## Dia 4 (27/03/2025)
- 

## Dia 5 (28/03/2025)
- 

## Dia 6 (31/03/2025)
- 

## Dia 7 (01/04/2025)
- 
