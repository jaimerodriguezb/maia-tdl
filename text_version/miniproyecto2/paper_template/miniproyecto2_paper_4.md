Clasificación de Sentimientos de Reseñas de Películas en IMDb
con Redes Neuronales Recurrentes

Yezid Garcia∗, Juan Martin Santos∗, Jaime Rodriguez∗
∗Grupo 24. Códigos: 200810710, 202013610, 200717791

I. INTRODUCCIÓN

El análisis de sentimiento es una tarea del procesamiento
de lenguaje natural que determina la polaridad emocional
de un texto. En el contexto de reseñas de películas, el
identificar si
problema se reduce a clasificación binaria:
una reseña expresa una opinión positiva o negativa. Su
aplicación permite caracterizar la opinión del público de
forma automática, con utilidad en sistemas de recomendación
y monitoreo de reputación.

Los enfoques clásicos basados en frecuencia de términos
ignoran el orden de las palabras y pierden información
contextual. Las redes con celdas de memoria a largo y
corto plazo (LSTM) [1] superan esta limitación al procesar
secuencias de tokens y capturar dependencias entre pal-
abras distantes. La variante bidireccional (BiLSTM) combina
estados ocultos en ambas direcciones, proporcionando a
cada posición acceso al contexto anterior y posterior. Las
representaciones distribucionales de palabras [2] codifican
similitud semántica en vectores densos entrenados sobre
grandes corpus; inicializar un modelo con vectores preen-
trenados como GloVe [3] mejora la generalización cuando
el conjunto de entrenamiento es de tamaño moderado.

Este trabajo presenta la implementación y evaluación de un
modelo BiLSTM con embeddings GloVe para la clasificación
binaria de reseñas del conjunto IMDb [4]. Se describe el
pipeline de preprocesamiento, la arquitectura del modelo,
la estrategia de entrenamiento y los resultados obtenidos en
términos de precisión, recall y F1-score.

II. METODOLOGÍA

El conjunto de datos contiene 40 000 reseñas de IMDb [4]
con etiqueta binaria de sentimiento, balanceado en 20 000
muestras por clase y sin valores nulos. La partición es
estratificada: 80 % para entrenamiento (32 000 muestras),
10 % para validación (4 000) y 10 % para prueba (4 000).

Cada reseña pasa por un pipeline de preprocesamiento de
cinco pasos: eliminación de etiquetas HTML; descarte de
caracteres no alfabéticos; conversión a minúsculas; elimi-
nación de palabras funcionales en inglés; y lematización, que
reduce cada token a su forma canónica (por ejemplo, running
a run). Los tokens resultantes se convierten a índices enteros
usando un vocabulario construido exclusivamente sobre el
conjunto de entrenamiento, y las secuencias se rellenan o
truncan a 300 tokens.

Los embeddings se inicializan con vectores GloVe de
100 dimensiones [3]; la cobertura sobre el vocabulario del
conjunto es del 77.2 %. Siguiendo la estrategia de ajuste

progresivo propuesta en [5], los embeddings se congelan du-
rante las tres primeras épocas para que las capas recurrentes
converjan sin distorsionar las representaciones preentrenadas.
A partir de la cuarta época, se descongelan con una tasa de
aprendizaje diez veces menor para realizar un ajuste fino
controlado.

El modelo, denominado SentimentBiLSTM, combina cu-
atro etapas descritas en la Tabla 1. Una capa BiLSTM de
128 unidades por dirección procesa la secuencia en ambos
sentidos; luego un promedio sobre todos los estados ocultos
(mean pooling) produce una representación de longitud fija.
Esta operación, validada en [6], es superior al uso del último
estado oculto para secuencias largas donde el sentimiento
está distribuido a lo largo del texto. Una capa lineal con
activación sigmoide clasifica en positivo o negativo.

Tabla 1.
CAPAS DEL MODELO SentimentBiLSTM.

Capa

Dimensión de salida

Parámetros

B × 300 × 100
Embedding GloVe 100d
B × 300 × 100
Abandono (p = 0.3)
BiLSTM (128 ud., 1 capa) B × 300 × 256
Mean Pooling
Abandono (p = 0.3)
Lineal + Sigmoide

B × 256
B × 256
B × 1

Total

7,449,500
0
267,264
0
0
257

7,685,277

El entrenamiento usa el optimizador Adam con tasa de
aprendizaje inicial de 10−3 y pérdida de entropía cruzada
binaria, con lotes de 128 muestras. Se incorporan tres
mecanismos de control: un planificador que reduce la tasa
de aprendizaje a la mitad si la pérdida de validación no
mejora en dos épocas consecutivas; limitación de la norma
del gradiente a 1.0, que [7] identifica como crítico para
estabilizar LSTM en secuencias largas; y parada anticipada
con paciencia de cinco épocas. Las métricas de evaluación
son precisión, recall y F1-score.

III. RESULTADOS

A. Resultados cuantitativos

Se entrenó el modelo durante un máximo de 20 épocas; la
parada anticipada se activó en la época 19. La Fig. 1 muestra
la evolución de la pérdida y las métricas de validación a lo
largo del entrenamiento.

La Tabla 2 compara las métricas en tres momentos clave
para mostrar el efecto de la estrategia de ajuste progresivo:
al terminar la fase de congelado (ép. 3), al inicio del ajuste

