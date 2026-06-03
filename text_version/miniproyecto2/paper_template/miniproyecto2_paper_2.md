|     |     | Clasificación |     |     | de   | Sentimiento   |       | en Reseñas |            |     | de Películas |       |     |     |     |
| --- | --- | ------------- | --- | --- | ---- | ------------- | ----- | ---------- | ---------- | --- | ------------ | ----- | --- | --- | --- |
|     |     | con           | Red |     | LSTM | Bidireccional |       | y          | Embeddings |     |              | GloVe |     |     |     |
|     |     |               |     |     |      |               | Jaime | Rodriguez  |            |     |              |       |     |     |     |
Abstract—Se entrena un modelo de red neuronal re- II. METODOLOGÍA
| currente | bidireccional |     | (BiLSTM)     |     | para        | clasificar | el sen-    |             |     |       |     |     |     |     |     |
| -------- | ------------- | --- | ------------ | --- | ----------- | ---------- | ---------- | ----------- | --- | ----- | --- | --- | --- | --- | --- |
|          |               |     |              |     |             |            |            | A. Conjunto | de  | datos |     |     |     |     |     |
| timiento | de reseñas    |     | de películas |     | en positivo | (1)        | o negativo |             |     |       |     |     |     |     |     |
(0). El pipeline de preprocesamiento aplica eliminación de Elconjuntocontiene40000reseñasdeIMDB[3]coneti-
| HTML,       | filtrado           | de caracteres, |     | stopwords  |          | NLTK       | y lemati-   |                |       |              |               |                 |        |                |          |
| ----------- | ------------------ | -------------- | --- | ---------- | -------- | ---------- | ----------- | -------------- | ----- | ------------ | ------------- | --------------- | ------ | -------------- | -------- |
|             |                    |                |     |            |          |            |             | queta binaria  | de    | sentimiento. |               | La distribución |        | es balanceada: |          |
| zación con  | WordNetLemmatizer. |                |     |            | Los      | embeddings | se ini-     |                |       |              |               |                 |        |                |          |
|             |                    |                |     |            |          |            |             | 20000 muestras |       | positivas    | y 20000       | negativas.      |        | No se          | encon-   |
| cializan    | con GloVe-100d     |                | y   | se ajustan | mediante |            | fine-tuning |                |       |              |               |                 |        |                |          |
|             |                    |                |     |            |          |            |             | traron valores | nulos | ni           | filas vacías, | por             | lo que | no se          | requirió |
| progresivo. | El                 | entrenamiento  |     | usa        | parada   | anticipada | sobre       |                |       |              |               |                 |        |                |          |
| val_loss,   | ReduceLROnPlateau  |                |     | y          | gradient | clipping.  | Se re-      | imputación.    |       |              |               |                 |        |                |          |
portan precisión, recall y F1-score sobre un conjunto de La división es estratificada por clase:
| prueba | de 4000 | muestras. |     | El código | está | implementado | en  |                  |     |     |        |           |     |     |     |
| ------ | ------- | --------- | --- | --------- | ---- | ------------ | --- | ---------------- | --- | --- | ------ | --------- | --- | --- | --- |
|        |         |           |     |           |      |              |     | • Entrenamiento: |     | 80% | (32000 | muestras) |     |     |     |
miniproyecto2_draft_2.ipynb.
|     |     |     |     |     |     |     |     | Validación: |     | 10% (4000 |     | muestras) |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------- | --- | --------- | --- | --------- | --- | --- | --- |
•
|             |     |             |              |        |       |                   |     | • Prueba:           | 10%  | (4000    | muestras)    |           |         |         |     |
| ----------- | --- | ----------- | ------------ | ------ | ----- | ----------------- | --- | ------------------- | ---- | -------- | ------------ | --------- | ------- | ------- | --- |
|             |     | I.          | INTRODUCCIÓN |        |       |                   |     | B. Preprocesamiento |      |          |              |           |         |         |     |
|             |     |             |              |        |       |                   |     | Cada reseña         | pasa | por      | el siguiente | pipeline: |         |         |     |
| El análisis | de  | sentimiento |              | es una | tarea | del procesamiento |     |                     |      |          |              |           |         |         |     |
|             |     |             |              |        |       |                   |     | 1) Eliminación      |      | de HTML: |              | expresión | regular | <[^>]+> |     |
dellenguajenatural(NLP)quebuscadeterminarlapolaridad elimina etiquetas como <br /> y <b>.
| de un texto. | Se  | aplica | en sistemas |     | de recomendación, |     | mon- |              |     |              |     |             |      |         |     |
| ------------ | --- | ------ | ----------- | --- | ----------------- | --- | ---- | ------------ | --- | ------------ | --- | ----------- | ---- | ------- | --- |
|              |     |        |             |     |                   |     |      | 2) Filtrado: |     | se conservan |     | solo letras | A–Z; | números | y   |
itoreo de redes sociales y análisis de mercado. En reseñas puntuación se descartan.
| de películas | el          | problema | se  | reduce | a clasificación |     | binaria: |                |     |               |     |          |             |           |     |
| ------------ | ----------- | -------- | --- | ------ | --------------- | --- | -------- | -------------- | --- | ------------- | --- | -------- | ----------- | --------- | --- |
|              |             |          |     |        |                 |     |          | 3) Minúsculas: |     | normalización |     | de       | mayúsculas. |           |     |
| positivo     | o negativo. |          |     |        |                 |     |          |                |     |               |     |          |             |           |     |
|              |             |          |     |        |                 |     |          | 4) Stopwords:  |     | se eliminan   |     | palabras | sin carga   | semántica |     |
Los modelos clásicos de bolsa de palabras (bag-of-words) usando la lista del inglés de NLTK.
representan el texto como un vector de frecuencias de 5) Lematización: WordNetLemmatizer reduce cada
términos. Este enfoque ignora el orden de las palabras y token a su forma base (running → run, dogs → dog).
| pierde información |       | sobre    | el  | contexto.  | Las | redes  | neuronales |          |           |     |         |     |         |           |     |
| ------------------ | ----- | -------- | --- | ---------- | --- | ------ | ---------- | -------- | --------- | --- | ------- | --- | ------- | --------- | --- |
|                    |       |          |     |            |     |        |            | La Tabla | I muestra | un  | ejemplo | de  | entrada | y salida. |     |
| recurrentes        | (RNN) | procesan |     | secuencias | de  | tokens | y pueden   |          |           |     |         |     |         |           |     |
capturar dependencias entre palabras distantes. Las celdas TABLEI
EJEMPLODEPREPROCESAMIENTO.
| de memoria  | a   | corto     | y largo    | plazo         | (LSTM) | [1]     | resuelven    |       |       |     |     |     |     |     |     |
| ----------- | --- | --------- | ---------- | ------------- | ------ | ------- | ------------ | ----- | ----- | --- | --- | --- | --- | --- | --- |
| el problema | del | gradiente |            | desvaneciente |        | que     | afecta a las |       |       |     |     |     |     |     |     |
| RNN simples |     | mediante  | compuertas |               | que    | regulan | el flujo de  | Etapa | Texto |     |     |     |     |     |     |
información a lo largo de la secuencia. Entrada “A waste of film. Utter rubbish.<br/>Frakes
La variante bidireccional (BiLSTM) procesa la secuencia should hand in his directors chair!”
|             |          |                    |             |     |          |                    |          | Salida | [’waste’,   |     | ’film’,  | ’utter’, |         |     |     |
| ----------- | -------- | ------------------ | ----------- | --- | -------- | ------------------ | -------- | ------ | ----------- | --- | -------- | -------- | ------- | --- | --- |
| en ambos    | sentidos | (izquierda–derecha |             |     | y        | derecha–izquierda) |          |        |             |     |          |          |         |     |     |
|             |          |                    |             |     |          |                    |          |        | ’rubbish’,  |     | ’frake’, |          | ’hand’, |     |     |
| y concatena | los      | estados            | ocultos.    |     | Esto     | permite            | que cada |        |             |     |          |          |         |     |     |
|             |          |                    |             |     |          |                    |          |        | ’director’, |     | ’chair’] |          |         |     |     |
| posición    | tenga    | acceso             | al contexto |     | anterior | y posterior        | en la    |        |             |     |          |          |         |     |     |
secuencia.
|                      |             |            |                  |           |       |             |           | El vocabulario |             | se construye |            | sobre        | el conjunto |         | de entre- |
| -------------------- | ----------- | ---------- | ---------------- | --------- | ----- | ----------- | --------- | -------------- | ----------- | ------------ | ---------- | ------------ | ----------- | ------- | --------- |
| Las representaciones |             |            | distribucionales |           |       | de palabras | como      |                |             |              |            |              |             |         |           |
|                      |             |            |                  |           |       |             |           | namiento.      | Los tokens  | se           | convierten |              | a índices   | enteros | y se      |
| GloVe                | [2] asignan | a          | cada             | término   | un    | vector      | denso que |                |             |              |            |              |             |         |           |
|                      |             |            |                  |           |       |             |           | rellenan       | con padding |              | hasta      | una longitud | máxima      |         | de 300    |
| codifica             | similitud   | semántica, |                  | entrenado | sobre | un          | corpus de |                |             |              |            |              |             |         |           |
tokens.
| gran escala | (Wikipedia |     | y   | Gigaword). | Inicializar |     | los em- |     |     |     |     |     |     |     |     |
| ----------- | ---------- | --- | --- | ---------- | ----------- | --- | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
beddings del modelo con vectores preentrenados acelera la C. Embeddings GloVe
convergencia y mejora el rendimiento cuando el conjunto de Se usa el modelo glove-wiki-gigaword-100 (100
| datos de | entrenamiento |     | es limitado. |     |     |     |     |              |         |     | gensim.downloader). |     |     |     |     |
| -------- | ------------- | --- | ------------ | --- | --- | --- | --- | ------------ | ------- | --- | ------------------- | --- | --- | --- | --- |
|          |               |     |              |     |     |     |     | dimensiones, | cargado |     | con                 |     |     |     | La  |
EstetrabajoimplementaunmodeloSentimentBiLSTM cobertura típica sobre el vocabulario del dataset supera el
que combina embeddings GloVe, una capa BiLSTM con 85%. Las palabras ausentes se inicializan en cero. Los
mean pooling y fine-tuning progresivo de los embeddings. embeddings se congelan durante las primeras 3 épocas y se
Se aplican optimizaciones para reducir el tiempo de entre- descongelancontasadeaprendizaje10−4 paraelfine-tuning
| namiento | sin impacto |     | significativo |     | en la | precisión. |     | progresivo. |     |     |     |     |     |     |     |
| -------- | ----------- | --- | ------------- | --- | ----- | ---------- | --- | ----------- | --- | --- | --- | --- | --- | --- | --- |

