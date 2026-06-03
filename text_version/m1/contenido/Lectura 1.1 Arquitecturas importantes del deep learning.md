Arquitecturas importantes del Deep Learning

Arquitecturas importantes del
Deep Learning

A continuación, haremos una breve descripción de algunas de las arquitecturas más importantes

del Deep Learning.

Redes neuronales convolucionales

Una de las arquitecturas importantes en Deep Learning son las redes neuronales convolucionales o

CNNs por sus siglas en inglés. El término "red neuronal convolucional" indica que la red emplea

una  operación  matemática  llamada  convolución.  La  convolución  es  un  tipo  especializado  de

operación  lineal  que  filtra  la  información  y  extrae  características  de  los  datos  para  "ayudar"  al

modelo a encontrar patrones ocultos en la información. El éxito de las redes convolucionales está

en las capas convolucionales, que actúan como una 'lupa inteligente', escaneando la información y

detectando  patrones  simples  en  las  capas  iniciales,  como  por  ejemplo  bordes  y  texturas  en  una

imagen. Luego, otras capas convolucionales agrupan la información para resaltar las características

más  importantes.  Es  como  si  estuviéramos  capturando  gradualmente  detalles  cada  vez  más

complejos,  desde  líneas  hasta  formas  y  objetos  completos.  Esto  nos  permite  que  la  red

convolucional "aprenda" a reconocer, detectar y clasificar elementos en la información de entrada

de  manera efectiva, extrayendo las características  que  codifican y representan  una estructura de

datos espacial. La Figura 1 muestra un ejemplo de arquitectura de una red neuronal convolucional

usada para clasificación.

Las CNN's han sido particularmente exitosas en tareas de clasificación, segmentación y detección

en  información  como  imágenes,  videos  y  series  de  tiempo.  Podemos  encontrar  aplicaciones  en

áreas  como  el  reconocimiento  facial,  sistemas  avanzados  de  detección  de  objetos  en  vehículos

autónomos y diagnóstico médico a partir de imágenes. Se han empleado en el análisis energético

con mapas solares y estimación agrícola mediante imágenes de cultivos adquiridas por satélites o

drones,  entre  otras  aplicaciones.  También  han  sido  utilizadas  en  procesamiento  de  señales

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

1

Arquitecturas importantes del Deep Learning

unidimensionales. Por ejemplo, monitoreo en tiempo real de electroencefalogramas y en detección

de daño estructural en edificios.

Figura 1.  Ejemplo ilustrativo de la arquitectura de una red neuronal neuronal convolucional.

Redes neuronales recurrentes

Continuamos ahora en las Redes Neuronales Recurrentes, también conocidas como RNN por sus

siglas del idioma inglés. Son también un tipo de red neuronal diseñadas para tratar con información

secuencial  o  dependiente  del tiempo,  a  diferencia  de  las  redes  neuronales  convolucionales  que

tratan  con  información  espacial.   Las  RNNs fueron  diseñadas  para  manejar  datos  secuenciales  al

modelar dependencias temporales. Su capacidad para capturar patrones a lo largo del tiempo y su

adaptabilidad a tareas complejas las convierten en una herramienta valiosa para aplicaciones que

involucran secuencias, y su profundidad juega un papel clave en su capacidad para comprender y

procesar  datos  secuenciales  de  manera  efectiva. La  arquitectura  de  las  RNN  se  identifica  por

presentar las conexiones recurrentes que  permiten tomar decisiones ponderando  la información

previa en el contexto actual. La Figura 2 ilustra la arquitectura de una red neuronal recurrente.

Si consideramos un ejemplo donde la entrada es un párrafo, las RNN no solo analizan cada palabra

individualmente, sino que también capturan cómo las palabras se interconectan. Esto les habilita

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

2

Arquitecturas importantes del Deep Learning

para entender la información previa y la coherencia del texto, lo que se  traduce en  aplicaciones

como la generación automática de subtítulos para videos o la predicción de series de tiempo. Estas

arquitecturas han sido muy exitosas en aplicaciones como procesamiento del lenguaje natural, el

reconocimiento de voz, y predicción de sismos y series de tiempo en general.

Figura 2.  Ejemplo ilustrativo de la arquitectura de una red neuronal recurrente.

Transformers de lenguaje

En 2017 surgieron los Transformers como alternativa a las redes recurrentes para el procesamiento

de lenguaje natural. La novedad de estas arquitecturas es que poseen un mecanismo de atención

que  cuantifica  la  importancia  relativa  de  cada  palabra  de  la  frase  de  entrada  para  asignarle  un

significado global. A diferencia de las RNNs y las CNNs que se basan en estructuras secuenciales o

convolucionales, los Transformers se fundamentan en el concepto de atención.  Esta arquitectura se

ha destacado por su capacidad para capturar relaciones de largo alcance y comprender contextos

complejos en datos secuenciales.

Para  comprender  las  relaciones  entre  palabras  en  oraciones  complejas,  las  arquitecturas  de

Transformers implementan simultáneamente múltiples mecanismos (o cabezas) de auto-atención.

Por ejemplo, al analizar la frase “el animal no cruzó la calle porque él estaba muy asustado” como

se muestra en la Figura 3, para entender el significado del pronombre personal “él”, una cabeza

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

3

Arquitecturas importantes del Deep Learning

