Clasificación de Artículos de Noticias de la BBC usando Transformers

Yezid Garcia1, Juan Martin Santos1 y Jaime Rodriguez1
1Universidad de los Andes, Bogotá, Colombia
Códigos: 200810710, 202013610, 200717791

I. INTRODUCCIÓN

La arquitectura transformer, propuesta por Vaswani et
al. [1], reemplaza las redes recurrentes por mecanismos
de atención que relacionan cualquier par de posiciones de
una secuencia en tiempo constante. Este diseño elimina la
dependencia secuencial de las LSTM y permite paralelizar
el entrenamiento sobre secuencias largas. Sobre esta base,
Devlin et al. [2] desarrollaron BERT, un modelo preentrenado
mediante predicción de tokens enmascarados en grandes
corpus no etiquetados, cuyo ajuste fino sobre tareas especí-
ficas establece resultados de referencia en clasificación de
texto, extracción de información y preguntas y respuestas.
En paralelo, Radford et al. [3] demostraron con GPT que
el preentrenamiento autorregresivo seguido de fine-tuning
también generaliza bien a múltiples tareas de comprensión
del lenguaje.

La clasificación automática de noticias presenta el reto
de asignar categorías temáticas a textos de longitud variable
con solapamiento semántico entre dominios. El corpus BBC
News [4], con 2225 artículos en cinco categorías, es un
banco de prueba estándar para este problema: un artículo
de política económica comparte términos con noticias de
negocios; una crónica deportiva con cifras puede confundirse
con contenido financiero. Las soluciones basadas en bolsa
de palabras pierden el orden y el contexto necesarios para
resolver estas ambigüedades.

En este trabajo se implementa un clasificador sobre el
corpus BBC News usando DistilBERT [5], versión destilada
de BERT que conserva el 97% de su rendimiento con la
mitad de parámetros. El modelo se ajusta mediante fine-
tuning durante cinco épocas. El documento describe los
datos, la arquitectura, el procedimiento de entrenamiento,
los resultados cuantitativos con curvas de entrenamiento, los
resultados cualitativos y una discusión sobre limitaciones y
trabajo futuro.

II. METODOLOGÍA

A. Datos

Se utiliza el conjunto BBC News [4], compuesto por
2225 artículos periodísticos en cinco categorías: business
(510), entertainment (386), politics (417), sport (511) y tech
(401). Cada entrada contiene el titular y el cuerpo del texto
como cadena plana. El conjunto no presenta valores nulos ni
duplicados.

Los datos se dividen de forma estratificada en tres sub-
conjuntos: entrenamiento (70%, 1557 artículos), validación

(15%, 334 artículos) y prueba (15%, 334 artículos). La
partición estratificada preserva la proporción de categorías
en cada subconjunto.

B. Preprocesamiento

El texto se tokeniza con el vocabulario WordPiece de
DistilBERT, que descompone las palabras en subpalabras
frecuentes del corpus de preentrenamiento. A cada secuencia
se agregan los tokens especiales [CLS] al inicio y [SEP] al
final, siguiendo el esquema de BERT [2]. Las secuencias se
truncan o rellenan hasta 256 tokens. Una máscara de atención
binaria indica cuáles posiciones corresponden a contenido
real. Las etiquetas de categoría se codifican como enteros
del 0 al 4. La tokenización del conjunto completo se ejecuta
una sola vez antes del entrenamiento para evitar cómputo
redundante en cada época.

C. Arquitectura

El modelo se organiza en dos bloques, siguiendo el
esquema de clasificación de secuencias de BERT [2]. El
primer bloque es DistilBERT [5], que procesa la secuencia
mediante seis capas de atención multi-cabeza y produce
una representación contextual para cada posición. La repre-
sentación del token [CLS] —que agrega el contexto global
de la secuencia— se extrae como vector de 768 dimensiones.
El segundo bloque es una capa de clasificación lineal que
proyecta este vector sobre cinco clases y aplica softmax. El
modelo tiene aproximadamente 67 millones de parámetros.

D. Entrenamiento y métricas

El modelo se entrena durante cinco épocas con el opti-
mizador AdamW con tasa de aprendizaje inicial 2 × 10−5.
Se aplica un scheduler lineal con calentamiento en el 10%
de los pasos totales,
lo que reduce la magnitud de las
actualizaciones iniciales y estabiliza el ajuste fino de los
pesos preentrenados. El gradiente se recorta a norma máxima
1.0 antes de cada actualización. El tamaño de lote es 16. Se
guarda el checkpoint con menor pérdida de validación, que
se usa para la evaluación final.

Las métricas de evaluación son precisión, recall y F1-score
por categoría, y exactitud global sobre el conjunto de prueba.

III. RESULTADOS

A. Resultados cuantitativos

La Tabla 1 presenta los resultados sobre el conjunto de
prueba (334 artículos). El modelo alcanza una exactitud
global de 97.90% (327/334) y un F1-score macro de 0.979.

del aprendizaje por transferencia introducido por BERT [2]
y GPT [3]. DistilBERT [5], preentrenado sobre grandes
corpus mediante predicción de tokens enmascarados, captura
estructura sintáctica y semántica del lenguaje sin requerir
etiquetas de tarea. El ajuste fino sobre el corpus BBC orienta
esta representación general hacia la clasificación temática
en pocas épocas, lo que confirma el principio demostrado
también por T5 [6] y GPT-3 [7]: el costo de adaptación a
un dominio específico se reduce sustancialmente al partir de
pesos preentrenados en texto general.

