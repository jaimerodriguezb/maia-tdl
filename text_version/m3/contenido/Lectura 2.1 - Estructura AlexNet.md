Estructura de una Red Neuronal Convolucional | AlexNet

Estructura de una Red Neuronal
Convolucional: AlexNet

El nacimiento del aprendizaje profundo

En 2010 se realizó la primera versión de la competición ImageNet Large Scale Visual Recognition

Challenge  (ILSVRC),  un  reto  de  clasificación  basado  en  el  conjunto  de  datos  ImageNet  el  cual

contiene 1.2 millones de imágenes distribuidas en 1000 categorías [1]. En esta competencia la tarea

de  clasificación era de  alta complejidad, por  esta razón, la evaluación del rendimiento se  realizó

utilizando una métrica conocida como "error top 5", que medía la frecuencia con la que la categoría

correcta  no  se  encontraba  entre  las  cinco  predicciones  con  mayor  confianza  del  modelo.  Esta

competencia  se  celebró  anualmente  desde  el  2010  hasta  el  año  2017,  en  el  año  2012,  un  hito

significativo ocurrió cuando Geoffrey Hinton y Alex Krizhevsky presentaron la arquitectura AlexNet.

Este  modelo  logró  un  rendimiento  excepcional,  con  un  error  top  5  del  15.3%,  mientras  que  el

segundo clasificado obtuvo un error del 26.2%. Este logro marcó un punto de inflexión en el campo

de la visión por computadora.

La arquitectura de AlexNet

Figura 1.  Diagrama de la arquitectura AlexNet. Adaptado de (LearnOpenCV, 2018).

1

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

Estructura de una Red Neuronal Convolucional | AlexNet

La arquitectura AlexNet, propuesta por Alex Krizhevsky, Ilya Sutskever y Geoffrey Hinton, marcó un

avance importante en el campo de las redes neuronales convolucionales. Este modelo consta de un

total  de  8  capas,  con  la  mayoría  de  ellas  siendo  capas  convolucionales,  seguidas  de  3  capas

completamente  conectadas.  Las  funciones  de  actividación  empleadas  en  las  capas  de  AlexNet

corresponden  a    funciones  tipo  ReLU  (Rectified  Linear  Unit),  estos  elementos  incluyen  las  no

linealidades  del  modelo.    En  la  Figura  1  se  puede  detallar  un  diagrama  esquematico  de  la

arquitectura  AlexNet,  se  detalla  la  dimensión  de  las  capas  y  el  tipo  de  capa,  a  continuación  se

describen en mayor detalle algunos elementos de esta arquitectura.

Entrada y salida del modelo

AlexNet,  diseñada  para  el  reto  ILSVRC,  recibe  imágenes  de  entrada  de  dimensiones  256x256

pixeles. Para garantizar este tamaño de imagen, previamente los datos son escalados y recortados

para ajustarse a la resolución. Además, AlexNet recibe imágenes a color, es decir, imágenes con 3

canales: rojo, verde y azul. En caso de que la imagen de ingreso sea a blanco y negro (únicamente

1 canal), el canal de intensidad se replica para obtener los 3 canales de color.

La  imagen  de  256x256  pixeles  se  recorta  aleatoriamente  hasta  obtener  un  cuadro  de  227x227

pixeles; esto se hace con el objetivo de aumentar el número de datos disponibles. A pesar de que

las imágenes puedan ser muy similares, las pequeñas modificaciones en el recorte le permiten al

modelo  comprender  que,  a  pesar  de  que  haya  leves  desplazamientos  en  la  imagen,  esta  sigue

perteneciendo a la misma categoría. El aumento de datos es clave para prevenir el fenómeno de

sobreajuste (overfitting), en el cual el modelo aprende los patrones del conjunto de entrenamiento

de forma excelente, pero sus predicciones no son generalizables al probarlo con datos nuevos.

Capas convolucionales y completamente conexas

En la Figura 1 observamos un bosquejo de la arquitectura, en la parte superior izquierda se observa

el inicio de la red, en donde la entrada tiene dimensiones de 227x227x3 pixeles, representando el

