<h1 align="center">Entrega Final : "Reseña de vinos"</h1>
<hr>
<img src="https://raw.githubusercontent.com/Mauritas99/Proyect_images/refs/heads/main/Vinoteca.png">
<h2>Descripción general del proyecto.</h2>
<p>El siguiente trabajo tiene como finalidad aplicar todos los conocimientos y herramientas adquiridas durante el cursado de la diplomatura en Data Science en Comunidad ICARO.</p>
<p>Teniendo en cuenta esto, se parte de un dataset disponible en Kaggle [ <a href="https://www.kaggle.com/datasets/zynicide/wine-reviews">"wine-reviews"</a> ], el cual esta compuesto por 130k reseñas de sommeliers a vinos de todo el mundo, donde ademas encontramos caracteristicas de los mismos (lugar de procedencia, variedad de uva, bodega, entre otros).</p>
<p>El siguiente proyecto esta dividido en 4 secciones, que abarcan desde la <em><b>limpieza del dataset</b></em>, como su posterior analisis, principales <em><b>insights</b></em></em> y elaboración de modelos predictivos de <em><b>machine learning</b></em>.</p>
<p color=red><b>IMPORTANTE: Para utilizar los notebooks y correr los scripts, se recomienda clonar el repositorio, para que las rutas relativas puedan acceder a las versiones del dataset.</b></p>
<p>Tecnologias empleadas:</p>
<p>
<img src="https://raw.githubusercontent.com/Mauritas99/Proyect_images/refs/heads/main/Buttons_github/Python.png" height=40px>
<img src="https://raw.githubusercontent.com/Mauritas99/Proyect_images/refs/heads/main/Buttons_github/Jupyter.png" height=40px>
<img src="https://raw.githubusercontent.com/Mauritas99/Proyect_images/refs/heads/main/Buttons_github/HTML.png" height=40px>
<img src="https://raw.githubusercontent.com/Mauritas99/Proyect_images/refs/heads/main/Buttons_github/Numpy.png" height=40px>
<img src="https://raw.githubusercontent.com/Mauritas99/Proyect_images/refs/heads/main/Buttons_github/Pandas.png" height=40px>
<img src="https://raw.githubusercontent.com/Mauritas99/Proyect_images/refs/heads/main/Buttons_github/Matplotlib.png" height=40px>
<img src="https://raw.githubusercontent.com/Mauritas99/Proyect_images/refs/heads/main/Buttons_github/Seaborn.png" height=40px>
<img src="https://raw.githubusercontent.com/Mauritas99/Proyect_images/refs/heads/main/Buttons_github/Scikit_learn.png" height=40px>
</p>
<p><b>Para instalar los módulos y dependencias, dirigete a la carpeta del proyecto y ejecuta el siguiente comando bash:</b></p>
<li><em>pip install -r requirements.txt</em></li>


<h2><u>Glosario</u></h2>
<ol>
  <li><a href="https://github.com/Mauritas99/Proyecto-Final/blob/main/2_Notebooks/1_ETL_EDA.ipynb">ETL-EDA.</a></li>
    <ul>
      <li>Inspección del dataset.</li>
      <li>Visualizaciones de interés.</li>
      <li>Transformación e imputacion de datos.</li>
    </ul>
  <li><a href="https://github.com/Mauritas99/Proyecto-Final/blob/main/2_Notebooks/2_Analisis_precio.ipynb">Sistema de analisis de precios.</a></li>
  <ul>
      <li>Ratio price/points.</li>
      <li>Visualización del ratio segun grupos de interés.</li>
      <li>Implementación y evaluación de modelo de predicción de precio.</li>
    </ul>
  <li><a href="https://github.com/Mauritas99/Proyecto-Final/blob/main/2_Notebooks/3_NLP.ipynb">NLP.</a></li>
  <ul>
      <li>Analizar reseñas.</li>
      <li>Preprocesamiento de texto.</li>
      <li>Modelo de analisis de sentimientos en reseñas.</li>
    </ul>
  <li><a href="https://github.com/Mauritas99/Proyecto-Final/blob/main/2_Notebooks/4_Sistema_recomendacion.ipynb">Sistemas de recomendación de vinos.</a></li>
  <ul>
      <li>Preparación el dataset.</li>
      <li>Elaboración de sistema de recomendación mixto con LightFM.</li>
      <li>Funciones de recomendación de vinos.</li>
    </ul>
