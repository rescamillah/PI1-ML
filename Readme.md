
# Proyecto MLOps: Sistema de Recomendación de Videojuegos para los Usuarios de la plataforma Steam

### Descripción del Proyecto
Este es el primer proyecto individual perteneciente a la fase de Labs del bootcamp "Henry", con esta labor se pretende hacer uso de parte de lo aprendido en la trayectoria del curso, en esta ocasión se desarrolla un caso de negocio real utilizando inforomación pública de la plataforma STEAM, una plataforma de videojuegos, en la cuál se le entregarán modelos de de Machine Learning y consultas importantes para su análisis.

### Objetivo
Se busca generar un modelo de Machine Learning, el cuál prinda brindar un sistema de recomendación de videojuegos, ya sean recomendaciones para un usuario en específico o, recomendaciones que lleguen a partir de un videojuego existente.

# Procedimientos Generales
Para la realización de este proyecto, para llegar al objetivo de la creación de un modelo de Machine Learning, el cuál esté disponible en una API de forma pública disponible para su consume en internet, se requieren realizar los procesos de ETL, EDA y deployment de la misma API mencionada.
<br />

## Desarrollo del proyecto <br />
Los archivos utilizados se encuentran ordenados por carpetas según su objetivo, además, cada archivo contiene el código documentado y MarkDowns que brindan mayor detalle de lo que se va a realizar en cada paso.
<br />
**1. Ingeniería de Datos (ETL)** <br />

