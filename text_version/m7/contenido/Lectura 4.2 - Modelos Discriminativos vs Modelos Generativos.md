Modelos Discriminativos vs Modelos Generativos

Modelos Discriminativos vs
Modelos Generativos

En el campo de  la Inteligencia Artificial (IA), existen diferentes enfoques y técnicas para abordar

problemas de  aprendizaje  automático. Dos enfoques clave  son los modelos  discriminativos y los

modelos generativos. En esta lectura, exploraremos en detalle los conceptos y características de los

modelos discriminativos y generativos, y analizaremos sus fortalezas y debilidades.

Modelos discriminativos

En el campo del aprendizaje automático, los modelos discriminativos son modelos utilizados para

clasificar y separar datos en diferentes categorías o clases.  Estos modelos se centran en aprender

la  frontera  que  define  las  regiones  asociadas  a  cada  categoría  en  el  espacio  de  características.

Desde una perspectiva probabilística, esto se puede ver como el aprendizaje de la distribución de

probabilidad  de  las  categorías  condicionada  en  la  observación  de  las  características.  El  objetivo

principal  de  los  modelos  discriminativos  es  determinar  la  relación  entre  las  características  y  las

etiquetas para realizar clasificaciones precisas.

Un ejemplo común de modelo discriminativo es la regresión logística. Esta técnica obtiene un plano

separador y se utiliza ampliamente en problemas de clasificación binaria y multiclase. Otro ejemplo

popular son las máquinas de vectores de soporte (SVM), que también se utilizan para la clasificación

y pueden manejar tanto problemas lineales como no lineales. Los árboles de decisión son otro tipo

de modelo discriminativo que utiliza estructuras jerárquicas para realizar clasificaciones.

Una de las principales características de los modelos discriminativos es su enfoque en la frontera de

decisión. Estos modelos aprenden a trazar un límite que separa las diferentes clases en el espacio

de  características.  Al  determinar  esta  frontera,  pueden  realizar  clasificaciones  precisas  incluso

cuando las relaciones entre las características y las etiquetas son altamente no lineales.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

1

Modelos Discriminativos vs Modelos Generativos

Los modelos discriminativos se utilizan en una amplia gama de aplicaciones de Inteligencia Artificial.

Por ejemplo, en el reconocimiento de voz, estos modelos pueden clasificar rápidamente las señales

de  audio  en  diferentes  palabras  o  frases.  En  el  reconocimiento  facial,  pueden  determinar  si  una

imagen  contiene  el  rostro  de  una  persona  específica  o  no.  En  el  procesamiento  de  texto,  los

modelos discriminativos son útiles para la clasificación de documentos y la detección de spam.

Modelos generativos

Los modelos generativos son utilizados para modelar la distribución conjunta de las variables de

entrada y salida. Un ejemplo de este tipo de modelos es el clasificador de Bayes, el cual construye

un  clasificador  modelando  la  distribución  conjunta  de  las  variables  de  entrada  y  salida  como  el

producto entre la distribución de las variables de entrada condicionada en la variable de salida y la

distribución a priori de la variable de salida. Interesantemente, los modelos generativos tienen la

capacidad  no  solo  de  realizar  clasificaciones,  sino  también  de  generar  nuevos  datos  que  se

asemejen a los datos de entrenamiento. Dos ejemplos destacados de modelos generativos son las

redes generativas adversariales (GANs) y los modelos probabilísticos de difusión.

Las  GANs  se  componen  de  dos  componentes  principales:  un  generador  y  un  discriminador.  El

generador  crea  muestras  sintéticas  a  partir  de  una  distribución  de  ruido,  mientras  que  el

discriminador  evalúa  la  autenticidad  de  las  muestras  generadas  en  comparación  con  los  datos

reales. Estos dos componentes se entrenan en un juego en el que el generador intenta engañar al

discriminador,  y  el  discriminador  intenta  distinguir  entre  las  muestras  generadas  y  las  muestras

reales. A medida que  se  entrena la GAN, el  generador mejora su capacidad para generar datos

realistas que sigan la distribución de los datos de entrenamiento.

Otro  enfoque  de  modelo  generativo  es  el  modelo  probabilístico  de  difusión.  Estos  modelos  se

basan  en  la  idea  de  que  los  datos  pueden  evolucionar  a  lo  largo  del  tiempo  a  medida  que  se

difunden y se mezclan. Utilizan iteraciones repetidas de procesos de difusión para generar nuevas

muestras.  Estos  modelos  han  demostrado  ser  eficaces  en  la  generación  de  información  de  alta

