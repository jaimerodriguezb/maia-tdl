Redes Generativas Adversarias | Función de pérdida

Metodología de entrenamiento:
Función de pérdida en las Redes
Generativas Adversariales.

Las Redes Generativas Adversariales (GANs, por sus siglas en inglés) han surgido como un marco

poderoso en el campo del aprendizaje automático para generar datos sintéticos realistas y de alta

calidad. Las GANs emplean una  arquitectura  particular que  consiste  en dos redes neuronales, el

generador y el discriminador, las cuales participan en  un proceso de  aprendizaje  competitivo. El

generador  tiene  como  objetivo  producir  muestras  sintéticas  que  se  asemejen  a  datos  reales,

mientras que el discriminador intenta distinguir entre muestras reales y falsas. El éxito de las GANs

depende  de  la  optimización  efectiva  de  estas  dos  redes,  y  en  el  centro  de  esta  optimización  se

encuentra la elección de una función de pérdida adecuada. La función de pérdida sirve como una

métrica orientadora para cuantificar el rendimiento de las redes del generador y el discriminador.

En este texto, nos adentraremos en las complejidades de las funciones de pérdida utilizadas en las

GANs y exploraremos cómo influyen en la dinámica de entrenamiento y la calidad final de la salida.

En el contexto de la red del generador, el objetivo principal es generar muestras sintéticas que sean

indistinguibles de los datos reales. Esto implica la definición de una función de pérdida adecuada

que  cuantifique  la  discrepancia  entre  las  muestras  generadas  y  la  distribución  de  datos  reales.

Exploraremos funciones de pérdida comunes utilizadas en el generador, como la divergencia de

Jensen-Shannon y la distancia de Wasserstein, arrojando luz sobre sus ventajas y limitaciones.

Por  otro lado, la red del discriminador tiene  como  objetivo clasificar correctamente  las muestras

como reales o falsas. Para lograr esto, es crucial utilizar una función de pérdida que guíe de manera

efectiva el proceso de aprendizaje del discriminador. Por esto, examinaremos funciones de pérdida

utilizadas para el discriminador, como la entropía cruzada binaria (cross-entropy loss) y la hinge loss,

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

1

Redes Generativas Adversarias | Función de pérdida

y  aclararemos  cómo  facilitan  el  entrenamiento  del  discriminador  y  contribuyen  a  la  dinámica

adversarial general.

Funciones de pérdida

Figura 1. Ejemplo de una Red Generativa Adversaria (GAN). El generador crea imágenes nuevas
basadas  en  el  conjunto  de  datos  de  entrenamiento,  mientras  que  el  discriminador  aprende  a
diferenciar las imágenes originales de las imágenes generadas.

En  las  GANs,  generador  y  el  discriminador  están  involucrados  en  un  proceso  de  aprendizaje

competitivo, cada una con su propia función de pérdida distintiva. El generador busca minimizar la

función  de  pérdida  asociada  a  la  diferencia  de  las  imágenes  generadas  y  las  imágenes  reales,

mientras que el discriminador busca maximizar su habilidad para discriminar los datos generados

de los reales.  En el primer trabajo donde las GANs fueron presentadas, Ian Goodfellow propone

esta forma de aprendizaje como un juego de dos jugadores conocido en la teoría de juegos como

minimax.  En  este  juego,  el  jugador  correspondiente  al  generador  busca  minimizar  la  diferencia

entre las imágenes generadas y las imágenes reales, y el jugador asociado al discriminador busca

maximizar la habilidad para discriminar los datos generados de los reales. Bajo esta propuesta se

definió  una  función  objetivo  a  minimizar  de  la  cual  se  derivaron  la  función  de  pérdida  para  el

generador  y  la  función  de  pérdida  para  el  discriminador.  Después  del  trabajo  seminal  por

Goodfellow se han propuesto funciones de pérdida más sofisticadas que permiten obtener mejores

resultados de generación, de las cuales listamos algunas a continuación.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

2

Redes Generativas Adversarias | Función de pérdida

Función de Pérdida para el Generador:

El objetivo principal de  la  red del generador en una  GAN es generar muestras sintéticas que  se

asemejen  estrechamente  a  los  datos  reales.  La  función  de  pérdida  del  generador  cuantifica  la

discrepancia entre las muestras  generadas y la distribución de datos reales, proporcionando una