</ol>
<hr>
<h3>ETL - EDA 🔍</h3>
  <h6>Inspección del dataset.</h6>
  <p>Los primeros valores que arrojo la inspección del dataset mostraron una cantidad considerable de valores nulos, ningun valor duplicado y un valor aproximado de 130k filas y 14 columnas.</p>
  <img src="https://raw.githubusercontent.com/Mauritas99/Proyect_images/refs/heads/main/Imagenes%20para%20github/Resumen_etl.PNG" height=120px>
  <h6>Visualizaciones de interés.</h6>
  <p>Se empleo histogramas, boxplot y matriz de correlacion para las variables numéricas y gráficos de frecuencia con barras para las variables categóricas (solo aquellas que no tenian una cantidad elevada de categorías posibles por columna).</p>
  <img src="https://raw.githubusercontent.com/Mauritas99/Proyect_images/refs/heads/main/Imagenes%20para%20github/Visualizacion_1.PNG" height=500px>
  <img src="https://raw.githubusercontent.com/Mauritas99/Proyect_images/refs/heads/main/Imagenes%20para%20github/Visualizacion_2.PNG" height=500px>
  <img src="https://raw.githubusercontent.com/Mauritas99/Proyect_images/refs/heads/main/Imagenes%20para%20github/Visualizacion_3.PNG" height=450px>
  <img src="https://raw.githubusercontent.com/Mauritas99/Proyect_images/refs/heads/main/Imagenes%20para%20github/Resumen_eda.PNG" height=130px>
  <h6>Transformación e imputacion de datos.</h6>
  <p>Al eliminar columnas fuera de interes (específicamente "Unnamed: 0"), se encontraron 9k filas duplicadas (enmascaradas por el indice desfasado de la columna, que las "distinguía" para el metodo .duplicated()). Se retiraron del dataset.</p>
  <p>Si bien los precios de los vinos son unicos, al ser una cantidad menor al 10% valores nulos, se decidió imputar con la media de precios.</p>
  <p>Las variables categóricas poseen una cantidad importante de outliers, por lo que se decide reemplazar por cadenas "Sin dato", para manipularlos de manera adecuada, dependiendo de los modelos mas adelante.</p>
  <p>Se categorizó la variable precio a 4 posibles categorias, según el valor del vino.</p>
  <p>Se exportó la base de datos como "df_wines_limpio.csv", para su posterior uso.</p>
  <hr>
<h3>Sistema de analisis de precios 💰</h3>
  <h6>Ratio price/points.</h6>
  <p>Teniendo en cuenta la <a href="https://wain.cr/collections/wine-enthusiast-we#:~:text=Las%20calificaciones%20de%20Wine%20Enthusiast,evaluar%20la%20calidad%20del%20vino.&text=Un%20muy%20buen%20vino%20con%20fuertes%20cualidades.&text=Un%20buen%20vino%20que%20merece%20la%20pena%20disfrutar.">escala de Wine Enthusiast</a>, y por cuestiones de facilidad en la interpretación de datos, se generó la variable "price/point_ratio", que señala el "precio" que posee cada punto que obtiene un vino (aquellos vinos con un ratio menor a 0, son considerados "gangas", al ser baratos para la cantidad de puntos que obtiene). Para ello, se estandarizaron los valores de "price" y "points".</p>
   <img src="https://raw.githubusercontent.com/Mauritas99/Proyect_images/refs/heads/main/Imagenes%20para%20github/Price_points_ratio.PNG" height=130px>
  <h6>Visualización del ratio segun grupos de interés.</h6>
  <img src="https://raw.githubusercontent.com/Mauritas99/Proyect_images/refs/heads/main/Imagenes%20para%20github/Frecuencias_ratio.PNG" height=500px>
  <img src="https://raw.githubusercontent.com/Mauritas99/Proyect_images/refs/heads/main/Imagenes%20para%20github/Resumen_ratio.PNG" height= 150px>
  <h6>Implementación y evaluación de modelo de predicción de precio.</h6>
  <p>Se entrenó un modelo de regresión "Random Forest", para predecir el precio en base a determinadas columnas del dataset (se agregaron a X aquellas columnas que mostraban correlación con la variable objetivo).</p>
  <p>Se definió un Pipeline donde se establecia el preprocesamiento de variables categoricas y numéricas y el modelo a emplear.</p>
  <p>La evaluación finalmente arrojo valores positivos para las diferentes métricas:</p>
  <p>
    <img src="https://raw.githubusercontent.com/Mauritas99/Proyect_images/refs/heads/main/Imagenes%20para%20github/Pipeline_forest.PNG" height=200px>
  <img src="https://github.com/Mauritas99/Proyect_images/blob/main/Imagenes%20para%20github/Metricas_png.PNG" height=100px>
  </p>
