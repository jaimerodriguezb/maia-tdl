1.  Introducción
El  diagnóstico  temprano  y  preciso  de  tumores  Las imágenes fueron redimensionadas a 128×128 píxeles
|             |                                            |                                    |     | y  convertidas            | a  tensores                   | PyTorch  | con  |
| ----------- | ------------------------------------------ | ---------------------------------- | --- | ------------------------- | ----------------------------- | -------- | ---- |
| cerebrales  | es  uno  de                                | los  desafíos  más críticos en la  |     |                           |                               |          |      |
|             |                                            |                                    |     | `transforms.ToTensor()`,  | normalizando automáticamente  |          |      |
| medicina    | moderna. Las resonancias magnéticas (MRI)  |                                    |     |                           |                               |          |      |
constituyen la herramienta principal para su detección,  los valores al rango [0, 1]. No se aplicó data augmentation
pero su interpretación manual por parte de radiólogos es  en  esta  versión.  La  carga  se  realizó  con
|     |     |     |     | `torchvision.datasets.ImageFolder`  |     | y  la  división  | con  |
| --- | --- | --- | --- | ----------------------------------- | --- | ---------------- | ---- |
costosa en tiempo y susceptible a variabilidad humana. En
este contexto, el Deep Learning ha emergido como una  `random_split`  estratificado  con semilla fija (42) para
| alternativa  | prometedora,  | alcanzando  | precisiones  | reproducibilidad.  |     |     |     |
| ------------ | ------------- | ----------- | ------------ | ------------------ | --- | --- | --- |

comparables a especialistas en tareas de clasificación de
El modelo `BrainTumorCNN` implementa la arquitectura
imágenes médicas (Litjens et al., 2017).
|     |     |     |     | de bloques convolucionales descrita en la Tabla 2.Donde  |     |     |     |
| --- | --- | --- | --- | -------------------------------------------------------- | --- | --- | --- |
cada bloque sigue el patrón:
| Las  | redes  neuronales  | convolucionales  | (CNNs)  han  |     |     |     |     |
| ---- | ------------------ | ---------------- | ------------ | --- | --- | --- | --- |

demostrado ser especialmente efectivas para el análisis de
imágenes médicas, gracias a su capacidad de aprender  Conv2d → BatchNorm2d → ReLU →
automáticamente representaciones jerárquicas de features  Conv2d → ReLU →
MaxPool2d(2×2) → Dropout2d(0.25).
visuales — desde bordes y texturas en capas tempranas,
| hasta  | estructuras  anatómicas  | complejas  | en  capas  |     |     |     |     |
| ------ | ------------------------ | ---------- | ---------- | --- | --- | --- | --- |
profundas.  Sin  embargo,  la  generalización  de  estos  Tabla 2. Bloques convolucionales.
modelos sigue siendo un reto, particularmente cuando se
trabaja con datasets pequeños y clases con alta similitud
| visual,  | como  ocurre  | con  distintos  tipos  | de  tumores  |     |     |     |     |
| -------- | ------------- | ---------------------- | ------------ | --- | --- | --- | --- |
cerebrales.

2.  Metodología

Se  implementó  una  CNN  personalizada  con  La progresión 32→64→128 filtros sigue el principio de
arquitectura de tres bloques convolucionales seguida de  jerarquía de features: las capas iniciales aprenden features
capas  densas  de  clasificación,  usando  PyTorch  como  simples (bordes, texturas) con pocos filtros, mientras las
|            |             |                                     |     | capas  profundas  | aprenden  | representaciones  | más  |
| ---------- | ----------- | ----------------------------------- | --- | ----------------- | --------- | ----------------- | ---- |
| framework  | principal.  | El  flujo  del  trabajo comprende:  |     |                   |           |                   |      |
carga y preprocesamiento del dataset, definición de la  complejas  que  requieren  mayor  capacidad.  Cada
arquitectura,  configuración  del  entrenamiento  con  MaxPool2d  reduce  la  resolución  espacial  a la mitad,
compensada con el incremento en filtros para preservar la
regularización adaptativa, y evaluación mediante métricas
estándar de clasificación multiclase.  capacidad representacional.
|     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
El entrenamiento del modelo se realizó utilizando los
El dataset utilizado fue Brain Tumor MRI Scan de
Kaggle,  el  cual  contiene  un  total  de  7023 imágenes  siguientes hiperparametros:
| distribuidos en 4 categorias balanceadas.    |     |     |     |                                           |     |     |     |
| -------------------------------------------- | --- | --- | --- | ----------------------------------------- | --- | --- | --- |
|                                              |     |     |     | Tabla 3. Hperparámetros de entranmiento.  |     |     |     |
Tabla 1. Categorías en que se pueden clasificar las imágenes
MRI.

|     |     |     |     | Se  empleó  | ReduceLROnPlateau  | para  | reducir  |
| --- | --- | --- | --- | ----------- | ------------------ | ----- | -------- |

automáticamente el learning rate cuando la pérdida de  de error por clase. Las mayores confusiones ocurren entre
validación deja de mejorar, y early stopping manual para  glioma y meningioma, lo que es entendible ya que ambos
restaurar  los  pesos  del  mejor  epoch  al  finalizar  el  son  tumores  con  apariencias  en  MRI  visualmente
entrenamiento.  similares. Adicionalmente, la clase healthy típicamente
|                 |     |     |     |     |     | presenta                  | la  menor  | tasa  de  | error  por  | su  | morfología  |     |
| --------------- | --- | --- | --- | --- | --- | ------------------------- | ---------- | --------- | ----------- | --- | ----------- | --- |
| 3.  Resultados  |     |     |     |     |     | claramente diferenciada.  |            |           |             |     |             |     |

