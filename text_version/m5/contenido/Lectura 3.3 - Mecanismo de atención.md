Fundamentos de Transformers para NLP | Mecanismo de autoatención

Mecanismo de autoatención en
los Transformers para el
Procesamiento de Lenguaje
Natural

Los Transformers, como modelos de  aprendizaje  automático, se  fundamentan en un mecanismo

esencial llamado autoatención o atención de múltiples cabezas (multi-head attention en inglés).

Este mecanismo habilita a los Transformers para capturar las relaciones de dependencia entre las

palabras  en  una  oración,  lo  que,  a  su  vez,  potencia  la  calidad  y  coherencia  de  los  resultados

generados. En esta lectura, vamos a explorar el mecanismo de autoatención en los Transformers y

su  papel  esencial  en  el  procesamiento  de  lenguaje  natural.  Comenzaremos  por  entender  los

conceptos  fundamentales  de  la  atención  y  luego  profundizaremos  en  cómo  los  Transformers

emplean este mecanismo para adquirir representaciones contextuales de las palabras en un texto.

¿Cómo entendemos la atención?

La atención es una capacidad humana que nos permite centrarnos en ciertos elementos y filtrar la

información relevante de un conjunto más amplio. En el contexto del Procesamiento de Lenguaje

Natural, la atención se refiere a la capacidad de asignar importancia a diferentes partes de una

oración para comprender y generar texto.

Mecanismo de autoatención

El mecanismo de autoatención en los Transformers se basa en la idea de que cada palabra en una

oración puede "atender" a otras palabras para obtener información relevante. En lugar de depender

únicamente de contextos locales, como las ventanas de contexto fijas utilizadas en otros modelos,

los  Transformers  permiten  que  cada  palabra  atienda  a  todas  las  demás  palabras  de  la  oración,

generando así una mejor representación contextual.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

1

Fundamentos de Transformers para NLP | Mecanismo de autoatención

Para  entender  el  mecanismo  de  autoatención  iniciaremos  defiendo  los  siguientes  elementos:

consultas (Q), llaves (K) y valores (V). Las consultas (Q) se pueden entender como una pregunta que

cada palabra hace a las demás.  Las llaves (K) se puede pensar como la lista de palabras con las que

la palabra que se analiza se puede comparar. Finalmente, los valores (V) se pueden relacionar con

guardar la información clave de la palabra de análisis. Estas partes (Q, K y V) se utilizan para ayudar

a entender cómo se relacionan todas las palabras en la oración.

Figura 1. Transformación para la creación de las consultas (Q), llaves (K) y valores (V) para un

conjunto de tokens que ya tienen representación numérica y posicional.

Para cada palabra de  una  oración se  calculan las consultas (Q), llaves (K) y valores (V).  Estos tres

elementos  se  representan  como  vectores  de  características  y  se  generan  a  través  de

transformaciones  lineales  independientes  de  las  palabras  originales.  Dado  que  no  es  posible

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

2

Fundamentos de Transformers para NLP | Mecanismo de autoatención

analizar las palabras en su formato de texto, se utiliza su representación en tokens la cual es numérica

y posicional.  En la Figura 1 se ilustra cómo las palabras se transforman en estas partes clave. En la

figura se utilizó como ejemplo la oración “Cuando juegas muchos videojuegos”, la cual tiene una

codificación  en  una  matriz  de  tamaño  4x4.  Particularmente,  en  este  ejemplo  se  utiliza  una

transformación de 3 capas. Es decir, la codificación numérica y posicional original se multiplica por

una matriz de pesos de tamaño 4x3 específica para las consultas, llaves y valores.  Como resultado,

se tendrán matrices de 4x3 que almacenan las consultas, llaves y valores de cada palabra.

Figura 2. Cálculo de los pesos de atención utilizando las consultas (Q) y la transpuesta de las llaves

(K).

Una vez que hemos calculado las matrices de consulta (Q), llaves (K) y valores (V) para toda la oración

utilizamos estos  valores en cálculos adicionales para determinar cómo se  relacionan las palabras

entre sí y para obtener una representación contextual de la oración en su conjunto. En un segundo

paso, calculamos los coeficientes de la matriz de atención, conocidos como pesos de atención. Este

cálculo se realiza mediante el producto escalar entre la matriz de consulta y la versión transpuesta

de  la matriz de  claves, seguido de  aplicar la función  softmax para normalizar estos pesos. Como

resultado, la matriz de atención contiene valores de peso que indican la relevancia relativa de las

palabras en función de su similitud con la consulta. Las palabras más relevantes tienen pesos más

altos, lo que permite obtener una representación contextual más precisa en base a esta importancia

relativa. La representación visual de este proceso se ilustra en la Figura 2.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

