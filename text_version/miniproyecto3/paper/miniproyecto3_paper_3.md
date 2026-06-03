Clasificación de Artículos de Noticias de la BBC usando Transformers
Yezid Garcia1, Juan Martin Santos1 y Jaime Rodriguez1
1Universidad de los Andes, Bogotá, Colombia
Códigos: 200810710, 202013610, 200717791
I. INTRODUCCIÓN Los datos se dividen de forma estratificada en tres sub-
conjuntos: entrenamiento (70%, 1557 artículos), validación
La arquitectura transformer, propuesta por Vaswani et
(15%, 334 artículos) y prueba (15%, 334 artículos). La
al. [1], reemplaza las redes recurrentes por mecanismos
partición estratificada preserva la proporción de categorías
de atención que relacionan cualquier par de posiciones de
en cada subconjunto.
una secuencia en tiempo constante. Este diseño elimina la
dependencia secuencial de las LSTM y permite paralelizar B. Preprocesamiento
el entrenamiento sobre secuencias largas. Sobre esta base,
El texto se tokeniza con el vocabulario WordPiece de
Devlinetal.[2]desarrollaronBERT,unmodelopreentrenado
DistilBERT, que descompone las palabras en subpalabras
mediante predicción de tokens enmascarados en grandes
frecuentesdelcorpusdepreentrenamiento.Acadasecuencia
corpus no etiquetados, cuyo ajuste fino sobre tareas especí-
seagreganlostokensespeciales[CLS]alinicioy[SEP]al
ficas establece resultados de referencia en clasificación de
final, siguiendo el esquema de BERT [2]. Las secuencias se
texto, extracción de información, preguntas y respuestas.
truncanorellenanhasta256tokens.Unamáscaradeatención
En paralelo, Radford et al. [3] demostraron con GPT que
binaria indica cuáles posiciones corresponden a contenido
el preentrenamiento autorregresivo seguido de fine-tuning
real. Las etiquetas de categoría se codifican como enteros
también generaliza bien.
del 0 al 4. La tokenización del conjunto completo se ejecuta
La clasificación automática de noticias presenta el reto
una sola vez antes del entrenamiento para evitar cómputo
de asignar categorías temáticas a textos de longitud variable
redundante en cada época.
con traslape semántico. El corpus BBC News [4], con 2225
artículosencincocategorías,esunbancodepruebaestándar C. Arquitectura
para este problema: un artículo de económica comparte El modelo se organiza en dos bloques, siguiendo el
términos con noticias de negocios; una crónica deportiva esquema de clasificación de secuencias de BERT [2]. El
con cifras puede confundirse con contenido financiero. Las primer bloque es DistilBERT [5], que procesa la secuencia
soluciones basadas en bolsa de palabras pierden el orden y mediante seis capas de atención multi-cabeza y produce una
el contexto necesarios para resolver estas ambigüedades. representación contextual para cada posición. Cada bloque
En este trabajo se implementa un clasificador sobre el transformer incluye una capa de atención con proyecciones
corpus BBC News usando DistilBERT [5], versión destilada lineal Q, K y V de dimensión 768, normalización de
de BERT que conserva el 97% de su rendimiento con la capa, una red de avance posición a posición con activación
mitad de parámetros. El modelo se ajusta mediante fine- GELU (768→3072→768) y normalización de salida. La
tuning durante cinco épocas. El documento describe los representación del token [CLS] se extrae como vector
datos, la arquitectura, el procedimiento de entrenamiento, de 768 dimensiones. El segundo bloque es una cabeza
los resultados cuantitativos con curvas de entrenamiento, los de clasificación compuesta por una capa lineal intermedia
resultados cualitativos y una discusión sobre limitaciones y (768→768) seguida de una capa de salida (768→5) con
trabajo futuro. softmax. El modelo tiene aproximadamente 67 millones de
parámetros. La Fig. 1 muestra la arquitectura completa.
II. METODOLOGÍA
D. Entrenamiento y métricas
Paraeldesarrollodelproyectosesiguióelciclotradicional
de aprendizaje automático: entendimiento del problema, re- El modelo se entrena durante cinco épocas con el opti-
copilaciónypreparacióndelosdatos,diseñoyentrenamiento mizador AdamW con tasa de aprendizaje inicial 2×10−5.
delmodelo,evaluaciónsobreunconjuntodepruebaindepen- Se aplica un scheduler lineal con calentamiento en el 10%
diente, y análisis de los resultados obtenidos. de los pasos totales, lo que reduce la magnitud de las
actualizaciones iniciales y estabiliza el ajuste fino de los
A. Datos
pesospreentrenados.Elgradienteserecortaanormamáxima
SeutilizaelconjuntoBBCNews[4],compuestopor2225 1.0 antes de cada actualización. El tamaño de lote es 16. Se
artículos periodísticos en cinco categorías: business (510), guarda el checkpoint con menor pérdida de validación, que
entertainment (386), politics (417),sport (511) y tech (401). se usa para la evaluación final.
Cada entrada contiene el titular y el cuerpo del texto como Lasmétricasdeevaluaciónsonprecisión,recallyF1-score
cadena plana. El conjunto no presenta valores nulos. porcategoría,yexactitudglobalsobreelconjuntodeprueba.