tamaño de la imagen y los tres canales de color. Posteriormente, es posible observar una serie de

parámetros  incluidos  en  la  parte  superior  del  conector  flecha,  estos  parámetros  caracterizan  y

resumen los elementos más relevantes de la capa situada en seguida. En la primera capa, se puede

observar que  se  menciona la abreviatura  CONV, esto  hace referencia  a  que  es  una capa de  tipo

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

2

Estructura de una Red Neuronal Convolucional | AlexNet

convolucional. También se puede notar el escrito 11x11, el cual hace referencia al tamaño del filtro

utilizado para la convolución (que será de 11x11x3 debido a que hay 3 canales). El parámetro stride,

incluido también en la caracterización de capa, indica el número de pixeles que se desplaza el filtro

luego de realizar cada operación de convolución, para la primera capa convolucional son 4 pixeles.

Finalmente, el número de filtros (o kernels) indica la cantidad de filtros con pesos entrenables que

se  utilizan  en  la  capa,  en  este  caso  son  96.  El  número  de  filtros  en  una  capa  convolucional  se

convertirá en la profundidad de la siguiente capa. La siguiente ecuación permite calcular el tamaño

de salida de la capa denotado como 𝑜𝑢𝑡𝑝𝑢𝑡𝑆𝑖𝑧𝑒:

𝑜𝑢𝑡𝑝𝑢𝑡𝑆𝑖𝑧𝑒 =   (

𝑖𝑛𝑝𝑢𝑡𝑆𝑖𝑧𝑒 − 𝑘𝑒𝑟𝑛𝑒𝑙𝑆𝑖𝑧𝑒
𝑠𝑡𝑟𝑖𝑑𝑒

) + 1.

En la ecuación 𝑖𝑛𝑝𝑢𝑡𝑆𝑖𝑧𝑒 corresponde a la dimensión de la entrada de la capa de entrada de la capa

(227 en este caso), el tamaño del filtro se denota como 𝑘𝑒𝑟𝑛𝑒𝑙𝑆𝑖𝑧𝑒 y corresponde a 11 y 𝑠𝑡𝑟𝑖𝑑𝑒 es 4.

De  esta  forma,  podemos  obtener  que  el  tamaño  de  salida  es  de  55x55x96,  debido  a  que  se

utilizaron 96 kernels.

Adicionalmente,  las  capas  convolucionales  pueden  incluir  padding,  operación  en  la  cual  se

adicionan pixeles en el dato de entrada antes de pasar por la capa convolucional. Esto suele hacerse

para mantener las dimensiones espaciales tras la convolución. En el caso de AlexNet, se utiliza un

padding de 1, es decir, se añaden pixeles en el borde de la entrada una vez. El valor de los pixeles

para esta arquitectura es de cero.

En la Figura 1 también se encuentran los términos como FC, Max POOL y Softmax. FC significa Fully

Connected o completamente conectado en español. Estas capas suelen encontrarse en el final de

la red y  se  caracterizan por  presentar neuronas que  aplican la transformación lineal en todos los

elementos del vector de entrada. Es decir, cada elemento de la salida de una capa completamente

conectado estuvo influenciado por la totalidad del vector de entrada.  El término Max POOL señala

la implementación de una capa de Max Pooling, capa que realiza una operación especial detallada

más adelante, mientras que Softmax indica que se emplea esta función de activación sobre la capa

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

3

Estructura de una Red Neuronal Convolucional | AlexNet

de salida, lo cual permite convertir las salidas de la última capa en una distribución de probabilidad

para completar la tarea de clasificación.

Max Pooling

La operación de Max Pooling se utiliza para disminuir la resolución espacial de la imagen mientras

se mantiene la profundidad de la red. Para esto, se toma una ventana con un tamaño definido, por

ejemplo,  3x3,  y  se  toma  como  resultado  de  la  operación  el  valor  más  alto  de  la  ventana.  A

continuación, se presenta un ejemplo en el cual se tiene una ventana de 3x3 con diferentes valores

numéricos y se reduce al seleccionar el máximo valor.

3

5

  6

8

7

9

4

4

0

9

