Clasificación de Sentimientos de Reseñas de Películas en IMDb
|     |     |     |        | con | Redes        | Neuronales |            | Recurrentes |       |            |     |     |     |     |     |
| --- | --- | --- | ------ | --- | ------------ | ---------- | ---------- | ----------- | ----- | ---------- | --- | --- | --- | --- | --- |
|     |     |     | Yezid  |     | Garcia∗,     | Juan       | Martin     | Santos∗,    | Jaime | Rodriguez∗ |     |     |     |     |     |
|     |     |     | ∗Grupo |     | 24. Códigos: |            | 200810710, | 202013610,  |       | 200717791  |     |     |     |     |     |
I. INTRODUCCIÓN para evitar fuga de información, y las secuencias se rellenan
|             |                     |             |     |             |                   |             |     | o truncan      | a 300 | tokens. |             |     |              |       |     |
| ----------- | ------------------- | ----------- | --- | ----------- | ----------------- | ----------- | --- | -------------- | ----- | ------- | ----------- | --- | ------------ | ----- | --- |
| El análisis | de                  | sentimiento | es  | una tarea   | del procesamiento |             |     |                |       |         |             |     |              |       |     |
|             |                     |             |     |             |                   |             |     | Los embeddings |       | se      | inicializan |     | con vectores | GloVe | de  |
| delenguaje  | naturalquedetermina |             |     | lapolaridad |                   | emocionalde |     |                |       |         |             |     |              |       |     |
untexto.Enelcontextodereseñasdepelículas,elproblema 100 dimensiones [3], con una cobertura del 77.2% sobre
|             |            |                 |     |     |               |         |     | el vocabulario. |     | Siguiendo | la  | estrategia | de  | ajuste progresivo |     |
| ----------- | ---------- | --------------- | --- | --- | ------------- | ------- | --- | --------------- | --- | --------- | --- | ---------- | --- | ----------------- | --- |
| consiste en | clasificar | automáticamente |     |     | si una reseña | expresa |     |                 |     |           |     |            |     |                   |     |
una opinión positiva o negativa. Esta capacidad tiene apli- propuestaen[5],losembeddingssecongelandurantelastres
cacióndirectaensistemasderecomendaciónymonitoreode primerasépocasparaquelascapasrecurrentesconverjansin
|             |       |          |         |           |     |          |     | distorsionar | las | representaciones |     | preentrenadas; |     | a   | partir de |
| ----------- | ----- | -------- | ------- | --------- | --- | -------- | --- | ------------ | --- | ---------------- | --- | -------------- | --- | --- | --------- |
| reputación, | donde | procesar | grandes | volúmenes |     | de texto | de  |              |     |                  |     |                |     |     |           |
forma manual no es viable. la cuarta época se descongelan con una tasa de aprendizaje
|              |       |          |          |               |         |             |     | diez veces | menor.          |     |     |          |     |       |           |
| ------------ | ----- | -------- | -------- | ------------- | ------- | ----------- | --- | ---------- | --------------- | --- | --- | -------- | --- | ----- | --------- |
| Los enfoques |       | clásicos | basados  | en frecuencia |         | de términos |     |            |                 |     |     |          |     |       |           |
|              |       |          |          |               |         |             |     | El modelo  | SentimentBiLSTM |     |     | encadena | las | capas | descritas |
| ignoran el   | orden | de las   | palabras | y             | pierden | información |     |            |                 |     |     |          |     |       |           |
contextual. Las redes con celdas de memoria a largo y corto en la Tabla 1. La capa BiLSTM de 128 unidades por direc-
|     |     |     |     |     |     |     |     | ción procesa | la  | secuencia | en  | ambos | sentidos; | un  | promedio |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------ | --- | --------- | --- | ----- | --------- | --- | -------- |
plazo(LSTM)[1]superanestalimitaciónalprocesarsecuen-
cias de tokens y capturar dependencias entre palabras dis- sobre todos los estados ocultos (mean pooling) produce
|                    |          |               |              |          |                |         |     | una representación |             | de  | longitud | fija.      | Esta operación, |        | validada |
| ------------------ | -------- | ------------- | ------------ | -------- | -------------- | ------- | --- | ------------------ | ----------- | --- | -------- | ---------- | --------------- | ------ | -------- |
| tantes. La         | variante | bidireccional |              | (BiLSTM) | combina        | estados |     |                    |             |     |          |            |                 |        |          |
|                    |          |               |              |          |                |         |     | en [6],            | es superior | al  | uso      | del último | estado          | oculto | para     |
| ocultos procesados |          | en ambas      | direcciones, |          | proporcionando |         | a   |                    |             |     |          |            |                 |        |          |
cada posición acceso al contexto anterior y posterior. Las secuencias largas donde el sentimiento está distribuido a
|                  |     |                  |     |             |     |               |     | lo largo | del texto. | Una | capa | lineal | con activación |     | sigmoide |
| ---------------- | --- | ---------------- | --- | ----------- | --- | ------------- | --- | -------- | ---------- | --- | ---- | ------ | -------------- | --- | -------- |
| representaciones |     | distribucionales |     | de palabras |     | [2] codifican |     |          |            |     |      |        |                |     |          |
similitud semántica en vectores densos entrenados sobre produce la clasificación final.
| grandes corpus; |     | inicializar | un modelo |     | con vectores |     | preen- |     |     |     |     |     |     |     |     |
| --------------- | --- | ----------- | --------- | --- | ------------ | --- | ------ | --- | --- | --- | --- | --- | --- | --- | --- |
Tabla1.
| trenados como | GloVe | [3] | mejora | la generalización |     | cuando |     |     |     |     |     |     |     |     |     |
| ------------- | ----- | --- | ------ | ----------------- | --- | ------ | --- | --- | --- | --- | --- | --- | --- | --- | --- |
CAPASDELMODELOSentimentBiLSTM.
| el conjunto | de entrenamiento |     | es  | de tamaño | moderado. |     |     |     |     |     |     |     |     |     |     |
| ----------- | ---------------- | --- | --- | --------- | --------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Estetrabajodescribelaimplementaciónyevaluacióndeun
|     |     |     |     |     |     |     |     | Capa |     |     | Dimensión |     | de salida | Parámetros |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ---- | --- | --- | --------- | --- | --------- | ---------- | --- |
modeloBiLSTMconembeddingsGloVeparalaclasificación
binaria de reseñas del conjunto IMDb [4]. Se presentan el EmbeddingGloVe100d B×300×100 7,449,500
|     |     |     |     |     |     |     |     | Abandono(p=0.3) |     |     | B×300×100 |     |     |     | 0   |
| --- | --- | --- | --- | --- | --- | --- | --- | --------------- | --- | --- | --------- | --- | --- | --- | --- |
pipeline de preprocesamiento, la arquitectura del modelo, BiLSTM(128ud.,1capa) B×300×256 267,264
la estrategia de entrenamiento, los resultados cuantitativos MeanPooling B×256 0
|                 |     |             |     |              |     |          |     | Abandono(p=0.3) |     |     | B×256 |     |     |           | 0   |
| --------------- | --- | ----------- | --- | ------------ | --- | -------- | --- | --------------- | --- | --- | ----- | --- | --- | --------- | --- |
| y cualitativos, | y   | un análisis | de  | los factores | que | explican | el  |                 |     |     |       |     |     |           |     |
|                 |     |             |     |              |     |          |     | Lineal+Sigmoide |     |     | B×1   |     |     |           | 257 |
| comportamiento  |     | del modelo. |     |              |     |          |     |                 |     |     |       |     |     |           |     |
|                 |     |             |     |              |     |          |     | Total           |     |     |       |     |     | 7,685,277 |     |
II. METODOLOGÍA
Paraeldesarrollodelproyectosesiguióelciclotradicional ElentrenamientousaAdamcontasadeaprendizajeinicial
de aprendizaje automático: entendimiento del problema, re- de 10−3 y pérdida de entropía cruzada binaria, con lotes
copilaciónypreparacióndelosdatos,diseñoyentrenamiento
|     |     |     |     |     |     |     |     | de 128 muestras. |     | Se aplican |     | tres mecanismos |     | de control: | un  |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------------- | --- | ---------- | --- | --------------- | --- | ----------- | --- |
delmodelo,evaluaciónsobreunconjuntodepruebaindepen- planificadorquereducelatasadeaprendizajealamitadsila
diente, y análisis de los resultados obtenidos. pérdidadevalidaciónnomejoraendosépocasconsecutivas;
El conjunto de datos contiene 40000 reseñas de IMDb limitación de la norma del gradiente a 1.0, que [7] identifica
[4]conetiquetabinariadesentimiento,balanceadoen20000 como crítico para estabilizar el entrenamiento de LSTM en
muestrasporclaseysinvaloresnulos.Ladivisiónesestrati-
secuenciaslargas;yparadaanticipadaconpacienciadecinco
ficadaporclase:80%paraentrenamiento(32000muestras), épocas. Las métricas de evaluación son precisión, recall y
10% para validación (4000) y 10% para prueba (4000). F1-score, calculadas sobre el conjunto de prueba al finalizar
| Cada reseña | pasa      | por   | un pipeline |     | de cinco      | pasos: | elim-  | el entrenamiento. |     |     |     |     |     |     |     |
| ----------- | --------- | ----- | ----------- | --- | ------------- | ------ | ------ | ----------------- | --- | --- | --- | --- | --- | --- | --- |
| inación de  | etiquetas | HTML; | descarte    |     | de caracteres |        | no al- |                   |     |     |     |     |     |     |     |
fabéticos; conversión a minúsculas; eliminación de palabras III. RESULTADOS
funcionaleseninglés;ylematización,quereducecadatoken Se implementó un clasificador de sentimiento binario
a su forma canónica (running → run). El vocabulario se sobre40000reseñasdeIMDb,entrenandounaredBiLSTM
construyeexclusivamentesobreelconjuntodeentrenamiento de una capa con embeddings GloVe de 100 dimensiones