medida de qué tan bien está funcionando el generador. Dos funciones de  pérdida comúnmente

utilizadas para el generador son:

       a) Divergencia de Jensen-Shannon:

 La  divergencia  de  Jensen-Shannon  (JSD)  es  una  elección  popular  de  función  de  pérdida  en  las

GAN. Ésta mide la similitud entre dos distribuciones de probabilidad, y se deriva de otra llamada

Kullback-Leibler. La pérdida de JSD tiene como objetivo minimizar la diferencia entre la distribución

de  las  muestras  generadas y  la  distribución  de  las  muestras  reales.  Minimizar  la  pérdida  de  JSD

alienta al generador a producir muestras que sean indistinguibles de los datos reales.

     b) Distancia de Wasserstein:

 La  distancia  de  Wasserstein  es  otra  función  de  pérdida  utilizada  en  las  GANs.  Proporciona  una

métrica  para  cuantificar  la  disparidad  entre  dos  distribuciones  de  probabilidad.  La  función  de

pérdida  de  la  distancia  de  Wasserstein  alienta  al  generador  a  minimizar  la  diferencia  entre  la

distribución  de  las  muestras  generadas  y  la  distribución  de  los  datos  reales.  Una  ventaja  de  la

distancia  de  Wasserstein  es  que  proporciona  un  paisaje  de  optimización  más  estable  en

comparación  con  otras  funciones  de  pérdida,  mitigando  problemas  como  el  hecho  de  que  el

generador sólo genera un tipo de salida, conocido como problema del colapso del modo (mode

collapse, en inglés).

El  colapso  del  modo  en  una  GAN  ocurre  cuando  el  Generador  se  enfoca  en  generar  muestras

exclusivamente  de  un  conjunto  limitado  de  datos  concentrados  alrededor  de  un  modo  de  la

distribución de los datos, tratando de engañar al Discriminador. Esto resulta en la falta de diversidad

en  las  muestras  generadas,  ya  que  el  Discriminador  eventualmente  lo  descubre  y  el  Generador

cambia a otro modo, repitiendo este ciclo indefinidamente. Esto limita la variedad de las muestras

generadas y reduce la efectividad del Generador para engañar al Discriminador.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

3

Redes Generativas Adversarias | Función de pérdida

Función de Pérdida para el Discriminador:

 La  red  del discriminador  en  una  GAN  tiene  como  objetivo  clasificar  correctamente  las  muestras

como  reales  o  falsas.  La  función  de  pérdida  para  el  discriminador  está  diseñada  para  guiar  su

proceso de aprendizaje al proporcionar una señal para distinguir entre muestras reales y generadas.

Dos funciones de pérdida comúnmente utilizadas para el discriminador son:

    a) Cross-entropy loss:

La Cross-entropy loss es una función de pérdida ampliamente utilizada para tareas de clasificación

binaria, incluido el discriminador en una GAN. Mide la disparidad entre las probabilidades de clase

predichas  y  las  etiquetas  de  verdad.  El  objetivo  del  discriminador  es  minimizar  esta  pérdida,

clasificando correctamente las muestras reales como reales (etiqueta 1) y las muestras generadas

como falsas (etiqueta 0).

    b) Hinge loss:

 La Hinge loss (o pérdida de bisagra) es otra función de pérdida comúnmente utilizada para entrenar

el  discriminador  en  las  GANs.  La  Hinge  loss  fomenta  un  margen  entre  las  predicciones  del

discriminador  para  muestras  reales  y  generadas.  Al  minimizar  la  pérdida  de  bisagra,  el

discriminador busca lograr una separación clara entre las muestras reales y falsas, facilitando una

discriminación más efectiva.

Es importante tener en cuenta que la elección de las funciones de pérdida en las GANs puede variar

según los requisitos específicos de la tarea y las propiedades deseadas de las muestras generadas.

Los investigadores a menudo exploran nuevas funciones de pérdida o variaciones de las existentes

para abordar desafíos específicos y mejorar la dinámica de entrenamiento de las GANs.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

4

Redes Generativas Adversarias | Función de pérdida

Bibliografía

Goodfellow, I., Pouget-Abadie, J., Mirza, M., Xu, B., Warde-Farley, D., Ozair, S., ... & Bengio, Y. (2014).
Generative adversarial nets. Advances in neural information processing systems, 27.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

5

Redes Generativas Adversarias | Función de pérdida

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

6