- **1.1 *Transformaciones de Datos:*** Inicialmente, se recibieron tres archivos en formato JSON, los cuáles se encuentran en el siguiente link **[Datos Originales](https://docs.google.com/spreadsheets/d/e/2PACX-1vR459kVWPsFGSBy6Hhzibp6hRVyvzSFUA0ta_v_FcMgNQnE84Kbt9XKIWLDPlJTqg/pubhtml?gid=1246267749&single=true)**, nos encontramos con el problema que dos de estos archivos no se encontraban en el formato correcto que se estabelce para JSOn, por lo qué, se tuvo que hacer ciertos reemplazos de caracteres para convertir dichos archivos a un formato correcto y podrlos utilizar.
Hay que tomar en consideración que, cada archivo de JSON se trabajo de manera individual, por lo que existen un archivo notebook de jupyter en el que se muestra a detalle la manera en la que fue procesada la información, los pasos que se siguieron y su justificación para realizarlo, al finalizar con las transformaciones, se guarda el resultado final en un archivo de tipo csv que podemos llamar "limpió", ya que contiene el formato correcto para su análisis y listo para poder utilizarlo en dataframes de pandas. 
<br /> Los archivos se componen de la siguiente manera: 
  + [australian_user_reviews.json]: Nos brinda las reseñas a ciertos videojuegos emitidos por los usuarios de la plataforma. <br />
  + [output_steam_games.json]: Nos brinda el listado detallado de los juegos disponibles dentro de la plataforma, donde incluye descripciones y características de dichos videojuegos.<br /> 
  + [australian_users_items.json]: Nos brinda un listado detallado de los usuarios existentes en la plataforma.<br />
  
- **1.2 *Feature Engineering:*** Se crea la columna **``` sentiment_analysis ```** utilizando la librería de NLTK (Natural Language Toolkit), se aplica un análisis de sentimiento a las reseñas de los usuarios, para esto se hizo una limpieza de dicho campo, donde se eliminaron caractéres especiales para darle la misma intención a cada valor, se le da formato al resultado para obtener un valor de 0 en caso de ser una reseña negativa, valor 1 para reseñas neutrales y un valor 2 para reseñas positivas. <br />

- **1.3 *Desarrollo de API:*** Se utilizó la herramienta de FastAPI para correr nuestro sistema de manera local y posteriormente se hace un deployment utilizando Render, el resultado final es proporcionar cinco consultas con información relevante sobre la información obtenida en los archivos de datos.<br />
  + Endpoint 1 (PlayTimeGenre): Devuelve año con mas horas jugadas para un género dado.<br />
  + Endpoint 2 (UserForGenre): Devuelve el usuario que acumula más horas jugadas para el género dado y una lista de la acumulación de horas jugadas por año.<br />
  + Endpoint 3 (UsersRecommend): Devuelve el top 3 de juegos MÁS recomendados por usuarios para el año dado.<br />
  + Endpoint 4 (UsersWorstDeveloper): Devuelve el top 3 de desarrolladoras con juegos MENOS recomendados por usuarios para el año dado.<br />
  + Endpoint 5 (sentiment_analysis): Según la empresa desarrolladora, se devuelve un diccionario con el nombre de la desarrolladora como llave y una lista con la cantidad total de registros de reseñas de usuarios que se encuentren categorizados con un análisis de sentimiento como valor.<br />
Para acceder a la funcionalidad completa de este sistema y ejecutar las consultas en tiempo real, se puede realizar utilizando el siguiente link de Render **[URL de la API](https://fastapi-fown.onrender.com/docs)**. <br />
  
**2. Análisis Exploratorio de Datos (EDA)** <br />
Se realiza una investigación a detalle de los datos obtenidos, en la cuál se generan insights soportados con gráficas que permiten realizan un análisis a profundidad de la información, esto consultable en el archivo EDA.<br />

**3. Modelo de Aprendizaje Automático** <br />
Se crea un modelo de Machine Learning utilizando como base la similitud de cosenos, apoyado de un contador de vectores, el cuál se utiliza para vectorizar los textos contenidos en la columnas "specs", esta columnas nos da características inherentes al videojuego, por ende, se vuelve la base de nuestro aprendizaje. 
Ya que se ha vectorizado la información, se utiliza la similitud del coseno para medir la distancia entre dos vectores, siendo así que, entre más cercano a 1, los vectores son más similares, de este modo, es cómo podemos saber qué juego se puede recomendar basado en otro video juego o en el historial del jugador.

- **3.1 *[Sistema de Recomendación por juego]***: Se dispone de modelo que recibe cómo parámetro el ID de un videojuego dentro de la plataforma y nos retorna un listado de 5 videojuegos recomendables a partir del videojuego inicial.<br />

- **3.1 *[Sistema de Recomendación por jugador]***: Se dispone de un modelo que recibe como parámetro el ID del jugador y nos retorna un listado de 5 videojuegos recomendables para dicho usuario.<br />

**4. Implementación de MLOps** <br />
**Deploy del Modelo:** Se realiza el deploy de nuestro proyecto por modelo: **[URL de la API](https://fastapi-fown.onrender.com/docs)**. <br />

**5. Video Explicativo** <br />
Se graba un video donde se muestra el funcionamiento de la API y se explican partes sobre las consultas, funciones y modelos aplicados del código [Video](https://github.com/rescamillah/PI1-ML/blob/main/video3513975660.mp4).<br />
<br />

## Estructura del Repositorio <br />
**1. [/Notebooks](Notebooks/):** Contiene separados por carpetas los notebooks de Jupyter utilizados para la realización del EDA, ETL, Funciones y consultas.<br />

**2. Main:** Contiene los archivos de python necesarios para correr el sistema, además, se colocan los archivos de csv utilizados para cada una de las consultas propuestas en el punto 1, estos archivos brindan una mayor facilidad y eficiencia de trabajo, ya que se separan de los archivos orginales. <br />

## NOTA IMPORTANTE
Para poder realizar el proyecto, se tuvo que limitar el uso de los dataframe, de tal forma que después de limpiar la información no se trabajó con los miles o cientos de miles de registros resultantes, sino que se trabajó con solo un porcentaje de la información, esto con la intención de no sobrepasar la memoria disponible en el aplicativo de render.

Si se desea trabajar con la información completa, se puede descargar estsa información para crear una nueva versión de este proyecto y eliminar la línea de código que límita la información utilizada.

## Autor <br />
#### Jovanni Escamilla. <br />