inicializados desde vectores preentrenados y ajustados de La convergencia es rápida en las primeras seis épocas,
formaprogresiva.Acontinuaciónsepresentanlosresultados donde el F1 pasa de 0.792 a 0.878; las épocas posteriores
mas relevantes. aportan mejoras marginales (0.878 a 0.899). La brecha
crecienteentrelapérdidadeentrenamientoyladevalidación
A. Resultados cuantitativos
a partir de la época 11 indica sobreajuste moderado que la
Seentrenóelmodeloduranteunmáximode20épocascon parada anticipada contiene sin eliminarlo por completo.
paradaanticipadaactivadaenlaépoca19.LaFig.1muestra
IV. DISCUSIÓN
la evolución de la pérdida en entrenamiento y validación,
y las métricas de precisión, recall y F1 en validación por El F1 de 0.893 sobre el conjunto de prueba es consistente
época. con los rangos reportados para arquitecturas recurrentes
sobre IMDb en [5]. El resultado corresponde al rango
esperado para una sola capa BiLSTM: [7] muestra que
capas adicionales no garantizan mejoras en clasificación
de secuencias de longitud moderada y pueden introducir
inestabilidad. El mean pooling sobre los estados ocultos,
validadoen[6],producerepresentacionesmásestablesqueel
últimoestadoocultoparareseñaslargasdondeelsentimiento
está distribuido a lo largo del texto, lo que contribuye a la
consistencia de las métricas en las épocas finales.
Fig.1. PérdidaBCE(izq.)ymétricasdevalidación(der.)porépoca.Parada La estrategia de congelado y ajuste fino es efectiva: la
anticipadaenépoca19. Tabla 2 muestra una ganancia de 2.7 puntos de F1 entre la
ép. 3 y la ép. 6, resultado coherente con [8], que demuestra
La Tabla 2 compara las métricas de validación en cuatro que los embeddings ajustables superan a los estáticos en
momentos del entrenamiento para cuantificar el efecto de tareas de clasificación de texto. El ajuste fino con tasa de
cada fase: con embeddings congelados (ép. 3), al inicio del aprendizaje reducida preserva las representaciones semán-
ajustefino(ép.6),enlaconvergencia(ép.11)yenlaúltima ticas preentrenadas mientras el modelo incorpora patrones
época ejecutada (ép. 19). La Tabla 3 reporta los resultados específicos del dominio. La cobertura de 77.2% de GloVe
finales sobre el conjunto de prueba. es suficiente para aportar información semántica útil desde
las primeras épocas; el 22.8% restante, inicializado en
Tabla2.
cero, corresponde principalmente a términos especializados
MÉTRICASDEVALIDACIÓNPORFASEDEENTRENAMIENTO.
o nombres propios de películas con menor impacto en la
clasificación.
Fase Precisión Recall F1
Entre las limitaciones del trabajo, el número de épocas
Ép.3—embeddingscongelados 0.811 0.895 0.851 de congelado es fijo y no se adapta a la velocidad de
Ép.6—inicioajustefino 0.848 0.909 0.878
convergenciadecadaejecución.Lasreseñasconmásde300
Ép.11—convergencia 0.889 0.894 0.892
tokens se truncan, perdiendo el contexto del final del texto,
Ép.19—paradaanticipada 0.890 0.909 0.899
dondeelcríticofrecuentementeexpresasuvaloracióndefini-
tiva. Adicionalmente, no se realizó búsqueda sistemática
de hiperparámetros, por lo que configuraciones alternativas
Tabla3.
podríanmejorarelrendimiento.Comotrabajofuturo,resulta
MÉTRICASFINALESSOBREELCONJUNTODEPRUEBA(4000
deinterésexplorarmecanismosdeatenciónsobrelosestados
MUESTRAS).
del BiLSTM como alternativa al mean pooling, evaluar el
impacto de distintas duraciones de la fase de congelado y
Métrica Valor
comparar el modelo con arquitecturas Transformer ligeras
Precisión 0.877
aplicadas al mismo conjunto de datos.
Recall 0.910
F1-Score 0.893
B. Resultados cualitativos
El recall supera sistemáticamente a la precisión tanto en
validacióncomoenprueba(0.910frentea0.877).Estoindica
una tendencia del modelo a clasificar como positivo ante la
ambigüedad,comportamientoconsistenteconelsesgodelos
vectores GloVe: intensificadores frecuentes en reseñas como
amazing o terrible tienen carga emocional pronunciada que
el modelo asocia con la clase positiva incluso en contextos
negativos. El efecto se mantiene estable tras el ajuste fino.

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
[5] J. Howard and S. Ruder, “Universal language model fine-tuning for
textclassification,”inProc.ACL,pp.328–339,2018.
[6] A.Conneau,D.Kiela,H.Schwenk,L.Barrault,andA.Bordes,“Su-
pervised learning of universal sentence representations from natural
languageinferencedata,”inProc.EMNLP,pp.670–680,2017.
[7] K. Greff, R. K. Srivastava, J. Koutn´ik, B. R. Steunebrink, and
J.Schmidhuber,“LSTM:Asearchspaceodyssey,”IEEETrans.Neural
Netw.Learn.Syst.,vol.28,no.10,pp.2222–2232,2017.
[8] Y. Kim, “Convolutional neural networks for sentence classification,”
inProc.EMNLP,pp.1746–1751,2014.