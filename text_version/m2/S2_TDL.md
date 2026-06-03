## Page 1

Retos del Deep Learning
1 1 8 {
éCuándo usar modelos de Deep Learning?
Criterios basados en:
La representación de los datos La información a priori que poseemos La capacidad para explicar 0 interpretar los modelos obtenidos

## Page 2

Retos del Deep Learning
1 1 9 {
Interpretabilidad en los modelos:
Alta transparencia en los modelos: entender por qué y cómo hace las predicciones Interpretar las características y pesos obtenidos para determinar la salida
Explicabilidad en los modelos: Cómo tomar un modelo de ML y explicarlo en términos "humanos" Para modelos complejos, se pueden usar métodos agnósticos como SHapley Additive exPlanations (SHAP), gráficos de dependencias; entre otros
Output
Input
Black Box
Explainable

## Page 3

Retos del Deep Learning
1 1 9 {
Hybrid modclling approaches New explainability-preserving modelling approaches Interpretable feature enginccring
XAI s future research arena
High
Model
Pocl-har erplainabiliry techniques Interpretability-driven model designs
1 Learning Ucep Ensembles SVM  Models lized Bayesian Gen "82_ kNN 9 Tres Dccision Lincar /Logistic tersion RCpr' Rule-buced learning Low Low High Model interpretability
Accuracy vs interpretability trade-off
Tomado de Arrieta A. B., Díaz-Rodríguez, N. Del Ser; J. Bennetot; A. , Tabik, $. Barbado, A. Herrera F.(2020). Explainable Artificial Intelligence (XAI): Concepts; taxonomies; opportunities and challenges toward responsible Al. Information fusion.

## Page 4

Retos del Deep Learning nature machineintelligence
1 1 9 {
Explore content
About the journal
Publish with us
Subscribe
Dature
Dalure_machine intelligence perspeclives article
Perspective Published: 13 May 2019 Stopexplaining black box machinelearning modelsfor high stakes decisions and use interpretable models instead
Cnthia Rudin
Nature Machine Intelligence 206 215 (2019) Cite this article
76kAccesses 3236 Citations 504  Altmetric Metnics
reprint version of the article available at arXiv
Geoffrey Hinton @geoffreyhinton
Suppose you have cancer and you have to choose between ablack box Al surgeon that cannot explain how it works but has a 909 cure rate and ahuman surgeon with an 80% cure rate. Do you want the Al surgeon to be illegal? Traducir post
3,37 p. M. 20 feb. 2020

## Page 5

1 1 9 {
Redes neuronales
VS
SVM
Entrada
Representación
Decisión

## Page 6

1 1 9 {
Teorema de Bayes Analisis estadistico propuesto por Thomas Bayes
Perceptrón McCullogh Pitts prooonen Modelo de perceptron
SVM Vapnik y Chervonenkis inventan maquina soporte vectorlal
Truco del kernel Boser; Isabelle Guyon Vapnik   proponen truco kernel paf SVMs
Random forest Leo Breiman propone modelo de random forest
1926
1944
1986
1995
2012
1763
1943
1964
1992
2001
Discriminante lineal Ronald Fisher propone un discriminante   lineal con aplicaciones eugenesia
Regresión logística Berkson despues Cox proponen modelo regresión logistica
Árboles de decision perceptron multicapa Qunan orodone ID3 y
Boosting Freund Schapire proponen AdaBoost para Usua aprendices débiles deforma secuencial
Resurgimiento del deep learning Alex Krizhevsky Ilya Sulskever aiU Geuffrey Hinton proponen Alexnet
Hinton, Rumelhart, Williams proponen algoritmo de backpropagation

## Page 7

Redes neuronales
1 1 9 {
Neuronas en serie y paralelo con funciones de activación no lineales en las capas ocultas
Aproximación de una función no lineal
X2
X
X
X1
Entrada
Representación
Decisión

## Page 8

Redes neuronales
1 1 9 {
éDe dónde viene el poder de las redes neuronales?
=5
22
ORIGINAL CONTRIBUTION
Multilayer Feedforward Networks are Universal Approximators
Hanvik Tst
Maxwna Srllr MALBFn Whnit Urrmtrcereil Yado (34 mucita "rtohar inoe Mnlse4etslne [) EJl Necmnjle oshaa Haness[alula /' Wedoroven 9ec aiane 5 Verieh aun
The Universal Approximation Theorem:
Una red neuronal con al menos una capa oculta, Y un número suficiente de neuronas, Y una función de activación no lineal puede aproximar cualquier función continua con un nivel arbitrario de exactitud.
Entrada
Representación
Decisión

## Page 9

Redes neuronales
1 1 9 {
Capas ocultas (con funciones de activación no lineales): clave para aprendizaje de representación

## Page 10

Redes neuronales 0{0, Zocen
Dlos
oTn
1 1 9 {
0.5
21 3
22 3
20.5
5
285 211
0.5
71 7
77 1
72_2

## Page 11

Redes neuronales 0{0, Zocen
Dlos
oTn
1 1 9 {
iClasificador lineal sobre este espacio!
0,5
Queremos un clasificador g(0) wl 0 + b que sea tal que:
223
Los datos de una clase (clase -1) estén un lado del plano: g(0)
Los datos de la otra clase (clase +1) estén al otro lado del plano: g() > 0
05
77 ?
721
70 5

## Page 12

Máquinas de soporte vectorial 1 1 9 {
Maximizar el margen entre el clasificador y los datos de ambas clases

## Page 13

Máquinas de soporte vectorial 1 Maximizar el margen entre el clasificador y los datos de ambas clases 1 g(x) wTx + b 9 { Queremos un clasificador g(x) wTx + b que sea tal que:
Los datos de una clase (clase -1) estén a un lado del plano: g(x) < 0
Los datos de la otra clase (clase +1) estén al otro lado del plano: g(x) > 0

## Page 14

Máquinas de soporte vectorial 1 Queremos clasificar X tal que: 1 9 Si es de clase -1, entonces { g(x) @j ZjxT1 xj + b < 0
X
Si es de clase +1, entonces
g(x)
dj ZjxTxj + b > 0
Donde Zj esla clase del dato Xj @j multiplicador de Lagrange asociado al vector Xj Los @j son cero cuando Xj no es un vector de soporte

## Page 15

Máquinas de soporte vectorial 1 Queremos clasificar x tal que 1 9 Si es de clase -1, entonces g(x) Zjk(x,xj) + b < 0 { @j
Kernelizar producto punto para generar aproximaciones no lineales
X2
Si es de clase +1, entonces
g(x) aj  Zjk(x,xj) + b > 0 J =
X1
Donde Zj es la clase del dato Xj Qj multiplicador de Lagrange asociado al vector Xj Los @j son cero cuando Xj no es un vector de soporte k es el producto punto en un nuevo espacio

## Page 16

Máquinas de soporte vectorial
m
1 1 9 {
g(x) = @j   Zjk(x, Xj) + b j=1
Z1k(  X1)
Q1
&2
Zzk(  X2)
2
am
Zjk( , Xm)
Entrada
Representación
Decisión

## Page 17

Máquinas de soporte vectorial
96) = 2 @j  Zjk(x,xj) + b
1 1 9 {
Z1k(.*1)
Zzk(*2)
9(x
Om
Zjk ( , Xm)
Entrada
Representación
Decislón

## Page 18

Máquinas de soporte vectorial
Redes neuronales
1 1 9 {
71k(e I1)
1zk6"2)
9k(u)
Entrada
Representacicn
Decislón
enrada
Rerasanlocion
Uarron
Representación a partir de operaciones muy básicas
Formulación matemática muy bien estudiada
Podemos diseñar kernels a la medida para diferentes tipos de datos y problemas
Cantidad de parámetros a encontrar puede ser bastante grande
Entrenamiento costoso computacionalmente
Se pueden definir algoritmos eficientes para resolver el problema de aprendizaje
Podrían ofrecer modelos mejor interpretabilidad comparados con redes neuronales
Facilidad para definir arquitecturas más complejas
