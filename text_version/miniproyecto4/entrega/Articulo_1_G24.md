Clasificación de Sonidos de la Naturaleza usando el Audio Spectrogram
Transformer (AST)

Jaime Rodriguez, Juan Martin Santos, Yezid Garcia — Grupo 24
Universidad de los Andes, Bogotá, Colombia
Códigos: 200717791, 202013610, 200810710
|     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
1.  Introducción  Face como confit/esc50-demo con el fold 1. El conjunto de
  La clasificación de sonidos del entorno natural tiene  entrenamiento contiene 1600 muestras y el de validación
400, con 50 clases originales. Las 50 clases se mapean a
| aplicaciones  | en  | monitoreo  | ambiental,  | conservación  | de  |     |     |     |     |
| ------------- | --- | ---------- | ----------- | ------------- | --- | --- | --- | --- | --- |
cuatro super-categorías: aves, mamíferos, agua  y viento.
biodiversidad y vigilancia ecológica. Identificar fuentes
sonoras del ambiente permite caracterizar ecosistemas de  Las muestras sin categoría asignada se descartan. La Tabla
1 muestra la distribución resultante por categoría.
manera no invasiva y a gran escala. Los métodos basados

| en  características  |     | de  | audio  | tradicionales  | presentan  |     |     |     |     |
| -------------------- | --- | --- | ------ | -------------- | ---------- | --- | --- | --- | --- |
limitaciones ante la variabilidad acústica de los sonidos  Tabla 1. Distribución de muestras por categoría tras el
| naturales.  | Por  otra  | parte,             | los  | modelos  de  | aprendizaje  | filtrado.  |                          |     |           |
| ----------- | ---------- | ------------------ | ---- | ------------ | ------------ | ---------- | ------------------------ | --- | --------- |
|             |            |                    |      |              |              | Categoría  | Clases ESC-50 incluidas  |     | Muestras  |
| profundo,   | como       | los  transformers  |      | [1],  han    | demostrado   |            |                          |     |           |
(train)
| capacidad  | para  | extraer  | representaciones  |     | de  datos  |     |     |     |     |
| ---------- | ----- | -------- | ----------------- | --- | ---------- | --- | --- | --- | --- |
secuenciales sin depender de características predefinidas.  aves  rooster, hen, chirping_birds,  128
crow
| El  mecanismo  |          | de  auto-atención  |      |   de          | Transformers  |       |                   |     |      |
| -------------- | -------- | ------------------ | ---- | ------------- | ------------- | ----- | ----------------- | --- | ---- |
|                |          |                    |      |               |               | agua  | rain, sea_waves,  |     | 160  |
| propuesto      | en  [1]  | permite            | que  | los  modelos  | capturen      |       |                   |     |      |
relaciones entre todos los elementos de una secuencia en  water_drops, pouring_water,
thunderstorm
una sola operación, lo que resulta adecuado para el análisis
|                       |     |     |         |            |              | mamiferos  | dog, pig, cow, cat, frog,  |     | 192  |
| --------------------- | --- | --- | ------- | ---------- | ------------ | ---------- | -------------------------- | --- | ---- |
| de  representaciones  |     | de  | audio.  | El  Audio  | Spectrogram  |            |                            |     |      |
Transformer (AST) [2] adapta esta arquitectura al dominio  sheep
acústico: convierte señales de audio en espectrogramas  viento  wind  32
Cada grabación se remuestrea a 16 kHz si es necesario.
MEL. AST superó a los enfoques convolucionales en
múltiples benchmarks de clasificación de audio. El dataset  El  extractor  AST  genera  un  espectrograma  MEL
ESC-50  [3]  es  una  colección  de  referencia  con  2000  normalizado y de tamaño fijo, asegurando consistencia
entre muestras.
grabaciones en 50 categorías de sonidos de ambiente,
| ampliamente usada para evaluar modelos de clasificación  |     |     |     |     |     |                             |                                               |     |     |
| -------------------------------------------------------- | --- | --- | --- | --- | --- | --------------------------- | --------------------------------------------- | --- | --- |
| acústica.                                                |     |     |     |     |     | C. Arquitectura del modelo  |                                               |     |     |
|                                                          |     |     |     |     |     | Se  usa                     | el  modelo  MIT/ast-finetuned-audioset-10-10- |     |     |
El objetivo de este trabajo es adaptar el modelo AST
0.4593 [2], preentrenado en AudioSet con 527 clases y
preentrenado en AudioSet para clasificar sonidos naturales
en cuatro categorías: aves, agua, viento y mamíferos. Se  aproximadamente 86 millones de parámetros. La capa de
realiza  fine-tuning  del  modelo  MIT/ast-finetuned- clasificación final (con 527 salidas) se reemplaza por una
capa lineal con 4 salidas, una por cada categoría del
audioset-10-10-0.4593 sobre un subconjunto del dataset
ESC-50. El modelo se evalúa mediante precisión, recall y  proyecto. El resto de los pesos preentrenados se conservan
F1-score por categoría, y se analiza la matriz de confusión  para el fine-tuning.

