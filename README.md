# Project_01_Videojuegos

## Guión Análisis de Videojuegos

🧠 CONTEXTO

![Videojuegos_contexto](https://github.com/user-attachments/assets/aa743e72-dee8-4f10-a8be-1a7c4c81c737)

PixelWave Studios desea analizar el mercado de videojuegos para entender mejor qué géneros, plataformas y regiones generan mayor éxito comercial. El análisis también incluye la influencia de las reseñas en el rendimiento de ventas.

👨‍💼 SOLICITUD DEL CLIENTE
“Queremos identificar qué hace exitoso a un videojuego para enfocar mejor nuestras decisiones estratégicas de desarrollo y distribución.”

1. Analizar las tendencias de ventas por plataforma, género y región.
2. Evaluar el desempeño por región y las preferencias locales.
3. Analizar la popularidad por género según región y plataforma.
4. Observar tendencias según el año de lanzamiento.
5. Estudiar la relación entre reseñas y éxito comercial.
6. Detectar distribuidores y desarrolladores más exitosos.

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

Imagen de la distribución categórica
  ![CategoricalData](https://github.com/user-attachments/assets/4e9562b7-22b6-4210-b1e2-ef12ff21f5c6)

Imagen de la distribución numérica </summary>
  ![Numerical Data](https://github.com/user-attachments/assets/a2af12c2-4e1d-4745-be07-113207f875b8)




## Dia 2 (25/03/2025)
- Data cleaning.

Continuando con el proceso de data cleaning, se hace una búsqueda de mayúsculas y minúsculas. Se investiga qué significa el valor tbd en la columna User_Score.

Como parte del proceso de normalización, en JP_Sales se cambió un registro con un valor categórico llamado "Excel". Nos dimos cuenta de que, realizando una resta de los valores de otras columnas relacionadas podíamos llegar encontrar el valor de ese registro, siendo ese valor consistente.

En la columna Developer encontramos un registro con un valor numérico llamado "2015". Al realizar una busqueda concluimos que no existe ningún desarrollador con ese nombre, por lo que lo borramos.

Se borran dos registros porque no aparecían nombre ni género. Nos planteamos realizar una busqueda para intentar averiguar esa información a partir de la información de las restantes celdas, pero nos dimos cuenta de que era materialmente imposible encontrar esa información con los datos disponibles. 

Normalizar la columna Critic_Score en base a la columna User_Score y añadir decimales en ambas.

Se cambia el formato de las columnas Sales para que los ceros se muestren con decimales.

Se identificó que muchos videojuegos tienen múltiples desarrolladores en una misma celda, lo cual complica la normalización de datos. Para solucionarlo, se dividieron esos registros en columnas separadas, se estandarizaron ciertos sufijos como “,Inc” y se contó la frecuencia de cada desarrollador. Luego, se creó una tabla con los desarrolladores únicos y su frecuencia, y se añadieron columnas al dataset original para reflejar cuántas veces aparece cada uno. Finalmente, se usó una fórmula con MAX, MATCH y CHOOSE para determinar y mostrar al desarrollador más frecuente en cada registro.

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
- Visualización looker studio

Representación de los distintos apartados en looker studio. 

Se unificaron los 2 primeros puntos ya que se basan en lo mismo.

1. Analizar las tendencias de ventas por plataforma, género y región.
2. Evaluar el desempeño por región y las preferencias locales.

Dashboard puntos 1 y 2

![Apartado_01](https://github.com/user-attachments/assets/012b75de-49ea-4a5d-8be1-aae256742f70)

Para el segundo apartado se comparó las ventas globales con la las Score de los usuarios y se observó una tendencia clara.

![Predictor](https://github.com/user-attachments/assets/54392682-14b0-4f9a-bb7c-86da7360d453)


## Dia 5 (28/03/2025)
- 

## Dia 6 (31/03/2025)
- 

## Dia 7 (01/04/2025)
- 