En el caso de AlexNet, utilizaron Max Pooling sobrelapado, es decir, escogieron un stride de 2 para

un tamaño de  filtro 3x3, lo que  causa  que  una columna del filtro se  sobre  lape con la operación

anterior en cada iteración.

ReLU

Por  otro lado,  recordemos que  la función de  activación no lineal  evita que  toda la red se  pueda

expresar como una única combinación lineal. AlexNet utiliza la función de activación Rectified Linear

Unit (ReLU) después de la salida de cada capa para este fin. La función de activación ReLU convierte

todos los números negativos en cero, mientras que  aplica la identidad en los números positivos.

Esta función se  aplica en todas las capas de AlexNet menos, como se explicó previamente, en la

capa de salida, en la cual se fija como función de activación Softmax.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

4

Estructura de una Red Neuronal Convolucional | AlexNet

Aprendizaje por transferencia o Transfer Learning

Una gran ventaja de las CNN es que podemos entrenarlas para un problema particular utilizando

una  estrategia  conocida  como  Transfer  Learning.  El  Transfer  Learning  consiste  en  tomar  una

arquitectura de CNN, como por ejemplo AlexNet, que ya ha sido preentrenada en un conjunto de

datos grande, y luego ajustar sus parámetros a una tarea diferente  pero relacionada para la cual

tenemos pocos datos de entrenamiento. Esto se conoce como sintonización fina o fine-tuning. En

lugar  de  entrenar  una  CNN  desde  cero,  se  aprovecha  el  conocimiento  y  las  características

aprendidas por la red en el conjunto de  datos original para mejorar el rendimiento en una tarea

específica. Esto ahorra tiempo y recursos, ya que no es necesario entrenar una red completa, y suele

dar como resultado modelos de CNN más efectivos para la nueva tarea.

Conclusiones

AlexNet es una arquitectura de red neuronal convolucional pionera en el campo de la visión por

computadora. Esta arquitectura revolucionó el rendimiento en tareas de clasificación de imágenes,

principalmente  en  el  conjunto  de  datos  ImageNet.  AlexNet  incluye  elementos  como  capas

convolucionales,  capas  completamente  conectadas  y  capas  de  Max  Pooling,  además  del  uso  de

funciones de  activación tipo ReLU y  Softmax en su capa de  salida, todos estos elementos se han

convertido en pilares fundamentales en el diseño de arquitecturas de CNN posteriores. El éxito de

esta arquitectura promovió el uso e investigación en arquitecturas de redes neuronales profundas,

y  sentó  las  bases  para  desarrollos  futuros  en  el  campo,  en  particular  en  el  área  de  visión  por

computadora.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

5

Estructura de una Red Neuronal Convolucional | AlexNet

Bibliografía

Nayak S. (2018). Understanding AlexNet. [Internet]. Tomado de LeanOpenCV.

Hinton, G. E., Krizhevsky, A., & Sutskever, I. (2012). Imagenet classification with deep convolutional

neural networks. Advances in neural information processing systems, 25(1106-1114), 1.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

6

Estructura de una Red Neuronal Convolucional | AlexNet

©  -  Derechos  Reservados:  la  presente  obra,  y  en  general  todos  sus
contenidos,  se  encuentran  protegidos  por  las  normas  internacionales  y
nacionales vigentes sobre propiedad Intelectual, por lo tanto su utilización
parcial  o  total,  reproducción,  comunicación  pública,  transformación,
distribución, alquiler, préstamo público e importación, total o parcial, en todo
o en parte, en formato impreso o digital y en cualquier formato conocido o
por conocer, se encuentran prohibidos, y solo serán lícitos en la medida en
que  se  cuente  con  la  autorización  previa  y  expresa  por  escrito  de la
Universidad de los Andes.

De  igual  manera,  la  utilización  de  la  imagen  de  las  personas,  docentes  o
estudiantes, sin su previa autorización está expresamente prohibida. En caso
de  incumplirse  con  lo  mencionado,  se  procederá  de  conformidad  con los
reglamentos y políticas de la universidad, sin perjuicio de las demás acciones
legales aplicables.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

7