<hr>
<h3>NLP 🔠</h3>
  <h6>Preprocesamiento de texto.</h6>
  <p>Se aplicó un muestreo estratificado por variable "country", debido a la incapacidad de procesar la totalidad de reseñas por el costo computacional que conlleva (rescatando una muestra de 19k reseñas).</p>
  <p>Las reseñas de la muestra fueron preprocesadas (eliminación de stopwords, lemmatizacion y stemming) empleando las librerias Spacy, y NLTK.</p>
  <h6>Analizar reseñas.</h6>
  <p>Se obtuvo la frecuncia de las palabras mas recurrentes de aquellas reseñas con alto y bajo puntaje, para indagar en posibles diferencias en las reseñas de ambos estratos, empleando wordclouds para su visualización, pero sin encontrar diferencias notables.</p>
  <h6>Modelo de analisis de sentimientos en reseñas.</h6>
  <p>Finalmente, se elaboró un modelo de regresión logística, que pueda clasificar la polaridad de una reseña, como positiva o negativa. Para ello, se creo la columna de polaridad empleando TextBlob para clasificar cada reseña y entrenar al modelo.</p>
  <p>Las métricas de evaluación arrojaron valores positivos para las predicciónes brindadas:</p>
  <img src="https://github.com/Mauritas99/Proyect_images/blob/main/Imagenes%20para%20github/Metricas_nlp.PNG" height=100px>
  <hr>
<h3>Sistemas de recomendación de vinos 🍷</h3>
  <h6>Preparación el dataset.</h6>
  <p>Para entrenar el modelo de recomendación, es necesario retirar la mayor cantidad de valores nulos, por lo que se decidio reducir el numero máximo de elementos nulos por fila (2 máximos), recordando que luego aquellos nulos se reemplazan con cadenas "Sin dato" (se le redujo 20k filas al conjunto de datos original).</p>
  <p>Empleando la información que contiene el dataset, se elaboro un dataframe de puntuaciones de usuarios, para posteriormente, elaborar una matriz de interacciones (df_tasters). Para ello se generaron los identificadores unicos por cada vino ("wine_id") y por cada sommelier "taster_id".</p>
  <p>A su vez, se codificaron las variables categóricas que, debido a su alta cardinalidad por su contenido de categorias unicas, implicó utilizar TargetEncoder, empleando como el promedio de referencia la columna "points". Para recuperar la categoria perteneciente a la variable categórica, se elaboró un mapa que contenia el valor original y su valor codificado.</p>
  <h6>Elaboración de sistema de recomendación mixto con LightFM.</h6>
  <p>Para elaborar la matriz de interacciones, se empleo coo_matrix y csr_matrix de Scipy, utilizando el dataset de interacciones.</p>
  <p>Para elaborar la matriz de caracteristicas, se retiro del dataset las columnas <b>["price","points","taster_id","title" ]</b>. A su vez de creó un diccionario, para obtener el titulo del vino recomendado por su "wine_id"</p>
  <p>Se entrenó un modelo de recomendación híbrido lightFM con las matrices seleccionadas, con los siguientes hiperparametros:</p>
  <ul>
    <li>Loss='warp' : Funcion de perdida que optimiza el modelo para mejorar las recomendaciones de artículos entre los primeros resultados.</li>
    <li>No_components=33 : Cantidad de componentes o características ocultas que el modelo empleará para represeentar interacciones entre artículos y usuarios.</li>
    <li>Learning_rate=0.05 : Intensidad de la tasa de aprendizaje durante cada iteración (los cambios por ciclo no son tan "bruscos").</li>
    <li>Random_state=42 : Asegura la reproductividad de la semilla y los resultados (empleando los mismos conjuntos de datos y configuraciones).</li>
  </ul>
<p>Al evaluar la <b>precisión de k</b> (k=10), se obtuvo un valor de 0.87, lo que se traduce en que el <b>87%</b> de las recomendaciones brindadas al usuario son relevantes.</p>
  <h6>Funciones de recomendación de vinos.</h6>
  <p>Dentro de las funciones de recomendación generadas apartir del modelo, encontramos recomendacion de vinos por <b>pais de procedencia</b>, <b>sommelier de preferencia</b> y <b>variedad de uva</b> (adaptable a funciones de recomendación como por ejemplo vineria o categoria de precio).</p>
  <hr>
  <h3>Conclusiones</h3>
  <p>La finalidad del trabajo fue implementar la totalidad de conceptos y tecnologías aplicadas durante el cursado, encontrando desdde lo mas básico como <b>examinar - transformar</b> un dataset, implementar y justificar la toma de decisiones de dichas transformaciones, pasando por trabajar el procesamiento de texto y obtención de insights, como finalmente, crear y evaluar modelos de aprendizaje automático, capaces de predecir un precio según las caracteristicas de un artículo, la polaridadd de una reseña según las palabras que lo componen y la recomendación de elementos según sus características y preferencias de los usuarios.</p>
