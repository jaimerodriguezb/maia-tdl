Inteligencia artificial generativa | Otros modelos

Otras arquitecturas de inteligencia artificial
generativa

Autoencoder variacional - VAE

La  arquitectura  de  red  denominada  Autoencoder  variacional  o  VAE  por  sus  siglas  en  inglés  se

introdujo en el 2013 en el artículo "Auto-Encoding Variational Bayes" por de Kingma y Welling. En

esta arquitectura se utilizan dos redes neuronales profundas: un codificador y un decodificador. El

codificador  aprende  a  reducir  una  entrada  a  una  representación  interna  denominada  espacio

latente,  mientras  que  el  decodificador  aprende  a  reconstruir  la  entrada  a  partir  de  esa

representación interna. Ambas redes aprenden simultáneamente comparando la diferencia entre la

imagen generada de salida y la imagen original de entrada e intentando reducirla. Lo que diferencia

a las VAE de otras arquitecturas similares es que intentan organizar las representaciones internas de

forma  que  el  modelo  sea  capaz  de  generar  algo  nuevo.  Los  VAEs  han  sido  usado  para  generar

imágenes, texto, y audio.

La Figura 1 ilustra el VAE. El objetivo en el VAE es lograr aprender un espacio latente  𝑍 tal que la
salida 𝑋̃ sea lo más parecida a la entrada  𝑋. En el proceso, se aprende las distribuciones 𝑄𝜙(𝑍|𝑋) y
𝑃𝜃(𝑋|𝑍), es decir, la distribución que representa la variable latente  𝑍 a partir de la entrada  𝑋, y la

distribución  que  intenta  representar  𝑋  a  partir  de  la  variable  latente  𝑍.  Usando  esta  última

distribución, podemos generar contenido nuevo.

Figura 1. Diagrama del autoencoder variacional.

1

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

Inteligencia artificial generativa | Otros modelos

Transformer generativo preentrenado - GPT

Los  Transfomers  generativos  preentrenados,  GPTs,  por  sus  siglas  en  inglés,  son  modelos

generativos de lenguaje de gran tamaño (conocidos como LLMs por sus siglas en inglés) basados

en la arquitectura de los Transformers y creados por la empresa OpenAI. Estos modelos son la base

del  reconocido  ChatGPT.  Los  modelos  GPT  usan  solamente  el  bloque  decodificador  de  un

Transformer  de  lenguaje  entrenado  para  predecir  la  siguiente  palabra  en  una  oración,  de  esta

manera  producen  texto  similar  al  generado  por  un  humano.  Estas  arquitecturas  tienen  miles  de

millones  de  parámetros,  y  han  sido  entrenadas  con  cientos  de  billones  de  palabras.  Las

arquitecturas de GPT 1, 2, y 3 pueden recibir como entradas texto, mientras que la arquitectura de

GPT 4 puede recibir como entradas tanto texto como imágenes. De ahí que GPT 4 se denomina

modelo multimodal, es decir, es capaz de procesar e integrar diferentes tipos de información.

Modelos de Lenguaje de Gran Tamaño Meta AI - LLaMA

Es una familia de modelos generativos de lenguaje de gran tamaño creados por la empresa Meta.

Al igual que GPT, la arquitectura de LLaMA está basada en el decodificador de un Transformer de

lenguaje.  Las  principales  características  de  esta  familia  de  modelos  es  su  tamaño  reducido  y

excelente  desempeño  comparado  con  otros  modelos  mucho  más  grandes  como  GPT.  Además,

Meta permite el uso libre de estos modelos para uso académico y comercial.

AudioGEN

Es un modelo generativo creado por la empresa Meta que recibe un texto como entrada y devuelve

un audio como salida. La arquitectura de AudioGEN tiene dos componentes principales:

•  Una estructura que codifica y decodifica audios en la que se define una representación

latente del audio que es discretizada.

•  Una componente basada en el decodificador de un Transformer de lenguaje que opera

sobre esta representación latente de audio y que está condicionado a entradas de texto.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

2

Inteligencia artificial generativa | Otros modelos

Bibliografía

Kingma,  D.  P  &  Welling,  M.    Dosovitskiy  (2013).  Auto-Encoding  Variational  Bayes.  arXiv  preprint

arXiv:1312.6114.

OpenAI: GPT 4 Technical Report. https://cdn.openai.com/papers/gpt-4.pdf  .

Touvron, H, et. al. (2023). LLaMA: Open and Efficient Foundation Language Models. arXiv preprint

arXiv:2302.13971.

Kreuk,  F,  et.  al.

(2023)  AudioGEN:  Textually  Guided  Audio  Generation.  arXiv  preprint

arXiv:2209.15352v2.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

3

Inteligencia artificial generativa | Otros modelos

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

4

