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
  <li><a href="https://github.com/Mauritas99/Proyecto-Final/blob/main/2_Notebooks/4_Sistema_recomendacion.ipynb">Sistemas de recomendación.</a></li>
  <ul>
      <li>Preparación el dataset.</li>
      <li>Elaboración de sistema de recomendación mixto con LightFM.</li>
      <li>Funciones de recomendación de vinos.</li>
    </ul>
</ol>
<hr>
<h3>ETL - EDA.</h3>
  <h6>Inspección del dataset.</h6>
  <p>Los primeros valores que arrojo la inspección del dataset arrojo una cantidad considerable de valores nulos, 0 valores duplicados (sesgados por una columna, que mas tarde se retomará) y un dataset de 130k filas y 14 columnas.</p>
  <img src="#">
  <h6>Visualizaciones de interés.</h6>
  <p>Se empleo histogramas, boxplot y matriz de correlacion para las variables numéricas y gráficos de frecuencia con barras para las variables categóricas (solo aquellas que no tenian una cantidad elevada de posibles categorías por columna).</p>
  <img src="#">
  <img src="#">
  <img src="#">
  <img src="#">
  <h6>Transformación e imputacion de datos.</h6>
  <p>Al eliminar columnas fuera de interes (especificamente "Unnamed: 0"), se encontraron 9k filas duplicadas (enmascaradas por el indice desfasado de la columna, que las volvia diferente para la función). Se retiraron del dataset.</p>
  <p>Si bien los precios de los vinos son unicos, al ser una cantidad menor al 10% valores nulos, se decidió imputar con la media de precios.</p>
  <p>En contraparte, las variables categóricas poseen una cantidad importante de outliers, por lo que se decide reemplazar por strings "Sin dato", para manipularlos de manera adecuada, dependiendo del modelo a futuro.</p>
  <p>Se categorizó la variable precio a 4 posibles categorias, según el valor del vino.</p>
  <p>Se exportó la base de datos como "df_wines_limpio.csv", para su posterior uso.</p>
  <hr>
<h3>Sistema de analisis de precios.</h3>
  <h6>Ratio price/points.</h6>
  <p>Teniendo en cuenta la <a href="https://wain.cr/collections/wine-enthusiast-we#:~:text=Las%20calificaciones%20de%20Wine%20Enthusiast,evaluar%20la%20calidad%20del%20vino.&text=Un%20muy%20buen%20vino%20con%20fuertes%20cualidades.&text=Un%20buen%20vino%20que%20merece%20la%20pena%20disfrutar.">escala de Wine Enthusiast</a>, y por cuestiones de facilidad de interpretación de datos, se generó la variable "price/point_ratio", que señala el "precio" que posee cada punto de la escala (aquellos vinos con un ratio menor a 0, son considerados "gangas", al ser baratos para la cantidad de puntos que obtiene). Para ello, se estandarizaron los valores de "price" y "points".</p>
  <h6>Visualización del ratio segun grupos de interés.</h6>
  <p>Empleando el ratio generado, y agrupando los distintos por categorías de interés, se encontró que:</p>
  <img src="#">
  <h6>Implementación y evaluación de modelo de predicción de precio.</h6>
  <p>Se entrenó un modelo de regresión "Random Forest", para predecir el precio en base a determinadas columnas del dataset (se agregaron a X aquellas columnas que mostraban correlación con la variable objetivo).</p>
  <p>La evaluación arrojo valores positivos para las diferentes métricas:</p>
  <img src="#">
<h3>NLP.</h3>
  <h6>Preprocesamiento de texto.</h6>
  <p>Se aplicó un muestreo estratificado por variable "country", debido a la incapacidad de procesar la totalidad de reseñas por el costo computacional que conlleva.</p>
  <p>Las reseñas de la muestra fueron preprocesadas (eliminación de stopwords, lemmatizacion y stemming) empleando las librerias Spacy, y NLTK.</p>
  <h6>Analizar reseñas.</h6>
  <p>Se obtuvo la frecuncia de las palabras mas recurrentes de aquellas reseñas con alto y bajo puntaje, para indagar en posibles diferencias en las reseñas de ambos estratos, empleando wordclouds para su visualización, pero sin encontrar diferencias notables.</p>
  <h6>Modelo de analisis de sentimientos en reseñas.</h6>
  <p>Finalmente, se elaboró un modelo de regresión logística, que pueda clasificar la polaridad de una reseña, como positiva o negativa. Para ello, se creo la columna de polaridad empleando TextBlob para clasificar cada reseña y entrenar al modelo.</p>
  <p>Las métricas de evaluación arrojaron valores positivos para las predicciónes brindadas:</p>
  <img src="#">
<h3>Sistemas de recomendación.</h3>
  <h6>Inspección del dataset.</h6>
  <h6>Visualizaciones de interés.</h6>
  <h6>Transformación e imputacion de datos.</h6>