3

Fundamentos de Transformers para NLP | Mecanismo de autoatención

En el tercer paso se combinan los valores (V) ponderándolos según los pesos de atención obtenidos

en el paso previo. Esta combinación se realiza calculando la suma ponderada de los valores (V) para

cada palabra. Es decir, la matriz de pesos de atención se multiplica matricialmente con los valores

(V).  Una  representación  visual  de  este  cálculo  se  ilustra  en  la  Figura  3.  El  resultado  es  una

representación  contextualizada  de  cada  palabra,  que  captura  la  información  relevante  de  las

palabras vecinas en función de su importancia relativa.

Figura 3. Cálculo de los valores filtrados con los pesos de atención y los valores (V)

Al unir los tres pasos que se han presentado previamente, llegamos a la ecuación de autoatención.

Esta fórmula se utiliza para calcular la representación contextual de una palabra en función de su

relación con las demás en la oración. La fórmula se puede expresar de la siguiente manera:

𝐴(𝑄, 𝐾, 𝑉) = 𝑠𝑜𝑓𝑡𝑚𝑎𝑥 (

𝑄𝐾𝑇

√𝑑𝑘

) 𝑉.

En la ecuación 𝐴 en función de (𝑄, 𝐾, 𝑉) representa la autoatención, 𝑄 las consultas, 𝐾 las llaves, 𝑉

los valores, y el término √𝑑𝑘 es un factor de escalamiento, con 𝑑𝑘 la dimensión de las llaves.

Es fundamental comprender que el mecanismo de autoatención se aplica en múltiples ocasiones

dentro  de  un  modelo  Transformer.  Cada  ejecución  de  este  proceso  se  denomina  "cabeza  de

atención". Los Transformers tienen la flexibilidad de usar múltiples cabezas de atención en paralelo,

es  decir  de  manera  simultánea,  lo  que  les  permite  aprender  diversas  representaciones  de  las

palabras desde  diferentes enfoques. Esta característica enriquece  la capacidad del modelo para

capturar relaciones semánticas complejas desde varias perspectivas.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

4

Fundamentos de Transformers para NLP | Mecanismo de autoatención

Además,  para  abordar  la  captura  de  relaciones  de  largo  alcance,  se  introduce  el  concepto  de

atención  con  ventana.  En  lugar  de  considerar  todas  las  palabras  de  la  oración,  se  restringe  el

alcance de  la atención  a un conjunto  predefinido de  palabras vecinas. Esto se  logra  mediante  la

incorporación  de  máscaras  que  especifican  qué  palabras  tienen  permiso  para  influir  en  otras

palabras  en  una  posición  determinada.  La  atención  con  ventana  permite  encontrar  un  equilibrio

entre la complejidad computacional y la captura de dependencias a larga distancia, sin sacrificar la

capacidad de modelar relaciones locales.

El mecanismo de autoatención en los Transformers ha demostrado ser una herramienta altamente

efectiva en el procesamiento de lenguaje natural. Al permitir que cada palabra interactúe con todas

las demás en una oración, los Transformers capturan de manera precisa y exhaustiva las relaciones

tanto  sintácticas  como  semánticas  entre  las  palabras.  Este  enfoque  ha  impulsado  mejoras

sustanciales en diversas aplicaciones del Procesamiento de Lenguaje Natural, como la traducción

automática, la generación de texto y el análisis de sentimientos, entre otras áreas.

Conclusión

En esta lectura, hemos explorado a fondo el mecanismo de autoatención en los Transformers para

el Procesamiento de Lenguaje Natural. La autoatención permite  que cada palabra interactúe con

todas  las  demás  en  una  oración,  lo  que  resulta  en  representaciones  contextuales  altamente

enriquecidas.  Este  mecanismo  ha  sido  fundamental  en  el  éxito  de  los  modelos  basados  en

Transformers en una amplia variedad de tareas de Procesamiento de Lenguaje Natural.

El  entendimiento  de  cómo  opera  la  autoatención  en  los  Transformers  proporciona  bases  para

abordar desafíos en el Procesamiento de Lenguaje Natural y explorar investigaciones futuras en este

campo  que  está  en  constante  evolución.  Los  Transformers  y  su  mecanismo  de  autoatención

continúan impulsando avances significativos en el campo del Procesamiento de Lenguaje Natural,

y su comprensión es esencial para aprovechar plenamente el potencial de la  Inteligencia Artificial

en el análisis y generación de texto.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

5

Fundamentos de Transformers para NLP | Mecanismo de autoatención

Bibliografía

Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., ... & Polosukhin, I. (2017).

Attention is all you need. Advances in neural information processing systems, 30.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

6

Fundamentos de Transformers para NLP | Mecanismo de autoatención

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

