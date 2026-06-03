Plantilla para informes de miniproyecto curso Técnicas de Deep
Learning
|     |     |     |     |     | Nombre | Autor | 1   | and Nombre | Autor | 2   |     |     |     |     |
| --- | --- | --- | --- | --- | ------ | ----- | --- | ---------- | ----- | --- | --- | --- | --- | --- |
I. INTRODUCCIÓN se utilizó validación cruzada o un conjunto de validación
En la introducción de un informe se debe presentar de independiente. En cuanto a la evaluación del modelo, es
|           |              |          |           |     |            |          |         | esencial | definir | las métricas | utilizadas |     | (precisión, | F1-score, |
| --------- | ------------ | -------- | --------- | --- | ---------- | -------- | ------- | -------- | ------- | ------------ | ---------- | --- | ----------- | --------- |
| manera    | clara el     | problema | abordado, | su  | relevancia | y        | la con- |          |         |              |            |     |             |           |
|           |              |          |           |     |            |          |         | IOU,     | etc.).  |              |            |     |             |           |
| tribución | del trabajo. | Para     | lograrlo, | se  | recomienda | comenzar |         |          |         |              |            |     |             |           |
con un contexto general que sitúe al lector en el área Finalmente, si se realizaron análisis adicionales, como
estudiosdeablaciónparaevaluarlacontribucióndedistintos
| de estudio. | Este | puede | incluir | una breve | referencia |     | a los |     |     |     |     |     |     |     |
| ----------- | ---- | ----- | ------- | --------- | ---------- | --- | ----- | --- | --- | --- | --- | --- | --- | --- |
avances recientes y a su impacto en diversas aplicaciones, componentesdelmodelo,estostambiéndebendescribirseen
| como visión | por | computadora, |     | procesamiento |     | del | lenguaje | esta sección. |     |     |     |     |     |     |
| ----------- | --- | ------------ | --- | ------------- | --- | --- | -------- | ------------- | --- | --- | --- | --- | --- | --- |
naturalobioinformática.Además,esimportantedestacarlos
desafíos actuales.
| Después | de  | establecer | el contexto, |     | se debe | definir | con |     |     |     |     |     |     |     |
| ------- | --- | ---------- | ------------ | --- | ------- | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
precisiónelproblemaespecíficoqueseabordaenelinforme.
| Es fundamental |             | justificar | su relevancia |         | y explicar |               | por qué |     |     |     |     |     |     |     |
| -------------- | ----------- | ---------- | ------------- | ------- | ---------- | ------------- | ------- | --- | --- | --- | --- | --- | --- | --- |
| representa     | un desafío  |            | dentro del    | campo.  | En         | este punto,   | es      |     |     |     |     |     |     |     |
| útil incluir   | referencias |            | a estudios    | previos | que        | han tratado   | de      |     |     |     |     |     |     |     |
| resolver       | problemas   | similares, | resaltando    |         | sus        | limitaciones. |         |     |     |     |     |     |     |     |
Finalmente, las introducciones finalizan con un pequeño Fig.1. Figuraqueejemplificaundiagramadelametodologíadeunpaper
|         |               |     |             |       |         |          |     | que trabaja | con                | modelos de | difusión. | Como se puede | ver    | es un diagrama    |
| ------- | ------------- | --- | ----------- | ----- | ------- | -------- | --- | ----------- | ------------------ | ---------- | --------- | ------------- | ------ | ----------------- |
| párrafo | especificando |     | que se hizo | en el | estudio | y cuales | son |             |                    |            |           |               |        |                   |
|         |               |     |             |       |         |          |     | simple      | del funcionamiento | del        | modelo    | utilizado.    | Es una | práctica bastante |
los aportes del mismo. común utilizar este tipo de diagramas para darle una idea al lector sobre
cualfueeltrabajorealizado.
|            |     | II.         | METODOLOGÍA |           |     |           |     |     |     |     |     |     |     |     |
| ---------- | --- | ----------- | ----------- | --------- | --- | --------- | --- | --- | --- | --- | --- | --- | --- | --- |
| La sección | de  | metodología | debe        | describir |     | de manera | de- |     |     |     |     |     |     |     |
talladaelenfoquepropuesto.Esfundamentalestructuraresta III. RESULTADOS
seccióndeformaclaraylógica,explicandoloscomponentes
Lasecciónderesultadosenuninformesepresentayanal-
| clave del | modelo, | los | datos utilizados |     | y el | procedimiento |     |     |     |     |     |     |     |     |
| --------- | ------- | --- | ---------------- | --- | ---- | ------------- | --- | --- | --- | --- | --- | --- | --- | --- |
experimental. izaloshallazgosobtenidosapartirdelosexperimentosreal-
Se recomienda comenzar con una descripción general del izados. Su objetivo es demostrar el desempeño del enfoque
|         |         |       |          |         |       |              |     | propuesto | y,  | de ser posible, | compararlo |     | con otros | métodos |
| ------- | ------- | ----- | -------- | ------- | ----- | ------------ | --- | --------- | --- | --------------- | ---------- | --- | --------- | ------- |
| enfoque | seguido | en el | estudio. | Aquí se | puede | proporcionar |     |           |     |                 |            |     |           |         |
una visión global del método, resaltando sus principales relevantes. Para que esta sección sea clara y efectiva, es
|                 |     |      |               |     |          |          |     | recomendable |     | estructurarla | de manera | ordenada, |     | destacando |
| --------------- | --- | ---- | ------------- | --- | -------- | -------- | --- | ------------ | --- | ------------- | --------- | --------- | --- | ---------- |
| características | y   | cómo | se diferencia | de  | enfoques | previos. | En  |              |     |               |           |           |     |            |
algunos casos, es útil incluir un diagrama que resuma la los aspectos más relevantes de los resultados sin sobrecargar
arquitectura del modelo o el flujo del proceso. al lector con información innecesaria.
Acontinuación,sedebendetallarlosdatosutilizadosenla Sepuedecomenzarconunadescripcióngeneraldelosex-
investigación. Esto incluye la fuente de los datos, las carac- perimentosrealizadosysusobjetivos.Esimportanterecordar
terísticas relevantes y cualquier preprocesamiento realizado. al lector qué aspectos del modelo se están evaluando y qué
Esimportantemencionaraspectoscomolanormalizaciónde se espera demostrar con los resultados. En este punto, se
los datos, el aumento de datos o la división en conjuntos de pueden incluirtablas o gráficos que resuman las métricas
|                |     |            |           |     |     |     |     | clave | obtenidas, | como | precisión, | F1-score, |     | pérdida, IoU, |
| -------------- | --- | ---------- | --------- | --- | --- | --- | --- | ----- | ---------- | ---- | ---------- | --------- | --- | ------------- |
| entrenamiento, |     | validación | y prueba. |     |     |     |     |       |            |      |            |           |     |               |
Después de describir losdatos, se debe presentar la arqui- entre otras, dependiendo de la naturaleza del problema.
tectura del modelo propuesto. En este apartado, se explica Luego, se presentan los resultados cuantitativos obtenidos.
la estructura de la red neuronal o del algoritmo empleado, Además de los resultados numéricos, es recomendable
incluyendoelnúmerodecapas,lostiposdeactivaciones,las incluiranálisiscualitativoscuandoseapertinente.Enproble-
funciones de pérdida y los optimizadores utilizados. mascomovisiónporcomputadoraogeneracióndetexto,las
Otro aspecto clave de la metodología es la estrategia de visualizacionesjueganunpapelclave.Porejemplo,entareas
entrenamiento y evaluación. Aquí se deben especificar los desegmentacióndeimágenes,sepuedenincluirejemplosde
hiperparámetros utilizados, como la tasa de aprendizaje, el segmentaciones predichas frente a las etiquetas reales para
tamaño del batch y el número de épocas. También se debe ilustrar el desempeño del modelo. En tareas de generación,
describir el procedimiento de validación, por ejemplo, si se pueden presentar ejemplos de las muestras generadas y