El modelo se entrenó durante las 20 épocas completas,
Tabla 4. Reporte de clasificación detallado.
mostrando convergencia progresiva y consistente.

Tabla 3.Evolución de métricas durante el entrenamiento.

Las cuatro clases obtuvieron métricas competitivas, con
F1-scores superiores al 93% en todas las categorías, lo
|     |     |     |     |     |     | que  demuestra  | que    | el  modelo      | no        | está sesgado hacia  |               |     |
| --- | --- | --- | --- | --- | --- | --------------- | ------ | --------------- | --------- | ------------------- | ------------- | --- |
|     |     |     |     |     |     | ninguna         | clase  | en  particular  | a  pesar  |                     | de  posibles  |     |
La precisión de validación supera a la de entrenamiento  desequilibrios en el dataset original.
| en  las  primeras  | épocas  | (epochs  | 1-3),  lo  que  | es  | un  |     |     |     |     |     |     |     |
| ------------------ | ------- | -------- | --------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
indicador de que el Dropout está activo y regularizando
| correctamente durante el entrenamiento.  |     |     |     |     |     | 4.  | Discusión  |     |     |     |     |     |
| ---------------------------------------- | --- | --- | --- | --- | --- | --- | ---------- | --- | --- | --- | --- | --- |
A partir de la época 10, ambas curvas convergen y la
El modelo alcanzó una precisión del 95.44% en el
| brecha  train/val  |        | se  mantiene    | pequeña      | (~1%),  |     |               |              |            |              |       |                |     |
| ------------------ | ------ | --------------- | ------------ | ------- | --- | ------------- | ------------ | ---------- | ------------ | ----- | -------------- | --- |
|                    |        |                 |              |         |     | conjunto      | de  prueba,  | resultado  | competitivo  |       | para           | un  |
| evidenciando       | buena  | generalización  | y  ausencia  |         | de  |               |              |            |              |       |                |     |
|                    |        |                 |              |         |     | clasificador  | CNN          | entrenado  | desde        | cero  | sin  transfer  |     |
sobreajuste severo.
|     |     |     |     |     |     | learning.  | La  brecha  | mínima  | entre  | la  | precisión  | de  |
| --- | --- | --- | --- | --- | --- | ---------- | ----------- | ------- | ------ | --- | ---------- | --- |
El learning rate se mantuvo constante en 1e-3 durante
validación (96.01%) y la de prueba (95.44%) confirma
| todo  el  entrenamiento,  |     | indicando  | que  la  pérdida  |     | de  |     |     |     |     |     |     |     |
| ------------------------- | --- | ---------- | ----------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
que el modelo generaliza bien a datos no vistos durante el
| validación  | mejoró  consistentemente y el scheduler no  |     |     |     |     |     |     |     |     |     |     |     |
| ----------- | ------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
entrenamiento.
tuvo necesidad de reducirlo.

La efectividad del enfoque se atribuye en gran parte a
la combinación de BatchNorm y Dropout: el primero
estabiliza el entrenamiento al normalizar las activaciones
de cada capa, acelerando la convergencia y reduciendo la
sensibilidad al learning rate inicial; el segundo fuerza al
modelo a aprender representaciones robustas al apagar
aleatoriamente neuronas durante el entrenamiento.

A pesar de los buenos resultados, es importante resaltar
que existieron limitaciones como: el tamaño del dataset es
relativamente pequeño para un entrenamiento desde cero,
se seleccionó una resolución de 128x128 para facilitar el
|     |     |     |     |     |     | entrenamiento  | pero        | perdiendo  | detalles   | finos             |     | de  las  |
| --- | --- | --- | --- | --- | --- | -------------- | ----------- | ---------- | ---------- | ----------------- | --- | -------- |
|     |     |     |     |     |     | imágenes       | originales  | y  el      | hecho  de  | que no se aplicó  |     |          |
ninguna técnica de data augmentation como rotaciones,
flips o cambios en el brillo y/o contraste de la imagen.
Los aspectos anteriores podrían considerarse como trabajo
|     |     |     |     |     |     | futuro para una nueva iteración del presente proyecto.  |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | ------------------------------------------------------- | --- | --- | --- | --- | --- | --- |
Fig 1. Matriz de confusión.

La matriz de confusión permite identificar los patrones

Referencias
[1] Litjens, G., et al. (2017). A survey on deep learning in
medical image analysis. Medical Image Analysis, 42,
60–88.
[2]
[3] Cheng, J., et al. (2015). Enhanced Performance of Brain
Tumor Classification via Tumor Region Augmentation and
Partition. PLOS ONE, 10(10).
[4] He, K., Zhang, X., Ren, S., & Sun, J. (2016). Deep
Residual Learning for Image Recognition. CVPR 2016.
[5] Ioffe, S., & Szegedy, C. (2015). Batch Normalization:
Accelerating Deep Network Training by Reducing Internal
Covariate Shift. ICML 2015.
[6] Paszke, A., et al. (2019). PyTorch: An Imperative Style,
High-Performance Deep Learning Library. NeurIPS 2019.