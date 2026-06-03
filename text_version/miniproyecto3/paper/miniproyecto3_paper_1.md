Clasificación de Artículos de Noticias de la BBC usando Transformers
Yezid Garcia1, Juan Martin Santos1 y Jaime Rodriguez1
1Universidad de los Andes, Bogotá, Colombia
Códigos: 200810710, 202013610, 200717791
I. INTRODUCCIÓN B. Preprocesamiento
El texto de cada artículo se tokeniza con el vocabulario
El procesamiento de lenguaje natural ha avanzado con
WordPiece de DistilBERT, que descompone las palabras en
la introducción de la arquitectura transformer [1], que
subpalabras frecuentes en el corpus de preentrenamiento. A
reemplaza las redes recurrentes por mecanismos de aten-
cada secuencia se agregan los tokens especiales [CLS] al
ción capaces de relacionar cualquier par de posiciones de
inicioy[SEP]alfinal.Lassecuenciassetruncanorellenan
una secuencia en tiempo constante. Este diseño supera la
hasta una longitud máxima de 256 tokens. Se genera una
degradación de gradiente que afecta a las LSTM en se-
máscara de atención binaria que indica al modelo cuáles
cuencias largas y ha dado lugar a modelos de lenguaje
posiciones corresponden a contenido real y cuáles a relleno.
preentrenados como BERT [2] y GPT [5], cuyo ajuste fino
Lasetiquetasdecategoríasecodificancomoenterosdel0al
sobre tareas específicas alcanza resultados comparables o
4.Latokenizacióndelconjuntocompletoserealizaunasola
superiores a los de modelos entrenados desde cero con
vez antes del entrenamiento para evitar cómputo redundante
órdenes de magnitud más datos etiquetados.
en cada época.
La clasificación automática de noticias presenta el reto
de asignar categorías temáticas a textos de longitud variable C. Arquitectura
conposiblesolapamientosemánticoentretemas.Unartículo
El modelo se organiza en dos bloques. El primer bloque
sobre regulación tecnológica puede compartir términos con
es DistilBERT [3], que procesa la secuencia de tokens
noticias de economía o política; una crónica deportiva que
mediante seis capas de atención multi-cabeza y produce
mencionacifrasfinancieraspuedeconfundirseconcontenido
una representación contextual para cada posición. La rep-
de negocios. Las soluciones basadas en representaciones de
resentación del token [CLS], que agrega el contexto global
bolsa de palabras pierden el orden y el contexto necesarios
de la secuencia, se extrae como vector de 768 dimensiones.
para resolver estas ambigüedades.
El segundo bloque es una capa de clasificación lineal que
En este trabajo se implementa un clasificador de cinco
proyecta este vector sobre cinco clases y aplica la función
categorías sobre el corpus BBC News [4] utilizando Dis-
softmax para obtener una distribución de probabilidad. El
tilBERT [3], versión destilada de BERT que conserva el
modelo tiene aproximadamente 67 millones de parámetros
97% delrendimiento conla mitadde parámetros.El modelo
entrenables. Este diseño sigue el patrón de clasificación de
se ajusta mediante fine-tuning durante cinco épocas. El
secuencias de BERT [2], adaptado a la versión destilada.
documento describe el conjunto de datos, la arquitectura, el
procedimiento de entrenamiento, los resultados cuantitativos D. Entrenamiento y métricas
y cualitativos obtenidos, y concluye con una discusión sobre
El modelo se entrena durante cinco épocas con el opti-
las limitaciones y el trabajo futuro.
mizadorAdamWcontasadeaprendizajeinicialde2×10−5.
Seaplicaunschedulerlinealconfasedecalentamientoenel
II. METODOLOGÍA 10% de los pasos totales de entrenamiento, lo que reduce la
magnitud de las actualizaciones durante las primeras itera-
A. Datos ciones y estabiliza el ajuste fino de los pesos preentrenados.
El gradiente se recorta a una norma máxima de 1.0 antes
Se utiliza el conjunto BBC News [4], compuesto por
de cada actualización. El tamaño de lote es 16. Se guarda
2225 artículos periodísticos distribuidos en cinco categorías:
el checkpoint con la menor pérdida sobre el conjunto de
business (510), entertainment (386), politics (417), sport
validación y este se usa para la evaluación final.
(511) y tech (401). Cada artículo contiene el titular y el
Lasmétricasdeevaluaciónsonprecisión,recallyF1-score
cuerpodeltextocomocadenaplana.Elconjuntonopresenta
porcategoría,yexactitudglobalsobreelconjuntodeprueba.
valores nulos ni duplicados.
Los datos se dividen de forma estratificada en tres sub-
III. RESULTADOS
conjuntos: entrenamiento (70%, 1557 artículos), validación
A. Resultados cuantitativos
(15%, 334 artículos) y prueba (15%, 334 artículos). La
partición estratificada preserva la proporción de categorías La Tabla 1 presenta los resultados del modelo sobre el
en cada subconjunto. conjunto de prueba (334 artículos). El modelo alcanza una