| D. Arquitectura  |         | del modelo    |           |               |       |         |         |     |     |     |     |     |     |     |
| ---------------- | ------- | ------------- | --------- | ------------- | ----- | ------- | ------- | --- | --- | --- | --- | --- | --- | --- |
| La               | Tabla   | II            | describe  | las           | capas | del     | modelo  |     |     |     |     |     |     |     |
| SentimentBiLSTM. |         |               | La        | secuencia     |       | de 300  | índices |     |     |     |     |     |     |     |
| pasa por         | la capa | de embedding, |           | una           | capa  | BiLSTM  | de 128  |     |     |     |     |     |     |     |
| unidades         | por     | dirección     | (256      | total),       | mean  | pooling | sobre   |     |     |     |     |     |     |     |
| todos los        | estados | ocultos       | de        | la secuencia, |       | dropout | y una   |     |     |     |     |     |     |     |
| capa densa       | con     | función       | sigmoide. |               |       |         |         |     |     |     |     |     |     |     |
Fig.1. PérdidaBCE(izq.)ymétricasdevalidación(der.)porépoca.La
|     |     |     | TABLEII |     |     |     |     | convergenciasedetieneporparadaanticipada. |     |     |     |     |     |     |
| --- | --- | --- | ------- | --- | --- | --- | --- | ----------------------------------------- | --- | --- | --- | --- | --- | --- |
CAPASDELMODELOSENTIMENTBILSTM.
TABLEIII
MÉTRICASENELCONJUNTODEPRUEBA(4000MUESTRAS).
| Capa        |         |           |       | Salida    |     |     | Parám.  |     |     |           |           |       |     |     |
| ----------- | ------- | --------- | ----- | --------- | --- | --- | ------- | --- | --- | --------- | --------- | ----- | --- | --- |
| Embedding   | (GloVe  | 100d)     |       | B×300×100 |     |     | |V|×100 |     |     |           |           |       |     |     |
|             |         |           |       |           |     |     |         |     |     | Métrica   |           | Valor |     |     |
| Dropout     | (0.3)   |           |       | B×300×100 |     |     | 0       |     |     |           |           |       |     |     |
| BiLSTM      | (128    | ud., 1    | capa) | B×300×256 |     |     | ∼267K   |     |     | Precisión |           | –     |     |     |
|             |         |           |       |           |     |     |         |     |     | Recall    |           | –     |     |     |
| Mean        | Pooling |           |       | B×256     |     |     | 0       |     |     |           |           |       |     |     |
|             |         |           |       |           |     |     |         |     |     | F1-Score  |           | –     |     |     |
| Dropout     | (0.3)   |           |       | B×256     |     |     | 0       |     |     |           |           |       |     |     |
| Linear(256, | 1)      | + Sigmoid |       | B×1       |     |     | 257     |     |     |           |           |       |     |     |
|             |         |           |       |           |     |     |         |     |     | IV.       | DISCUSIÓN |       |     |     |
Elmeanpoolingpromedialosestadosocultosdetodaslas
ElmodelocombinarepresentacionessemánticasdeGloVe
posicionesdelasecuencia,loquepermitealmodelocapturar
|     |     |     |     |     |     |     |     | con el modelado |     | secuencial | del | BiLSTM. | El  | mean pool- |
| --- | --- | --- | --- | --- | --- | --- | --- | --------------- | --- | ---------- | --- | ------- | --- | ---------- |
tokensrelevantesencualquierposición,adiferenciadetomar
|                  |     |        |         |     |     |     |     | ing sobre      | todos  | los estados  | ocultos   |     | proporciona | una rep-    |
| ---------------- | --- | ------ | ------- | --- | --- | --- | --- | -------------- | ------ | ------------ | --------- | --- | ----------- | ----------- |
| solo el último   |     | estado | oculto. |     |     |     |     |                |        |              |           |     |             |             |
|                  |     |        |         |     |     |     |     | resentación    | de     | la secuencia | completa, |     | lo que      | lo hace más |
|                  |     |        |         |     |     |     |     | robusto        | frente | a secuencias | largas    | que | el uso      | del último  |
| E. Entrenamiento |     |        |         |     |     |     |     | estado oculto. |        |              |           |     |             |             |
El optimizador es Adam con tasa de aprendizaje inicial El fine-tuning progresivo de embeddings estabiliza las
primerasépocasalmantenerfijoslosvectorespreentrenados
| 10−3 y | función | de  | pérdida | de entropía |     | cruzada | binaria |     |     |     |     |     |     |     |
| ------ | ------- | --- | ------- | ----------- | --- | ------- | ------- | --- | --- | --- | --- | --- | --- | --- |
(BCE). El tamaño de batch es 128. Los DataLoaders usan mientras el resto del modelo converge. Descongelarlos con
unatasadeaprendizajediezvecesmenorevitadestruirlain-
| num_workers=4 |     | y   | pin_memory=True |     |     | para | paralelizar |           |           |           |     |         |                      |     |
| ------------- | --- | --- | --------------- | --- | --- | ---- | ----------- | --------- | --------- | --------- | --- | ------- | -------------------- | --- |
|               |     |     |                 |     |     |      |             | formación | semántica | capturada |     | durante | el preentrenamiento. |     |
lacargadedatosyreducirlalatenciadetransferenciaCPU–
GPU. El entrenamiento se ejecuta hasta 20 épocas con los Las optimizaciones de velocidad (MAX_LEN=300, una
|            |             |     |             |           |          |     |         | capa LSTM, | 128       | unidades,     | batch=128, |                    | num_workers=4) |             |
| ---------- | ----------- | --- | ----------- | --------- | -------- | --- | ------- | ---------- | --------- | ------------- | ---------- | ------------------ | -------------- | ----------- |
| siguientes | mecanismos  |     | de control: |           |          |     |         |            |           |               |            |                    |                |             |
|            |             |     |             |           |          |     |         | reducen    | el tiempo | por           | época      | en aproximadamente |                | 3–4×        |
| • Parada   | anticipada: |     | se          | monitorea | val_loss |     | con pa- |            |           |               |            |                    |                |             |
|            |             |     |             |           |          |     |         | respecto   | a una     | configuración |            | más profunda,      |                | con impacto |
cienciade5épocas.Elentrenamientosedetienecuando
|                    |     |               |     |           |         |          |             | menor en      | las métricas | de         | evaluación. |           |              |        |
| ------------------ | --- | ------------- | --- | --------- | ------- | -------- | ----------- | ------------- | ------------ | ---------- | ----------- | --------- | ------------ | ------ |
| la pérdida         |     | de validación |     | no mejora | en      | al menos | 10−4.       |               |              |            |             |           |              |        |
|                    |     |               |     |           |         |          |             | Limitaciones: |              | el número  | de          | épocas    | de congelado | es     |
| ReduceLROnPlateau: |     |               |     | reduce    | la tasa | de       | aprendizaje |               |              |            |             |           |              |        |
| •                  |     |               |     |           |         |          |             | fijo; un      | criterio     | adaptativo | podría      | ajustarse | mejor        | a cada |
val_loss
| por          | un factor     | de             | 0.5        | si              |               | no mejora | en        | 2             |             |             |                  |         |            |             |
| ------------ | ------------- | -------------- | ---------- | --------------- | ------------- | --------- | --------- | ------------- | ----------- | ----------- | ---------------- | ------- | ---------- | ----------- |
|              |               |                |            |                 |               |           |           | ejecución.    | Las         | reseñas     | con más          | de 300  | tokens     | se truncan, |
| épocas       | consecutivas. |                |            |                 |               |           |           |               |             |             |                  |         |            |             |
|              |               |                |            |                 |               |           |           | perdiendo     | el contexto |             | del final        | del     | texto. No  | se realizó  |
| Gradient     |               | clipping:      |            | clip_grad_norm_ |               |           | con       |               |             |             |                  |         |            |             |
| •            |               |                |            |                 |               |           |           | búsqueda      | sistemática | de          | hiperparámetros. |         |            |             |
| max_norm=1.0 |               |                | estabiliza | el              | entrenamiento |           | limitando |               |             |             |                  |         |            |             |
|              |               |                |            |                 |               |           |           | Trabajo       | futuro:     | comparar    |                  | con     | un encoder | Trans-      |
| la norma     |               | del gradiente. |            |                 |               |           |           |               |             |             |                  |         |            |             |
|              |               |                |            |                 |               |           |           | former ligero |             | (DistilBERT | [5]),            | aplicar | precisión  | mixta       |
(torch.cuda.amp)paramayorvelocidadenGPUyeval-
III. RESULTADOS uar el impacto de distintas longitudes de secuencia.
| A. Curvas     | de    | entrenamiento |            |            |           |                  |             |     |     |     |     |     |     |     |
| ------------- | ----- | ------------- | ---------- | ---------- | --------- | ---------------- | ----------- | --- | --- | --- | --- | --- | --- | --- |
| La Figura     | 1     | muestra       | la pérdida |            | BCE en    | entrenamiento    |             | y   |     |     |     |     |     |     |
| validación,   | y las | métricas      | de         | precisión, | recall    | y                | F1-score en |     |     |     |     |     |     |     |
| validación,   | por   | época         | hasta      | el punto   | de parada | anticipada.      |             |     |     |     |     |     |     |     |
| B. Métricas   | en    | el conjunto   |            | de prueba  |           |                  |             |     |     |     |     |     |     |     |
| La Tabla      | III   | reporta       | las        | métricas   | obtenidas |                  | sobre las   |     |     |     |     |     |     |     |
| 4000 muestras |       | del conjunto  |            | de prueba  | tras      | el entrenamiento |             |     |     |     |     |     |     |     |
| completo.     | Los   | valores       | se generan | ejecutando |           | la última        | celda       |     |     |     |     |     |     |     |
miniproyecto2_draft_2.ipynb.
de