|     |     |     |     |     |     |     | Fig.2. Curvasdepérdida(izquierda)yexactitud(derecha)porépocasobre |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ----------------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
losconjuntosdeentrenamientoyvalidación.
|     |     |     |     |     |     |     | equipos— | que no         | aparecen | en           | otras categorías. |           | Tech | incluye   |
| --- | --- | --- | --- | --- | --- | --- | -------- | -------------- | -------- | ------------ | ----------------- | --------- | ---- | --------- |
|     |     |     |     |     |     |     | términos | de tecnología; |          | su precisión |                   | de 0.9836 |      | menor que |
Fig. 1. Arquitectura del modelo obtenida del notebook. El bloque 1.0 sugiere que algunos artículos de otras categorías con
| DistilBERT | (6 capas | transformer) | produce | la representación |     | [CLS], que |           |             |     |              |     |         |        |     |
| ---------- | -------- | ------------ | ------- | ----------------- | --- | ---------- | --------- | ----------- | --- | ------------ | --- | ------- | ------ | --- |
|            |          |              |         |                   |     |            | contenido | tecnológico | se  | clasificaron |     | en esta | clase. |     |
seproyectasobre5clasesmediantelacabezadeclasificación.
|     |     |     |     |     |     |     | Politics | es la | categoría | de  | mayor | dificultad. |     | Artículos |
| --- | --- | --- | --- | --- | --- | --- | -------- | ----- | --------- | --- | ----- | ----------- | --- | --------- |
sobrepolíticaeconómicaoregulacióntecnológicacomparten
|                |     |            |            |     |             |       |               |     | business | tech.      |     |           |         |          |
| -------------- | --- | ---------- | ---------- | --- | ----------- | ----- | ------------- | --- | -------- | ---------- | --- | --------- | ------- | -------- |
|                |     | III.       | RESULTADOS |     |             |       | vocabulario   | con |          | y          | El  | mecanismo | de      | atención |
|                |     |            |            |     |             |       | de DistilBERT |     | captura  | relaciones | de  | largo     | alcance | entre    |
| Los resultados |     | del modelo | entrenado  | se  | interpretan | desde |               |     |          |            |     |           |         |          |
palabrasdeltexto,loquepermiteresolverlamayoríadeestas
| dos perspectivas, |     | cuantitativa | y   | cualitativa, | siendo | este análi- |     |     |     |     |     |     |     |     |
| ----------------- | --- | ------------ | --- | ------------ | ------ | ----------- | --- | --- | --- | --- | --- | --- | --- | --- |
ambigüedadesapartirdelarepresentacióndeltoken[CLS].
| sis el insumo |           | para plantear | la dicusión    | acerca    | del           | proyecto. |               |           |              |             |                 |           |              |        |
| ------------- | --------- | ------------- | -------------- | --------- | ------------- | --------- | ------------- | --------- | ------------ | ----------- | --------------- | --------- | ------------ | ------ |
|               |           |               |                |           |               |           | Los seis      | artículos | clasificados |             | incorrectamente |           | corresponden |        |
|               |           |               |                |           |               |           | en su mayoría | a         | este tipo    | de traslape |                 | temático. |              |        |
| A. Resultados |           | cuantitativos |                |           |               |           |               |           |              |             |                 |           |              |        |
| La Tabla      | 1         | presenta      | los resultados | sobre     | el conjunto   | de        |               |           |              |             |                 |           |              |        |
|               |           |               |                |           |               |           |               |           | IV.          | DISCUSIÓN   |                 |           |              |        |
| prueba        | (334      | artículos).   | El modelo      | alcanza   | una           | exactitud |               |           |              |             |                 |           |              |        |
|               |           |               |                |           |               |           | El resultado  |           | de 98.20%    | de          | exactitud       | con       | cinco        | épocas |
| global        | de 98.20% | (328          | de 334         | artículos | correctamente |           |               |           |              |             |                 |           |              |        |
clasificados) y un F1-score macro de 0.982. de fine-tuning sobre 2225 documentos ilustra la efectividad
|     |     |     |        |     |     |     | del aprendizaje |                 | por transferencia |      | introducido  |     | por   | BERT [2] |
| --- | --- | --- | ------ | --- | --- | --- | --------------- | --------------- | ----------------- | ---- | ------------ | --- | ----- | -------- |
|     |     |     | Tabla1 |     |     |     | y GPT           | [3]. DistilBERT |                   | [5], | preentrenado |     | sobre | grandes  |
PRECISIÓN,RECALLYF1-SCOREPORCATEGORÍAENELCONJUNTODE corpusmedianteprediccióndetokensenmascarados,captura
PRUEBA. estructura sintáctica y semántica del lenguaje sin requerir
etiquetasdetarea.ElajustefinosobreelcorpusBBCorienta
| Categoría     |     | Precisión | Recall |     | F1     | Soporte |                     |         |         |          |     |               |            |          |
| ------------- | --- | --------- | ------ | --- | ------ | ------- | ------------------- | ------- | ------- | -------- | --- | ------------- | ---------- | -------- |
|               |     |           |        |     |        |         | esta representación |         | general | hacia    | la  | clasificación |            | temática |
| business      |     | 0.9737    | 0.9610 |     | 0.9673 | 77      |                     |         |         |          |     |               |            |          |
|               |     |           |        |     |        |         | en pocas            | épocas, | lo que  | confirma | el  | principio     | demostrado |          |
| entertainment |     | 0.9831    | 1.0000 |     | 0.9915 | 58      |                     |         |         |          |     |               |            |          |
politics 0.9672 0.9516 0.9593 62 también por T5 [6] y GPT-3 [7]: el costo de adaptación a
|       |     |        |        |     |        |     | un dominio | específico | se  | reduce | sustancialmente |     |     | al partir de |
| ----- | --- | ------ | ------ | --- | ------ | --- | ---------- | ---------- | --- | ------ | --------------- | --- | --- | ------------ |
| sport |     | 1.0000 | 1.0000 |     | 1.0000 | 77  |            |            |     |        |                 |     |     |              |
tech 0.9836 1.0000 0.9917 60 pesos preentrenados en texto general.
macro avg 0.9815 0.9825 0.9820 334 La arquitectura transformer [1] presenta ventajas frente a
|     |     |     |     |     |     |     | redes recurrentes |     | para texto | periodístico. |     | Su  | atención | global |
| --- | --- | --- | --- | --- | --- | --- | ----------------- | --- | ---------- | ------------- | --- | --- | -------- | ------ |
Como se observa en la Tabla 1, sport obtuvo clasificación permiterelacionareltitularconinformacióndepárrafospos-
perfecta (F1 = 1.0) y tech obtuvo recall perfecto (1.0) con teriores del artículo e integrar señales distribuidas a lo largo
precisiónde0.9836.LacategoríapoliticspresentóelF1más del documento. En el caso de politics, aunque los artículos
bajo (0.9593) con recall de 0.9516, indicando que algunos compartenvocabularioconotrascategorías,larepresentación
artículos de política se asignaron a otras categorías. contextualdeltoken[CLS]contieneseñalessuficientespara
LaFig.2muestralascurvasdepérdidayexactituddurante la clasificación correcta en el 95.16% de los casos.
el entrenamiento. La pérdida de validación desciende de Entre las limitaciones del trabajo se encuentran el tamaño
forma consistente durante las primeras épocas y se estabi- del conjunto (2225 artículos), la ausencia de una línea base
liza, lo que indica convergencia sin sobreajuste dentro del cuantitativa como clasificación sobre representaciones TF-
rango de cinco épocas. La incorporación del scheduler con IDF o DistilBERT con backbone congelado sin fine-tuning,
calentamiento y elrecorte de gradiente redujola varianza de y la falta de un estudio de ablación que aísle el efecto indi-
la pérdida entre épocas, produciendo curvas más regulares y vidual del scheduler y el recorte de gradiente. Como trabajo
un resultado final superior. futuro se propone comparar el fine-tuning completo frente
|     |     |     |     |     |     |     | a la extracción |     | de características |     | con | backbone |     | congelado, |
| --- | --- | --- | --- | --- | --- | --- | --------------- | --- | ------------------ | --- | --- | -------- | --- | ---------- |
B. Resultados cualitativos evaluarelmodeloencorpusdenoticiasdeotrasfuentespara
El modelo diferencia con mayor facilidad las categorías medir generalización entre dominios, y realizar un análisis
con vocabulario específico. Sport concentra términos de de errores por categoría que identifique los patrones léxicos
politics.
dominio deportivo —nombres de competencias, marcadores, asociados a las confusiones en