calidad  y  la  manipulación  controlada  de  información  ya  existente.  Al  permitir  que  los  datos  se

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

2

Modelos Discriminativos vs Modelos Generativos

difundan gradualmente, los modelos de difusión pueden generar muestras que sigan la estructura

y las características de los datos de entrenamiento.

Sin embargo, los modelos generativos también enfrentan desafíos. Por un lado, su entrenamiento

puede ser más complejo y requerir más recursos computacionales en comparación con los modelos

discriminativos. Además, la evaluación de la calidad de las muestras generadas puede ser subjetiva

y requiere técnicas de evaluación específicas. Además, la diversidad y la variabilidad en las muestras

generadas pueden ser desafiantes de controlar.

Discriminativo contra generativo

Enfoque y objetivo

Los modelos discriminativos se centran en aprender la distribución condicional de las variables de

salida (etiquetas) dado un conjunto de variables de entrada (características). Su objetivo principal

es  clasificar  y  separar  datos  en  diferentes  categorías  o  clases.  Los  modelos  discriminativos  se

interesan específicamente en la frontera de decisión que separa las clases y su aprendizaje se enfoca

en encontrar esta frontera de acuerdo con un criterio de optimalidad. Por otro lado, los modelos

generativos  buscan  aprender  la  distribución  conjunta  de  las  variables  de  entrada  y  salida.  Su

objetivo no se limita solo a la clasificación, sino que también pueden generar nuevos datos que sean

similares a los datos de entrenamiento. Los modelos generativos capturan la estructura subyacente

de los datos y su aprendizaje se enfoca en modelar y comprender la distribución completa de los

datos.

Capacidades y limitaciones

Los  modelos  discriminativos  tienen  la  ventaja  de  ser  más  simples  y  más  fáciles  de  entrenar  en

comparación  con  los  modelos  generativos.  Pueden  lograr  un  buen  rendimiento  en  tareas  de

clasificación y regresión, especialmente cuando hay una cantidad suficiente de datos etiquetados

disponibles. Sin embargo, pueden ser sensibles al ruido en los datos y pueden requerir grandes

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

3

Modelos Discriminativos vs Modelos Generativos

conjuntos  de  datos  etiquetados  para  un  aprendizaje  efectivo.  Por  otro  lado,  Los  modelos

generativos tienen la capacidad de capturar la estructura subyacente de los datos y generar nuevos

ejemplos. Estos modelos pueden ser útiles cuando los datos etiquetados son limitados o costosos

de  obtener.  Sin  embargo,  los  modelos  generativos  suelen  ser  más  complejos  y  requieren  más

tiempo de entrenamiento en comparación con los modelos discriminativos. Además, pueden ser

menos precisos en tareas de clasificación pura, ya que su objetivo principal no es solo la separación

de clases, sino también la generación de datos.

Conclusiones

Los modelos discriminativos y los modelos generativos son enfoques complementarios en machine

learning.  Mientras  que  los  modelos  discriminativos  se  centran  en  la  separación  de  clases  y  la

clasificación precisa, los modelos generativos capturan la estructura de los datos y  algunos tienen

la  capacidad  de  generar  nuevos  ejemplos.  La  elección  entre  ambos  enfoques  depende  de  la

naturaleza  del  problema  y  los  objetivos  del  aprendizaje  automático.  En  muchos  casos,  una

combinación  de  ambos  enfoques  puede  ofrecer  un  mayor  rendimiento  y  una  comprensión  más

profunda de los datos. Al comprender las características, aplicaciones, ventajas y limitaciones de los

modelos  discriminativos  y  generativos,  los  investigadores  y  profesionales  de  IA  pueden  tomar

decisiones informadas al abordar problemas de aprendizaje automático.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

4

Modelos Discriminativos vs Modelos Generativos

© - Derechos Reservados: la presente obra, y en general todos sus
contenidos, se encuentran protegidos por las normas internacionales y
nacionales vigentes sobre propiedad Intelectual, por lo tanto su utilización
parcial o total, reproducción, comunicación pública, transformación,
distribución, alquiler, préstamo público e importación, total o parcial, en
todo o en parte, en formato impreso o digital y en cualquier formato
conocido o por conocer, se encuentran prohibidos, y solo serán lícitos en la
medida en que se cuente con la autorización previa y expresa por escrito de
la Universidad de los Andes.

De igual manera, la utilización de la imagen de las personas, docentes o
estudiantes, sin su previa autorización está expresamente prohibida. En
caso de incumplirse con lo mencionado, se procederá de conformidad con
los reglamentos y políticas de la universidad, sin perjuicio de las demás
acciones legales aplicables.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

5

