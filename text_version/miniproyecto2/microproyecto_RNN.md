Clasificación de Sentimientos de Reseñas de Películas en IMDb con Redes
Neuronales Recurrentes

Los ratings y reseñas de películas son una fuente rica de datos textuales que pueden
ser analizados para identificar el sentimiento subyacente, ya sea positivo o negativo.
El uso de redes neuronales recurrentes (RNN) ha demostrado ser eficaz en la
clasificación de secuencias de texto, ya que estas redes pueden capturar la
información contextual en oraciones y palabras, identificando patrones relevantes
para determinar la polaridad de una reseña.

Redes Neuronales Recurrentes

Las RNN son especialmente adecuadas para el análisis de datos secuenciales como
texto, ya que tienen la capacidad de almacenar y recordar información previa en la
secuencia, lo cual es crucial para entender el contexto. Al aplicar una RNN a reseñas
de películas, la red puede ser entrenada para identificar palabras, frases y patrones
que generalmente se asocian con sentimientos positivos o negativos.

Procesamiento de Texto

El procesamiento de texto para este proyecto implica convertir las reseñas en un
formato numérico que la RNN pueda procesar. Esto se logra a través de técnicas
como la tokenización y la vectorización de palabras (por ejemplo, utilizando
embeddings). Luego, la RNN analizará la secuencia de palabras para clasificar cada
reseña en una de dos categorías: positiva o negativa.

Ventajas y Aplicaciones

Implementar RNN para la clasificación de sentimientos en reseñas de películas
ofrece varias ventajas:

-  Detección precisa de emociones: Mejora la capacidad de capturar sentimientos

más matizados en textos largos y complejos.

-  Adaptabilidad a distintos idiomas y contextos: Las RNN pueden ser entrenadas

en diferentes conjuntos de datos para adaptarse a lenguajes y contextos
específicos, como géneros de películas o plataformas de reseñas.

-  Asistencia en sistemas de recomendación: Permite mejorar las

recomendaciones personalizadas en plataformas de streaming basadas en el
análisis de reseñas de usuarios.

A. Objetivo

-  Desarrollar un método basado en redes neuronales recurrentes que permita
clasificar con precisión las reseñas de películas en IMDb en una de las dos
categorías: positiva o negativa.

B. Conjunto de datos

-  Los datos corresponden a un dataset de reseñas de películas en IMDb,
disponibles en el siguiente enlace. El dataset contiene miles de reseñas
etiquetadas con su correspondiente rating y etiqueta de sentimiento (positivo o
negativo).

C. Actividades por realizar

1.  Preprocesamiento de las reseñas: Construir un pipeline que permita limpiar y

tokenizar las reseñas de texto, convirtiéndolas en secuencias numéricas
utilizando embeddings (por ejemplo, Word2Vec o GloVe).

2.  Desarrollo de la arquitectura de red neuronal recurrente: Implementar una
RNN (por ejemplo, LSTM o GRU) para la clasificación de las reseñas en dos
categorías. La arquitectura de la red es de libre elección, pero se sugiere incluir
capas de embedding, capas recurrentes y una capa densa de salida con
activación sigmoide. Justificar la elección de cada capa del modelo.

3.  Entrenamiento y evaluación del modelo: Dividir el dataset en conjuntos de

entrenamiento, validación y prueba. Entrenar el modelo utilizando el conjunto de
entrenamiento y evaluar su rendimiento con el conjunto de prueba, reportando
métricas de precisión, recall y F1-score.