TABLEI
EJEMPLODEUNAMATRIZDECONFUSIÓNENLAQUESEPRESENTAN
LOSRESULTADOSDEUNMODELODECLASIFICACIÓNDEIMÁGENES.
PredvsAnot Pulmónsano Adenocarcinoma Cel.Escamosas
Pulmónsano 888 17 0
Adenocarcinoma 112 837 140
Cel.escamosas 0 146 860
compararlasconejemplosrealesoconlosresultadosdeotros
modelos.
Otro aspecto importante son estudios de ablación para
evaluar la contribución de diferentes componentes del mod-
elo, análisis de sensibilidad a los hiperparámetros o evalu-
aciónenconjuntosdedatosexternosparaprobarlacapacidad
de generalización.
Finalmente,sedebeproporcionarunainterpretacióndelos
resultados obtenidos. No basta con presentar métricas, sino
que es clave explicar qué significan en el contexto del prob-
lema estudiado. Se pueden discutir implicaciones prácticas,
limitaciones del enfoque y posibles mejoras futuras.
Lasecciónderesultadosdebeserclarayprecisa,evitando
interpretacionesespeculativassinevidenciaexperimental.Es
recomendable apoyarse en figuras y tablas bien diseñadas
para facilitar la comprensión de los hallazgos y permitir
comparaciones efectivas.
IV. DISCUSIÓN
La sección de discusión tiene como objetivo interpretar
y contextualizar los resultados obtenidos, explicando su
relevancia, implicaciones y posibles limitaciones. En esta
sección, se analizan los hallazgos en profundidad y se rela-
cionan con trabajos previos, destacando las contribuciones
del estudio y proponiendo direcciones futuras.
Se puede comenzar con un resumen de los principales
resultados obtenidos, resaltando los aspectos en los que el
enfoque propuesto ha demostrado ser exitoso. Es importante
contextualizar estos hallazgos dentro del campo de estudio
y explicar cómo se comparan con investigaciones previas.
A continuación, es fundamental analizar las limitaciones
del estudio. Todo modelo de Inteligencia Artificial tiene
restricciones,yreconocerlasdemuestrarigorcientífico.Estas
limitacionespuedenestarrelacionadasconlacantidadycal-
idad de los datos utilizados, la capacidad de generalización
del modelo, el costo computacional del entrenamiento o la
sensibilidad a ciertos hiperparámetros. También es relevante
discutirposiblessesgosenlosdatosoenlametodologíaque
podrían haber afectado los resultados.
REFERENCES
[1] G. O. Young, “Synthetic structure of industrial plastics (Book style
withpapertitleandeditor),”inPlastics,2nded.vol.3,J.Peters,Ed.
NewYork:McGraw-Hill,1964,pp.15–64.
[2] W.-K. Chen, Linear Networks and Systems (Book style). Belmont,
CA:Wadsworth,1993,pp.123–135.
[3] H. Poor, An Introduction to Signal Detection and Estimation. New
York:Springer-Verlag,1985,ch.4.