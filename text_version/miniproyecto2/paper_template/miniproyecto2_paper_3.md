Clasificación de Sentimientos de Reseñas de Películas en IMDb
con Redes Neuronales Recurrentes
Yezid Garcia∗, Juan Martin Santos∗, Jaime Rodriguez∗
∗Grupo 24. Códigos: 200810710, 202013610, 200717791
Abstract—Sepresentaunmodeloderedneuronalrecurrente • Validación: 10% (4000 muestras)
bidireccional(BiLSTM)paraclasificarelsentimientodereseñas • Prueba: 10% (4000 muestras)
de películas del conjunto de datos IMDb como positivo o
negativo.Elpipelinedepreprocesamientoaplicaeliminaciónde
etiquetasHTML,filtradodecaracteres,eliminacióndepalabras B. Preprocesamiento
funcionales y lematización. Los embeddings se inicializan con
vectores GloVe de 100 dimensiones y se ajustan mediante Cadareseñapasaporcincopasos:eliminacióndeetiquetas
una estrategia de entrenamiento progresivo que congela los HTML; descarte de caracteres no alfabéticos; conversión
embeddings en las primeras épocas y los desconecta con tasa a minúsculas; eliminación de palabras funcionales usando
de aprendizaje reducida. El modelo alcanza una precisión de
NLTK[9];ylematización.Lostokensseconviertenaíndices
0.877, un recall de 0.910 y un F1-score de 0.893 sobre 4000
enterosconunvocabularioconstruidosolosobreelconjunto
muestras de prueba.
deentrenamiento.Lassecuenciasserellenanotruncana300
I. INTRODUCCIÓN tokens.
El análisis de sentimiento es una tarea del procesamiento
de lenguaje natural (NLP) que determina la polaridad emo- C. Embeddings GloVe
cional de un texto. Su aplicación en reseñas de pelícu-
Los embeddings se inicializan con vectores GloVe de 100
las permite caracterizar la opinión del público de forma
dimensiones [3]; la cobertura sobre el vocabulario es del
automática, con utilidad en sistemas de recomendación y
77.2%. Para estabilizar el entrenamiento, los embeddings
monitoreo de reputación. Los enfoques clásicos basados en
se congelan durante las primeras tres épocas y luego se
frecuencia de términos ignoran el orden de las palabras y
descongelan con una tasa de aprendizaje diez veces menor.
pierden información contextual.
Estaestrategiadeajusteprogresivo,formalizadaen[6],evita
Las redes neuronales recurrentes con celdas LSTM [1]
destruir la información semántica preentrenada.
superan esta limitación al procesar secuencias de tokens
y capturar dependencias entre palabras distantes. La vari-
D. Arquitectura del modelo
ante bidireccional (BiLSTM) combina estados ocultos de
ambas direcciones, proporcionando a cada posición acceso El modelo encadena cuatro etapas descritas en la Tabla I.
al contexto anterior y posterior. Las representaciones dis- Lacapadeembeddingproyectacadaíndicealespaciovecto-
tribucionales de palabras [2] asignan a cada término un rial GloVe. La capa BiLSTM de 128 unidades por dirección
vector denso entrenado sobre grandes corpus; inicializar un (256 en total) procesa la secuencia en ambos sentidos. Un
modelo con vectores preentrenados como GloVe [3] mejora promedio sobre los estados ocultos de todas las posiciones
la generalización cuando el conjunto de entrenamiento es de de la secuencia (mean pooling) produce una representación
tamaño moderado. delongitudfija;[7]demuestraqueestaoperaciónessuperior
Estetrabajodescribelaimplementaciónyevaluacióndeun al uso del último estado oculto para tareas de clasificación.
modeloBiLSTMconembeddingsGloVeparalaclasificación Una capa lineal con activación sigmoide proyecta al espacio
binariadereseñasdelconjuntoIMDb.Sereportanprecisión, de probabilidad para la clasificación binaria.
recall y F1-score, se compara el rendimiento entre fases
de entrenamiento y se examinan los patrones de compor- TABLEI
tamiento del modelo. CAPASDELMODELOSentimentBiLSTM.
II. METODOLOGÍA Capa Dimensión de salida Parámetros
A. Conjunto de datos EmbeddingGloVe100d B×300×100 7,449,500
Abandono(p=0.3) B×300×100 0
El conjunto de datos contiene 40000 reseñas de IMDb BiLSTM(128ud.,1capa) B×300×256 267,264
[4] con etiqueta binaria de sentimiento. La distribución es MeanPooling B×256 0
balanceada:20000muestraspositivasy20000negativas.No Abandono(p=0.3) B×256 0
Lineal+Sigmoide B×1 257
se encontraron valores nulos ni texto vacío. La división es
Total 7,685,277
estratificada por clase:
• Entrenamiento: 80% (32000 muestras)