exactitud global de 97.90% (327 de 334 artículos correcta- y GPT-3 [7], reduce el costo de entrenamiento en dominios
mente clasificados) y un F1-score macro de 0.979. concretos al partir de pesosya ajustados al lenguaje general.
|     |     |     |     |     |     |     |     | La arquitectura |     | transformer |     | subyacente | [1] | presenta | ven- |
| --- | --- | --- | --- | --- | --- | --- | --- | --------------- | --- | ----------- | --- | ---------- | --- | -------- | ---- |
TABLE1
|     |     |     |     |     |     |     |     | tajas frente | a   | redes | recurrentes | para | el procesamiento |     | de  |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------ | --- | ----- | ----------- | ---- | ---------------- | --- | --- |
PRECISIÓN,RECALLYF1-SCOREPORCATEGORÍAENELCONJUNTODE texto periodístico: su atención global permite relacionar el
PRUEBA(334ARTÍCULOS).
|           |     |           |     |        |        |         |     | titular con  | párrafos | posteriores |           | del artículo, |          | integrar     | señales |
| --------- | --- | --------- | --- | ------ | ------ | ------- | --- | ------------ | -------- | ----------- | --------- | ------------- | -------- | ------------ | ------- |
|           |     |           |     |        |        |         |     | de distintas | partes   | del         | documento | y             | resolver | ambigüedades |         |
| Categoría |     | Precisión |     | Recall | F1     | Soporte |     |              |          |             |           |               |          |              |         |
|           |     |           |     |        |        |         |     | léxicas      | mediante | contexto.   |           | En el caso    | de       | politics,    | aunque  |
| business  |     | 0.9610    |     | 0.9610 | 0.9610 |         | 77  |              |          |             |           |               |          |              |         |
entertainment 0.9828 0.9828 0.9828 58 los artículos comparten vocabulario con otras categorías, la
distribuciónglobaldeltextocontieneseñalessuficientespara
| politics |     | 0.9672 |     | 0.9516 | 0.9593 |     | 62  |     |     |     |     |     |     |     |     |
| -------- | --- | ------ | --- | ------ | ------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
sport 1.0000 1.0000 1.0000 77 la clasificación correcta en el 95.16% de los casos.
tech 0.9836 1.0000 0.9917 60 Entre las limitaciones del trabajo se encuentran el tamaño
macro avg 0.9789 0.9791 0.9790 334 del conjunto de datos (2225 artículos), la ausencia de una
|     |     |     |     |     |     |     |     | comparación | directa |     | con modelos | de  | referencia | como | clasi- |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------- | ------- | --- | ----------- | --- | ---------- | ---- | ------ |
Como se observa en la Tabla 1, la categoría sport obtuvo ficadoressobrerepresentacionesTF-IDForegresiónlogística
clasificaciónperfecta(F1=1.0).Lacategoríatechobtuvore- sobre características del token [CLS] sin ajuste fino, y la
callperfectoconprecisiónde0.9836,indicandoquetodoslos falta de un estudio de ablación que aísle el efecto individual
artículos de tecnología fueron recuperados aunque algunos del scheduler y el recorte de gradiente sobre la calidad del
artículos de otras categorías se asignaron incorrectamente modelo. Como trabajo futuro se propone evaluar el modelo
a esta clase. La categoría politics presentó el F1 más bajo en conjuntos de noticias de otras fuentes o idiomas para
(0.9593) con un recall de 0.9516, lo que indica que algunos medir la capacidad de generalización entre dominios, incor-
artículos de política fueron clasificados en otras categorías. porar un análisis de errores por categoría que identifique los
En la versión base del pipeline, sin scheduler lineal patrones léxicos asociados a las confusiones, y comparar el
ni recorte de gradiente, la pérdida de validación presentó fine-tuning completo frente a la extracción de características
mayorvarianzaentreépocas.Laincorporacióndelscheduler con el backbone congelado.
| con calentamiento |     | y   | el recorte | de  | gradiente | estabilizó | la  |     |     |     |     |     |     |     |     |
| ----------------- | --- | --- | ---------- | --- | --------- | ---------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
REFERENCES
| convergencia, |     | lo que | respalda | el uso | de  | estas técnicas | en  |     |     |     |     |     |     |     |     |
| ------------- | --- | ------ | -------- | ------ | --- | -------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
el ajuste fino de transformers sobre conjuntos de datos de [1] A. Vaswani, N. Shazeer, N. Parmar, J. Uszkoreit, L. Jones, A. N.
|     |     |     |     |     |     |     |     | Gomez, | L.  | Kaiser e | I. Polosukhin, | “Attention | Is  | All You Need,” | en  |
| --- | --- | --- | --- | --- | --- | --- | --- | ------ | --- | -------- | -------------- | ---------- | --- | -------------- | --- |
tamaño moderado.
|     |     |     |     |     |     |     |     | Advances | in  | Neural | Information | Processing | Systems | (NeurIPS), | vol. |
| --- | --- | --- | --- | --- | --- | --- | --- | -------- | --- | ------ | ----------- | ---------- | ------- | ---------- | ---- |
30,2017.
B. Resultados cualitativos [2] J.Devlin,M.-W.Chang,K.LeeyK.Toutanova,“BERT:Pre-training
ofDeepBidirectionalTransformersforLanguageUnderstanding,”en
| El modelo |     | distingue | con | mayor | facilidad | las categorías |     |     |     |     |     |     |     |     |     |
| --------- | --- | --------- | --- | ----- | --------- | -------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Proc.NAACL-HLT,págs.4171–4186,2019.
| con vocabulario |     | específico | y   | bajo | solapamiento | semántico |     |              |     |        |             |            |              |     |           |
| --------------- | --- | ---------- | --- | ---- | ------------ | --------- | --- | ------------ | --- | ------ | ----------- | ---------- | ------------ | --- | --------- |
|                 |     |            |     |      |              |           |     | [3] V. Sanh, | L.  | Debut, | J. Chaumond | y T. Wolf, | “DistilBERT, | a   | distilled |
sport versionofBERT:smaller,faster,cheaperandlighter,”arXivpreprint
| con otras. | La categoría |     |     | concentra | términos | propios | del |     |     |     |     |     |     |     |     |
| ---------- | ------------ | --- | --- | --------- | -------- | ------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
arXiv:1910.01108,2019.
| dominio    | deportivo | —nombres    |     | de competencias, |     | marcadores  |     |               |     |                |     |            |           |                |     |
| ---------- | --------- | ----------- | --- | ---------------- | --- | ----------- | --- | ------------- | --- | -------------- | --- | ---------- | --------- | -------------- | --- |
|            |           |             |     |                  |     |             |     | [4] D. Greene | y   | P. Cunningham, |     | “Practical | Solutions | to the Problem | of  |
| y equipos— | que       | no aparecen |     | con frecuencia   |     | en noticias | de  |               |     |                |     |            |           |                |     |
DiagonalDominanceinKernelDocumentClustering,”enProc.23rd
economía o tecnología, lo que facilita su separación. Int.Conf.MachineLearning(ICML),págs.377–384,2006.
|              |     |          |       |          |             |           |     | [5] A. Radford, |               | K. Narasimhan, |     | T. Salimans | e I. Sutskever, | “Improving |     |
| ------------ | --- | -------- | ----- | -------- | ----------- | --------- | --- | --------------- | ------------- | -------------- | --- | ----------- | --------------- | ---------- | --- |
| La categoría |     | politics | es la | de mayor | dificultad. | Artículos |     |                 |               |                |     |             |                 |            |     |
|              |     |          |       |          |             |           |     | Language        | Understanding |                | by  | Generative  | Pre-Training,”  | Technical  | Re- |
que cubren política económica o regulación tecnológica port,OpenAI,2018.
comparten términos con business y tech, y la distinción [6] C.Raffel,N.Shazeer,A.Roberts,K.Lee,S.Narang,M.Matena,Y.
depende del contexto global del artículo. El mecanismo de Zhou, W. Li y P. J. Liu, “Exploring the Limits of Transfer Learning
withaUnifiedText-to-TextTransformer,”JournalofMachineLearn-
atención de DistilBERT permite capturar relaciones de largo ingResearch,vol.21,núm.140,págs.1–67,2020.
alcance entre palabras del texto, lo que en la mayoría de [7] T. B. Brown et al., “Language Models are Few-Shot Learners,” en
los casos permite resolver esta ambigüedad a partir de la Advances in Neural Information Processing Systems (NeurIPS), vol.
33,2020.
| representación  |              | del token         | [CLS].     |            | Los siete     | artículos      | mal     |     |     |     |     |     |     |     |     |
| --------------- | ------------ | ----------------- | ---------- | ---------- | ------------- | -------------- | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
| clasificados    | corresponden |                   | en         | su mayoría |               | a este         | tipo de |     |     |     |     |     |     |     |     |
| solapamiento    | temático.    |                   |            |            |               |                |         |     |     |     |     |     |     |     |     |
|                 |              | IV.               | DISCUSIÓN  |            |               |                |         |     |     |     |     |     |     |     |     |
| El resultado    |              | de 97.90%         | de         | exactitud  | con           | cinco          | épocas  |     |     |     |     |     |     |     |     |
| de ajuste       | fino         | sobre 2225        | documentos |            | ilustra       | la efectividad |         |     |     |     |     |     |     |     |     |
| del aprendizaje |              | por transferencia |            | en         | clasificación | de             | texto.  |     |     |     |     |     |     |     |     |
| DistilBERT      | [3]          | fue preentrenado  |            | sobre      | grandes       | corpus         | de      |     |     |     |     |     |     |     |     |
textoeninglésmedianteprediccióndetokensenmascarados,
| lo que le    | permite   | capturar | estructura |             | sintáctica | y semántica     |        |     |     |     |     |     |     |     |     |
| ------------ | --------- | -------- | ---------- | ----------- | ---------- | --------------- | ------ | --- | --- | --- | --- | --- | --- | --- | --- |
| sin requerir | etiquetas |          | de tarea   | específica. |            | Este principio, |        |     |     |     |     |     |     |     |     |
| introducido  | por       | BERT     | [2] y      | extendido   | en         | GPT [5],        | T5 [6] |     |     |     |     |     |     |     |     |