más robustas que el último estado oculto en reseñas largas
donde el sentimiento está distribuido a lo largo del texto,
lo que explica la estabilidad de las métricas en las épocas
finales.

La estrategia de congelar y luego descongelar los embed-
dings es efectiva: la Tabla 2 muestra una ganancia de 2.7
puntos de F1 entre la época 3 y la época 6, en línea con
los resultados de [2] al comparar estrategias de embeddings
estáticos y ajustables. El ajuste fino con tasa de aprendizaje
reducida evita destruir las representaciones preentrenadas
mientras el modelo captura patrones específicos del dominio.
La cobertura del 77.2 % de GloVe sobre el vocabulario
del conjunto es suficiente para que los embeddings aporten
información semántica útil desde las primeras épocas.

Como limitaciones, el número de épocas de congelado
es fijo, por lo que un criterio adaptativo podría ajustarse
mejor según la velocidad de convergencia de cada ejecución.
Las reseñas con más de 300 tokens se truncan, perdiendo el
contexto del final del texto, que en críticas de cine frecuente-
mente contiene la valoración final del autor. Tampoco se
realizó búsqueda sistemática de hiperparámetros, por lo que
la configuración actual puede no ser óptima. Como trabajo
futuro, resulta de interés explorar mecanismos de atención
sobre los estados del BiLSTM como alternativa al mean
pooling, comparar el rendimiento con un codificador Trans-
former ligero y evaluar el impacto de distintas duraciones de
la fase de congelado.

Fig. 1. Pérdida BCE (izq.) y métricas de validación (der.) por época. La
parada anticipada se activa en la época 19.

fino (ép. 6) y al final del entrenamiento (ép. 19). La Tabla 3
reporta los resultados sobre el conjunto de prueba.

Tabla 2.
EVOLUCIÓN DE MÉTRICAS EN VALIDACIÓN POR FASE.

Fase

Precisión

Recall

F1

Ép. 3 — embeddings congelados
Ép. 6 — inicio ajuste fino
Ép. 11 — convergencia
Ép. 19 — parada anticipada

0.811
0.848
0.889
0.890

0.895
0.909
0.894
0.909

0.851
0.878
0.892
0.899

Tabla 3.
MÉTRICAS FINALES SOBRE EL CONJUNTO DE PRUEBA.

Métrica

Valor

Precisión
Recall
F1-Score

0.877
0.910
0.893

B. Resultados cualitativos

El recall supera sistemáticamente a la precisión tanto en
validación como en prueba (0.910 frente a 0.877), lo que
indica una tendencia del modelo a clasificar como positivo
ante la ambigüedad. Esto es consistente con el sesgo de los
vectores GloVe: intensificadores frecuentes en reseñas como
amazing o terrible tienen carga emocional pronunciada que
el modelo asocia con la clase positiva incluso en contextos
negativos. El efecto persiste tras el ajuste fino.

La convergencia es rápida en las primeras seis épocas,
donde el F1 pasa de 0.792 a 0.878; las épocas siguientes
aportan mejoras marginales. La brecha creciente entre pér-
dida de entrenamiento y validación a partir de la época
11 señala sobreajuste moderado que la parada anticipada
contiene pero no elimina.

IV. DISCUSIÓN

El F1 de 0.893 es consistente con los rangos reportados
en trabajos sobre IMDb con arquitecturas recurrentes [5].
El resultado se ubica en el rango esperado para una sola
capa BiLSTM, ya que [7] muestra que arquitecturas más
profundas no siempre mejoran el rendimiento en tareas
de clasificación de longitud moderada y pueden introducir
inestabilidad en el entrenamiento. El mean pooling sobre los
estados ocultos, respaldado por [6], produce representaciones

REFERENCES

[1] S. Hochreiter and J. Schmidhuber, “Long short-term memory,” Neural

Computation, vol. 9, no. 8, pp. 1735–1780, 1997.

[2] Y. Kim, “Convolutional neural networks for sentence classification,”

in Proc. EMNLP, pp. 1746–1751, 2014.

[3] J. Pennington, R. Socher, and C. D. Manning, “GloVe: Global vectors
for word representation,” in Proc. EMNLP, pp. 1532–1543, 2014.
[4] A. L. Maas, R. E. Daly, P. T. Pham, D. Huang, A. Y. Ng, and C. Potts,
“Learning word vectors for sentiment analysis,” in Proc. 49th Annual
Meeting of the ACL, pp. 142–150, 2011.

[5] J. Howard and S. Ruder, “Universal language model fine-tuning for

text classification,” in Proc. ACL, pp. 328–339, 2018.

[6] A. Conneau, D. Kiela, H. Schwenk, L. Barrault, and A. Bordes, “Su-
pervised learning of universal sentence representations from natural
language inference data,” in Proc. EMNLP, pp. 670–680, 2017.
[7] K. Greff, R. K. Srivastava, J. Kout´nik, B. R. Steunebrink, and
J. Schmidhuber, “LSTM: A search space odyssey,” IEEE Trans. Neural
Netw. Learn. Syst., vol. 28, no. 10, pp. 2222–2232, 2017.

[8] T. Mikolov, K. Chen, G. Corrado, and J. Dean, “Efficient estimation of
word representations in vector space,” arXiv preprint arXiv:1301.3781,
2013.