E. Entrenamiento clasificar como positivo ante la ambigüedad. Esto es con-
El optimizador es Adam (lr = 10−3) con pérdida de sistente con el sesgo de los vectores GloVe: intensificadores
frecuentes en reseñas como amazing o terrible tienen carga
entropía cruzada binaria y tamaño de lote 128. El ciclo
emocional pronunciada que el modelo asocia con la clase
incorpora:unplanificadorquereducelatasadeaprendizajea
positiva incluso en contextos negativos. El efecto persiste
lamitadsilapérdidadevalidaciónnomejoraendosépocas;
tras el ajuste fino.
limitacióndelanormadelgradientea1.0,críticoparaLSTM
La convergencia es rápida en las primeras seis épocas
según[5];yparadaanticipadaconpacienciadecincoépocas.
(F1: 0.792 a 0.878); las épocas siguientes aportan mejo-
Las métricas de evaluación son precisión, recall y F1-score,
ras marginales. La brecha creciente entre pérdida de en-
calculadas sobre el conjunto de prueba al finalizar.
trenamiento y validación a partir de la época 11 señala
III. RESULTADOS sobreajustemoderadoquelaparadaanticipadacontienepero
no elimina.
A. Resultados cuantitativos
La Figura 1 muestra la evolución de la pérdida en entre-
IV. DISCUSIÓN
namiento y validación, y de las métricas de validación por El F1 de 0.893 es consistente con rangos reportados en
época.Elentrenamientosedetuvoenlaépoca19porparada trabajos sobre IMDb con arquitecturas recurrentes [6]. El
anticipada. resultado se ubica en el rango esperado para una sola capa
LSTM,yaque[5]muestraquecapasadicionalesnosiempre
mejoran el rendimiento y pueden introducir inestabilidad.
Elmeanpoolingsobrelosestadosocultos,respaldadopor
[7], produce representaciones más estables que el último
estado oculto en reseñas largas donde el sentimiento está
distribuido. La Tabla II confirma que el ajuste fino de
embeddingsaporta2.7puntosdeF1entrelasépocas3y6,en
línea con [8] al comparar embeddings estáticos y ajustables.
Limitaciones: el número de épocas de congelado es fijo;
Fig.1. PérdidaBCE(izq.)ymétricasdevalidación(der.)porépoca.La las reseñas con más de 300 tokens se truncan perdiendo
línea vertical implícita ocurre en la época 19, donde se activa la parada el contexto final, y no se realizó búsqueda sistemática de
anticipada.
hiperparámetros.
Trabajofuturo:compararconuncodificadorTransformer
La Tabla II compara las métricas en tres momentos clave
ligero, explorar mecanismos de atención como alternativa al
delentrenamientoparacuantificarelefectodelaestrategiade
mean pooling y evaluar distintas duraciones de la fase de
ajuste progresivo. La Tabla III reporta los resultados finales
congelado.
sobre el conjunto de prueba.
TABLEII
EVOLUCIÓNDEMÉTRICASENVALIDACIÓNPORFASEDE
ENTRENAMIENTO.
Fase Precisión Recall F1
Ép.3—embeddingscongelados 0.811 0.895 0.851
Ép.6—iniciodelajustefino 0.848 0.909 0.878
Ép.11—convergencia 0.889 0.894 0.892
Ép.19—paradaanticipada 0.890 0.909 0.899
TABLEIII
MÉTRICASFINALESENELCONJUNTODEPRUEBA(4000MUESTRAS).
Métrica Valor
Precisión 0.877
Recall 0.910
F1-Score 0.893
B. Resultados cualitativos
El recall supera sistemáticamente a la precisión (0.910
frente a 0.877), lo que indica una tendencia del modelo a

REFERENCES
[1] S.HochreiterandJ.Schmidhuber,“Longshort-termmemory,”Neural
Computation,vol.9,no.8,pp.1735–1780,1997.
[2] T.Mikolov,K.Chen,G.Corrado,andJ.Dean,“Efficientestimationof
wordrepresentationsinvectorspace,”arXivpreprintarXiv:1301.3781,
2013.
[3] J.Pennington,R.Socher,andC.D.Manning,“GloVe:Globalvectors
forwordrepresentation,”inProc.EMNLP,pp.1532–1543,2014.
[4] A.L.Maas,R.E.Daly,P.T.Pham,D.Huang,A.Y.Ng,andC.Potts,
“Learningwordvectorsforsentimentanalysis,”inProc.49thAnnual
MeetingoftheACL,pp.142–150,2011.
| [5] K. Greff, | R. K. | Srivastava, | J. Koutn´ik, | B.  | R. Steunebrink, | and |
| ------------- | ----- | ----------- | ------------ | --- | --------------- | --- |
J.Schmidhuber,“LSTM:Asearchspaceodyssey,”IEEETrans.Neural
Netw.Learn.Syst.,vol.28,no.10,pp.2222–2232,2017.
| [6] J. Howard | and S. | Ruder, “Universal |     | language | model fine-tuning | for |
| ------------- | ------ | ----------------- | --- | -------- | ----------------- | --- |
textclassification,”inProc.ACL,pp.328–339,2018.
[7] A.Conneau,D.Kiela,H.Schwenk,L.Barrault,andA.Bordes,“Su-
| pervised | learning of | universal | sentence | representations | from | natural |
| -------- | ----------- | --------- | -------- | --------------- | ---- | ------- |
languageinferencedata,”inProc.EMNLP,pp.670–680,2017.
| [8] Y. Kim, | “Convolutional | neural | networks | for sentence | classification,” |     |
| ----------- | -------------- | ------ | -------- | ------------ | ---------------- | --- |
inProc.EMNLP,pp.1746–1751,2014.
| [9] S. Bird, | E. Klein, | and E. Loper, | Natural | Language | Processing | with |
| ------------ | --------- | ------------- | ------- | -------- | ---------- | ---- |
Python.O’ReillyMedia,2009.