enfoca su atención en el antecedente “el animal” y otra en el participio “asustado”. A diferencia de

las RNN, que necesitan pasar información a lo largo de la secuencia paso a paso, los Transformers

pueden considerar toda la secuencia en un solo paso. Y no solo observan su contexto histórico, sino

también evalúan la importancia relativa de los eventos pasados.

Figura 3.  Ejemplo del mecanismo de atención en un Transformer de lenguaje.

Las  aplicaciones  de  las  arquitecturas  Transformers  son  vastas  y  han  dejado  huellas  en  muchos

campos.  Una  de  las  áreas  más  impactantes  es  el  procesamiento  de  lenguaje  natural  (NLP).  Los

Transformers  han  revolucionado  cómo  entendemos  y  generamos  lenguaje.  Desde  traducción

automática  y  chatbots  inteligentes  hasta  la  manipulación  de  objetos  a  través  de  mecanismos

robóticos, estas arquitecturas permiten que las máquinas comprendan y generen texto de manera

cercana a como un humano lo haría.

Transformers de visión

El éxito de los Transformers en el campo del procesamiento del lenguaje natural dio origen a los

Transformers Visuales. Podemos entender a esta arquitectura como una adaptación del mecanismo

de  auto-atención  pero  diseñada  para  establecer  relaciones  ponderadas  y  contextuales  entre

4

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

Arquitecturas importantes del Deep Learning

pequeños 'parches' de una imagen. Estas arquitecturas dividen las imágenes en una secuencia de

parches  para  asemejarse  a  las  palabras  en  una  oración  y  utilizan  la  atención  para  encontrar  las

regiones  de  la  imagen  que  son  más  importantes  para  cada  tarea  específica. Su  capacidad  para

procesar datos visuales de manera similar a cómo los Transformers originales procesan el lenguaje

ha  desencadenado  un  avance  en  tareas  como  la  detección  de  objetos,  la  segmentación  de

imágenes y la generación de contenido visual. Esta adaptación de los Transformers al dominio visual

marca un hito en el Deep Learning y ha abierto puertas a aplicaciones emocionantes.

Redes generativas adversariales

Las  Redes  Generativas  Adversariales,  o GANs  por  sus  siglas  en  inglés,  introducen  una  dinámica

única  en  el  aprendizaje  profundo,  donde  dos  redes  neuronales  una  generadora  y  una

discriminadora compiten en una especie de 'juego' creativo. Imagina a estas redes como un pintor

y un crítico de arte que trabajan juntos para crear y evaluar obras dramáticas, respectivamente. La

red generadora, como el pintor, crea muestras que se asemejan a ciertos datos de entrenamiento,

como  imágenes  de  rostros  humanos  o  paisajes.  La  red  discriminatoria,  como  el  crítico,  intenta

discernir si las muestras provienen del conjunto de datos reales o son creaciones generadas por la

red generadora. A medida que pasa el tiempo el artista mejora su habilidad para engañar al crítico

y el crítico se  vuelve  más perspicaz,  ambos evolucionan y mejoran en su oficio. Este  proceso de

competencia mutua resulta en una mejora constante en la calidad de las muestras generadas.

Este tipo de arquitectura permite la generación de datos estructurados, como las imágenes, esto ha

tenido un impacto significativo en áreas como el diseño gráfico, la moda y la creación de contenido

visual. Además de la generación, las GANs también han encontrado aplicaciones en la manipulación

de imágenes, como la traducción de estilo y la mejora de resolución. Otro campo donde las GANs

se  destacan  es  en  la  creación  de  contenido  audiovisual.  Pueden  generar  videos  y  animaciones

realistas a partir de imágenes fijas, lo que es de gran utilidad en la industria del entretenimiento y la

publicidad.  La  Figura  4  muestra  imágenes  generadas  por  el  generador  de  una  GAN  que  se

asemejan a personas reales.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

5

Arquitecturas importantes del Deep Learning

Figura 4.  Ejemplo de las imágenes generadas artificialmente usando la red generadora

entrenada en una GAN. Ninguna de estas personas es real. Generada a través del portal

https://thispersondoesnotexist.com/ .

Modelos probabilísticos de difusión

Los  modelos  de  difusión,  que  comparten  similitudes  con  el  funcionamiento  de  las  GANs,

desempeñan un papel crucial en la generación de nueva información. En este enfoque, se inicia con

un proceso de difusión que implica la adición gradual de ruido a los datos, como en el caso de una

imagen.  Esta  adición  progresiva  de  ruido  tiene  el  efecto  de  alterar  y  degradar  la  información

original. El modelo probabilístico de difusión, que persigue la creación de contenido  original, se

enfoca  en  el  proceso  contrario:  la  recuperación  de  la  información  original  a  partir  de  su  versión

degradada. A través de este enfoque, se busca modelar cómo los datos originalmente corruptos

pueden ser restaurados y esto genera información original similar a la información de entrada. La

Figura 5 ilustra el proceso de recuperación.

Figura 5.  Ejemplo del proceso de generación en un modelo probabilístico de difusión.

6

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

Arquitecturas importantes del Deep Learning

Bibliografía

Prince,  Simon  J.  D.  (2023).  Understanding  Deep  Learning.  The  MIT  Press.  Disponible  en:

https://udlbook.github.io/udlbook/

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

7

Arquitecturas importantes del Deep Learning

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

8

