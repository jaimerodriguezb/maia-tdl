Transformers | Codificación del texto

Transformers: Codificación de
texto

Cuando se quiere ingresar un fragmento de texto a un Transformer o a una red neuronal para que

sea procesado, es importante primero convertirlo a un formato que la máquina pueda entender. A

partir de esa necesidad, surgieron diferentes métodos para que esta información no solamente sea

reconocida por la máquina, sino que también mantenga su significado semántico.

One hot encoding

Una de las formas más sencillas de convertir información categórica a número es a través de one

hot encoding. En este tipo de codificación, se convierte cada valor categórico (por ejemplo, cada

palabra)  en  un  vector  binario.  A  continuación,  la  Figura  1  muestra  cómo  cada  palabra  tiene

asignada una posición en el vector.

Figura 1. Ejemplo de one hot encoding en una frase simple.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

1

Transformers | Codificación del texto

Si bien el one hot encoding es una forma sencilla de transformar datos categóricos a numéricos,

este tipo de codificación no mantiene ningún significado semántico de las palabras. Por ejemplo,

no es posible tomar la información codificada y saber si la palabra es un sustantivo, un adjetivo, un

verbo, un artículo o si es un animal. A partir de esta necesidad surgen los modelos de embedding,

también llamados modelos de embebimiento o codificación.

Embedding

El  embedding,  es  una  representación  numérica  de  la  información  que  puede  realizarse  en

imágenes, sonido, documentos, texto, código, entre otros. Esta técnica convierte la información a

un formato que le permite a la máquina comprender las relaciones que hay entre los datos. En el

caso  de  texto,  el  embedding  permite  capturar  el  significado  semántico  de  lo  que  se  está

codificando.

                      Figura 2. Vector de representación a partir de un modelo de embedding.

La Figura 2 muestra un ejemplo de un vector de representación que se forma a partir de un modelo

de  embedding  sobre  la  palabra  “perro”.  Si  realizamos  este  proceso  con  múltiples  palabras  y

medimos  las  distancias  de  cada  vector  de  representación  en  un  espacio  arbitrario,  podemos

observar que aquellas palabras con significados semánticos similares se encuentran más cerca. En

la Figura 3, se muestra un ejemplo de un embedding clásico conocido como Word2vec. En esta

figura, se muestra una proyección en dos dimensiones de algunas palabras tras ser codificadas en

un espacio de 300 dimensiones con el algoritmo Word2vec.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

2

Transformers | Codificación del texto

Figura  3.  Espacio  de  representación  del  embedding  de  palabras  cotidianas.  Las
palabras con significados semánticos similares se encuentran a menor distancia.

Modelos de embedding

A  diferencia  del  one  hot  encoding,  para  realizar  el  embedding  de  los  datos  es  usual  utilizar  un

modelo  preentrenado.  Algunos  ejemplos  de  modelos  de  embedding  son  Instructor,  Sentence

Transformers y los modelos de OpenAI: Ada, Davinci, Curie y Babbage.

3

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

Transformers | Codificación del texto

Una vez se obtiene el vector del embedding, es posible utilizar los datos para múltiples tareas. Por

ejemplo,  es  posible  medir  la  distancia  de  las  representaciones  de  dos  frases  para  ver  si  tienen

significados  similares.  También,  es  posible  pasar  una  imagen  por  el  modelo  de  embedding  y

comparar su espacio de  representación con respecto  al espacio de  una frase  para determinar si

están relacionadas. Este último ejemplo suele utilizarse en los motores de búsqueda para encontrar

imágenes que se asocien al mensaje de la barra de búsqueda. Del mismo modo, esta información

también se usa para publicidad en redes sociales.

Conclusiones

El  embedding  convierte  los  datos  a  una  representación  numérica  que  mantiene  el  significado

semántico y las relaciones entre la información. Se puede utilizar en múltiples tipos de datos y es

comúnmente  utilizado  en  el  procesamiento  de  lenguaje  natural.  Aquellos  vectores  que  se

encuentren  relacionados  se  encontrarán  más  cerca  en  el  espacio  de  representación,  esta

característica se utiliza comúnmente en los motores de búsqueda y en los sistemas automatizados

de publicidad.

Bibliografía

Muennighoff, N., Tazi, N., Magne, L., & Reimers, N. (2022). MTEB: Massive Text Embedding Benchmark. ArXiv

Preprint ArXiv:2210. 07316. doi:10.48550/ARXIV.2210.07316

OpenAI. (2022). New and Improved Embedding Model. [Internet]. Tomado de: https://openai.com/blog/new-

and-improved-embedding-model

Espejel, O. (2022). Getting Started With Embeddings. [Internet]. Tomado de:

https://huggingface.co/blog/getting-started-with-embeddings

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

4

Transformers | Codificación del texto

© - Derechos Reservados: la presente obra, y en general todos sus
contenidos, se encuentran protegidos por las normas internacionales y
nacionales vigentes sobre propiedad Intelectual, por lo tanto su utilización
parcial o total, reproducción, comunicación pública, transformación,
distribución, alquiler, préstamo público e importación, total o parcial, en
todo o en parte, en formato impreso o digital y en cualquier formato
conocido o por conocer, se encuentran prohibidos, y solo serán lícitos en la
medida en que se cuente con la autorización previa y expresa por escrito de
la Universidad de los Andes.

De igual manera, la utilización de la imagen de las personas, docentes o
estudiantes, sin su previa autorización está expresamente prohibida. En
caso de incumplirse con lo mencionado, se procederá de conformidad con
los reglamentos y políticas de la universidad, sin perjuicio de las demás
acciones legales aplicables.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

5