para identificar los patrones de error entre clases.
D. Entrenamiento y métricas
2.  Metodología  El  modelo  se  entrena  durante  2  épocas  con  el
optimizador AdamW, tasa de aprendizaje 1×10⁻⁴ y tamaño
A  continuación  se  describen  los  componentes  de lote de 8 muestras. La función de pérdida es la entropía
principales utilizados en el desarrollo del presente trabajo.
|     |     |     |     |     |     | cruzada.  | Se  reportan  precisión,  | recall  | y  F1-score  por  |
| --- | --- | --- | --- | --- | --- | --------- | ------------------------- | ------- | ----------------- |

categoría, métricas estándar para clasificación multiclase
A. Pipeline general  que  permiten  evaluar  el  desempeño  de  forma
Comprende cuatro etapas: (1) carga y filtrado del dataset
independiente por clase. La exactitud global (accuracy)
| a  las  cuatro  | categorías  |     | de  interés,  | (2)  | extracción  de  |     |     |     |     |
| --------------- | ----------- | --- | ------------- | ---- | --------------- | --- | --- | --- | --- |
complementa el análisis al igual que la matriz de confusión
características acústicas mediante el ASTFeatureExtractor,  permitiendo identificar qué pares de categorías el modelo
(3) fine-tuning del modelo AST, y (4) evaluación sobre el
confunde con mayor frecuencia.
conjunto de validación.
|     |     |     |     |     |     | 3.  | Resultados  |     |     |
| --- | --- | --- | --- | --- | --- | --- | ----------- | --- | --- |
B. Dataset y preprocesamiento
Se usa el dataset ESC-50 [3], cargado desde Hugging  Los resultados del modelo entrenado se interpretan desde

dos perspectivas, cuantitativa y cualitativa:  presentan mayor cantidad de muestras de entrenamiento, lo
|     |     |     |     |     | que influye en el desempeño del modelo. La categoría  |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | ----------------------------------------------------- | --- | --- | --- | --- | --- | --- |
A. Resultados cuantitativos  viento, con una sola clase ESC-50 mapeada, cuenta con el
|     |     |     |     |     | menor número de muestras y menor desempeño.  |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | -------------------------------------------- | --- | --- | --- | --- | --- | --- |

B. Resultados cualitativos

Fig 3. Ejemplos de espectrogramas MEL.

|     |     |     |     |     | La  Fig.  | 3  presenta  |     | ejemplos  | de  espectrogramas  |     | del  |
| --- | --- | --- | --- | --- | --------- | ------------ | --- | --------- | ------------------- | --- | ---- |
conjunto de validación con la etiqueta real y la predicción
del modelo. Los ejemplos de predicción correcta muestran
que el modelo identifica con consistencia los patrones
|     |     |     |     |     | espectrales  | característicos  |     | de  cada  | categoría:  |     | las  aves  |
| --- | --- | --- | --- | --- | ------------ | ---------------- | --- | --------- | ----------- | --- | ---------- |
Fig 1. Curva de pérdida (entropía cruzada) por época.
presentan componentes de alta frecuencia con variaciones

temporales rítmicas; los sonidos de agua exhiben energía
La Fig. 1 muestra la curva de pérdida promedio por
distribuida en bandas de frecuencia amplias; el viento
época durante el entrenamiento en donde se ve una mejora
presenta energía predominante en frecuencias bajas con
notable así como  la ausencia de más épocas.
poca estructura temporal.