REFERENCES
[1] S.HochreiterandJ.Schmidhuber,“Longshort-termmemory,”Neural
Computation,vol.9,no.8,pp.1735–1780,1997.
[2] J.Pennington,R.Socher,andC.D.Manning,“GloVe:Globalvectors
forwordrepresentation,”inProc.EMNLP,pp.1532–1543,2014.
[3] A.L.Maas,R.E.Daly,P.T.Pham,D.Huang,A.Y.Ng,andC.Potts,
“Learningwordvectorsforsentimentanalysis,”inProc.49thAnnual
MeetingoftheACL,pp.142–150,2011.
| [4] A. Paszke | et al., “PyTorch: | An  | imperative style, | high-performance |
| ------------- | ----------------- | --- | ----------------- | ---------------- |
deeplearninglibrary,”inAdvancesinNeurIPS,vol.32,2019.
| [5] V. Sanh, | L. Debut, J.     | Chaumond, | and T. Wolf,    | “DistilBERT, a |
| ------------ | ---------------- | --------- | --------------- | -------------- |
| distilled    | version of BERT: | smaller,  | faster, cheaper | and lighter,”  |
arXiv:1910.01108,2019.
| [6] S. Bird, | E. Klein, and E. | Loper, | Natural Language | Processing with |
| ------------ | ---------------- | ------ | ---------------- | --------------- |
Python.O’ReillyMedia,2009.