La arquitectura transformer [1] presenta ventajas frente a
redes recurrentes para texto periodístico. Su atención global
permite relacionar el titular con información de párrafos pos-
teriores del artículo e integrar señales distribuidas a lo largo
del documento. En el caso de politics, aunque los artículos
comparten vocabulario con otras categorías, la representación
contextual del token [CLS] contiene señales suficientes para
la clasificación correcta en el 95.16% de los casos.

Entre las limitaciones del trabajo se encuentran el tamaño
del conjunto (2225 artículos), la ausencia de una línea base
cuantitativa como clasificación sobre representaciones TF-
IDF o DistilBERT con backbone congelado sin fine-tuning,
y la falta de un estudio de ablación que aísle el efecto indi-
vidual del scheduler y el recorte de gradiente. Como trabajo
futuro se propone comparar el fine-tuning completo frente
a la extracción de características con backbone congelado,
evaluar el modelo en corpus de noticias de otras fuentes para
medir generalización entre dominios, y realizar un análisis
de errores por categoría que identifique los patrones léxicos
asociados a las confusiones en politics.

REFERENCES

[1] A. Vaswani, N. Shazeer, N. Parmar, J. Uszkoreit, L. Jones, A. N.
Gomez, L. Kaiser e I. Polosukhin, “Attention Is All You Need,” en
Advances in Neural Information Processing Systems (NeurIPS), vol.
30, 2017.

[2] J. Devlin, M.-W. Chang, K. Lee y K. Toutanova, “BERT: Pre-training
of Deep Bidirectional Transformers for Language Understanding,” en
Proc. NAACL-HLT, págs. 4171–4186, 2019.

[3] A. Radford, K. Narasimhan, T. Salimans e I. Sutskever, “Improving
Language Understanding by Generative Pre-Training,” Technical Re-
port, OpenAI, 2018.

[4] D. Greene y P. Cunningham, “Practical Solutions to the Problem of
Diagonal Dominance in Kernel Document Clustering,” en Proc. 23rd
Int. Conf. Machine Learning (ICML), págs. 377–384, 2006.

[5] V. Sanh, L. Debut, J. Chaumond y T. Wolf, “DistilBERT, a distilled
version of BERT: smaller, faster, cheaper and lighter,” arXiv preprint
arXiv:1910.01108, 2019.

[6] C. Raffel, N. Shazeer, A. Roberts, K. Lee, S. Narang, M. Matena, Y.
Zhou, W. Li y P. J. Liu, “Exploring the Limits of Transfer Learning
with a Unified Text-to-Text Transformer,” Journal of Machine Learn-
ing Research, vol. 21, núm. 140, págs. 1–67, 2020.

[7] T. B. Brown et al., “Language Models are Few-Shot Learners,” en
Advances in Neural Information Processing Systems (NeurIPS), vol.
33, 2020.

TABLE 1
PRECISIÓN, RECALL Y F1-SCORE POR CATEGORÍA EN EL CONJUNTO DE
PRUEBA.

Categoría
business
entertainment
politics
sport
tech
macro avg

Precisión
0.9610
0.9828
0.9672
1.0000
0.9836
0.9789

Recall
0.9610
0.9828
0.9516
1.0000
1.0000
0.9791

F1
0.9610
0.9828
0.9593
1.0000
0.9917
0.9790

Soporte
77
58
62
77
60
334

Como se observa en la Tabla 1, sport obtuvo clasificación
perfecta (F1 = 1.0) y tech obtuvo recall perfecto (1.0) con
precisión de 0.9836. La categoría politics presentó el F1 más
bajo (0.9593) con recall de 0.9516, indicando que algunos
artículos de política se asignaron a otras categorías.

La Fig. 1 muestra las curvas de pérdida y exactitud durante
el entrenamiento. La pérdida de validación desciende de
forma consistente durante las primeras épocas y se estabiliza,
lo que indica convergencia sin sobreajuste dentro del rango
de cinco épocas. La incorporación del scheduler con calen-
tamiento y el recorte de gradiente —ausentes en una versión
previa del pipeline— redujo la varianza de la pérdida entre
épocas, produciendo curvas más regulares.

Fig. 1. Curvas de pérdida (izquierda) y exactitud (derecha) por época sobre
los conjuntos de entrenamiento y validación. Generadas desde el notebook
de entrenamiento.

B. Resultados cualitativos

El modelo diferencia con mayor facilidad las categorías
con vocabulario específico. Sport concentra términos de
dominio deportivo —nombres de competencias, marcadores,
equipos— que no aparecen en otras categorías. Tech incluye
términos de tecnología cuya precisión de 0.9836 menor que
1.0 sugiere que algunos artículos de otras categorías con
contenido tecnológico se clasificaron en esta clase.

Politics es la categoría de mayor dificultad. Artículos
sobre política económica o regulación tecnológica comparten
vocabulario con business y tech. El mecanismo de atención
de DistilBERT captura relaciones de largo alcance entre
palabras del texto, lo que permite resolver la mayoría de estas
ambigüedades a partir de la representación del token [CLS].
Los siete artículos clasificados incorrectamente corresponden
en su mayoría a este tipo de solapamiento temático.

IV. DISCUSIÓN

El resultado de 97.90% de exactitud con cinco épocas
de fine-tuning sobre 2225 documentos ilustra la efectividad