Tabla 2. Métricas de clasificación.
4.  Discusión
| Categoría  | Precisión  | Recall  | F1-score  |     |     |     |     |     |     |     |     |
| ---------- | ---------- | ------- | --------- | --- | --- | --- | --- | --- | --- | --- | --- |
Agua  0.91  1  0.95  El  modelo  AST  muestra  capacidad  de  transferencia
Aves  1  0.94  0.97  desde AudioSet hacia la clasificación de sonidos naturales.
Mamiferos  0.96  1  0.98  La arquitectura de auto-atención [1], preentrenada en un
Viento  1  0.50  0.67  corpus de audio de gran escala, captura representaciones
espectrales reutilizables para tareas de clasificación en
| promedio  | 0.96  | 0.95  | 0.95  |     |     |     |     |     |     |     |     |
| --------- | ----- | ----- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
ponderado  dominios relacionados. Este resultado es consistente con la
La Tabla 2 presenta las métricas de clasificación por  observación  en  [2]  de  que  el  pre-entrenamiento  en
AudioSet generaliza a otras tareas acústicas.
categoría, al tiempo que la Fig. 2 presenta la matriz de
confusión sobre el conjunto de validación.  Las  diferencias  de  desempeño  entre  categorías  se
  explican en parte por el desbalance en el número de clases
|     |     |     |     |     | ESC-50     | mapeadas:            | mamíferos  |                   | tiene       | seis  clases  | (192   |
| --- | --- | --- | --- | --- | ---------- | -------------------- | ---------- | ----------------- | ----------- | ------------- | ------ |
|     |     |     |     |     | muestras   | de  entrenamiento),  |            | agua              | tiene       | cinco         | (160   |
|     |     |     |     |     | muestras)  | y  aves              | cuatro     | (128  muestras),  |             | mientras que  |        |
|     |     |     |     |     | viento     | tiene  una           | sola       | (32               | muestras).  | La            | menor  |
representación de viento limita la capacidad del modelo
|     |     |     |     |     | para  aprender  | variantes  |     | intra-clase.  | Por  | otro  | lado,  la  |
| --- | --- | --- | --- | --- | --------------- | ---------- | --- | ------------- | ---- | ----- | ---------- |
similitud espectral entre vocalizaciones de aves y algunos
sonidos de mamíferos puede generar confusión entre estas
categorías.
A pesar de los buenos resultados, las limitaciones del
presente trabajo incluyen: el número reducido de épocas de
entrenamiento (2), el desbalance en el número de muestras
por super-categoría, y la ausencia de técnicas de aumento
de datos. Incrementar las épocas de entrenamiento, aplicar

Fig 2. Matriz de confusión del modelo en el conjunto de  congelamiento parcial del encoder durante las primeras
validación.
épocas, o balancear las super-categorías podría mejorar el
|               |                 |                     |     |           | desempeño del modelo en una futura versión.  |     |     |     |     |     |     |
| ------------- | --------------- | ------------------- | --- | --------- | -------------------------------------------- | --- | --- | --- | --- | --- | --- |
| El  análisis  | por  categoría  | (Fig.  2)  muestra  |     | que  las  |                                              |     |     |     |     |     |     |
categorías con mayor variedad de clases ESC-50 mapeadas

5. Referencias
[1] [1] A. Vaswani, N. Shazeer, N. Parmar, J. Uszkoreit, L.
Jones, A. N. Gomez, L. Kaiser, and I. Polosukhin, "Attention
is all you need," in Advances in Neural Information
Processing Systems (NeurIPS), vol. 30, 2017.
[2] [2] Y. Gong, Y.-A. Chung, and J. R. Glass, "AST: Audio
Spectrogram Transformer," in Proc. Interspeech 2021, pp.
571–575, 2021. [Online]. Available:
https://arxiv.org/abs/2104.01778
[3] [3] K. J. Piczak, "ESC: Dataset for Environmental Sound
Classification," in Proc. 23rd ACM International Conference
on Multimedia (ACM MM), pp. 1015–1018, 2015.