REFERENCES
| [1] A. Vaswani, |           | N. Shazeer,        | N. Parmar, J.          | Uszkoreit, | L. Jones,      | A. N. |
| --------------- | --------- | ------------------ | ---------------------- | ---------- | -------------- | ----- |
| Gomez,          | L. Kaiser | e I.               | Polosukhin, “Attention | Is         | All You Need,” | en    |
| Advances        | in        | Neural Information | Processing             | Systems    | (NeurIPS),     | vol.  |
30,2017.
[2] J.Devlin,M.-W.Chang,K.LeeyK.Toutanova,“BERT:Pre-training
ofDeepBidirectionalTransformersforLanguageUnderstanding,”en
Proc.NAACL-HLT,págs.4171–4186,2019.
| [3] A. Radford, | K.            | Narasimhan, | T. Salimans   | e I. Sutskever, | “Improving |     |
| --------------- | ------------- | ----------- | ------------- | --------------- | ---------- | --- |
| Language        | Understanding |             | by Generative | Pre-Training,”  | Technical  | Re- |
port,OpenAI,2018.
| [4] D. Greene | y   | P. Cunningham, | “Practical | Solutions | to the Problem | of  |
| ------------- | --- | -------------- | ---------- | --------- | -------------- | --- |
DiagonalDominanceinKernelDocumentClustering,”enProc.23rd
Int.Conf.MachineLearning(ICML),págs.377–384,2006.
| [5] V. Sanh, | L. Debut, | J. Chaumond | y T. Wolf, | “DistilBERT, | a   | distilled |
| ------------ | --------- | ----------- | ---------- | ------------ | --- | --------- |
versionofBERT:smaller,faster,cheaperandlighter,”arXivpreprint
arXiv:1910.01108,2019.
[6] C.Raffel,N.Shazeer,A.Roberts,K.Lee,S.Narang,M.Matena,Y.
| Zhou, | W. Li | y P. J. Liu, | “Exploring the | Limits | of Transfer | Learning |
| ----- | ----- | ------------ | -------------- | ------ | ----------- | -------- |
withaUnifiedText-to-TextTransformer,”JournalofMachineLearn-
ingResearch,vol.21,núm.140,págs.1–67,2020.
| [7] T. B. | Brown | et al., “Language  | Models     | are Few-Shot | Learners,” | en   |
| --------- | ----- | ------------------ | ---------- | ------------ | ---------- | ---- |
| Advances  | in    | Neural Information | Processing | Systems      | (NeurIPS), | vol. |
33,2020.