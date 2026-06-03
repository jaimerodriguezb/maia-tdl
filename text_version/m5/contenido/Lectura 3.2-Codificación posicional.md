Fundamentos de transformers para NLP| Codificación Posicional

Codificación posicional en
Transformers para NLP

En los lenguajes, el orden y la posición de las palabras en una oración son realmente importantes.

El significado completo de la oración puede cambiar si se altera el orden de las palabras. Mientras

que las redes neuronales recurrentes tienen un mecanismo integrado para manejar el orden de las

secuencias  al  implementar  soluciones  de  procesamiento  de  lenguaje  natural  (NLP),  el  modelo

Transformer, por otro lado, no utiliza la recurrencia ni la convolución y trata cada punto de datos de

forma independiente. Por lo tanto, es necesario agregar información posicional explícitamente al

modelo para preservar el conocimiento del orden de las palabras en una oración. La codificación

posicional  es  el  método  mediante  el  cual  se  mantiene  la  información  sobre  el  orden  de  los

elementos en una secuencia.

En esta lectura, vamos a explicar la codificación posicional para los Transformers. Explicaremos qué

es la codificación posicional, por qué es importante y cómo funciona en los Transformers.

¿Qué es la codificación posicional?

La codificación posicional se refiere a la manera en que se asigna una ubicación o posición única

a cada entidad en una secuencia. Existen varias razones por las que un solo número, como el valor

del  índice,  no  se  utiliza  para  representar  la  posición  de  un  elemento  en  los  modelos  de

Transformers.  En  el  caso  de  secuencias  largas,  los  índices  pueden  volverse  demasiado  grandes.

Además, normalizar el valor del índice entre 0 y 1 puede generar problemas cuando se trabaja con

secuencias de longitud variable, ya que se normalizarían de manera diferente.

En cambio, los Transformers emplean un esquema de codificación posicional ingenioso, donde a

cada  posición  o  índice  se  le  asigna  un  vector  específico.  Por  lo  tanto,  la  salida  de  la  capa  de

codificación  posicional  es  una  matriz  en  la  que  cada  fila  representa  un  objeto  codificado  de  la

secuencia combinado con su información posicional.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

1

Fundamentos de transformers para NLP| Codificación Posicional

Capa de codificación posicional en los Transformers

Figura 1. Estructura del Transformer.
 Tomado de: Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., ... & Polosukhin, I.
(2017). Attention is all you need. Advances in neural information processing systems, 30.

En  el  artículo  original  que  introdujo  el  Transformer,  se  presentó  una  estrategia  ingeniosa  para

representar  la  posición  de  cada  elemento  en  una  secuencia  de  entrada.  Esta  representación

posicional es el último paso de procesamiento que se aplica a los datos de entrada antes de pasar

por el bloque  del  encoder, como se  ilustra en la  Figura 1. De  esta manera, cuando los datos se

introducen en el encoder, ya han adquirido relaciones semánticas a través del input embedding y

relaciones de posición mediante el positional embedding. Para comprender mejor cómo funciona

esta representación posicional, suponga que nuestra secuencia de entrada consiste de 7 vectores

𝑒0, 𝑒1, 𝑒2, 𝑒3, 𝑒4, 𝑒5, 𝑒6. Cada uno de estos vectores tiene dimensión 𝑑, pues ya han sido codificados en

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

2

Fundamentos de transformers para NLP| Codificación Posicional

un espacio de  dimensión alta tras pasar por el input embedding.   A cada vector 𝑒𝑝𝑜𝑠 le vamos a

asignar otro vector 𝑃𝑝𝑜𝑠 de la misma dimensión 𝑑. Este vector 𝑃𝑝𝑜𝑠 va a contener la información que

le indica al modelo que el vector 𝑒𝑝𝑜𝑠 se encuentra en la posición número 𝑝𝑜𝑠 de la secuencia. Estos

vectores se calculan de la siguiente forma:

𝑃(𝑝𝑜𝑠,2𝑖) = sin (𝑝𝑜𝑠/10000

2𝑖
𝑑 )

𝑃(𝑝𝑜𝑠,2𝑖+1) = cos (𝑝𝑜𝑠/10000

2𝑖
𝑑 )

La primera ecuación calcula las entradas del vector 𝑃𝑝𝑜𝑠 que están en las posiciones pares, mientras

que  la  segunda  ecuación  calcula  las  entradas  que  están  en  las  posiciones  impares.  Por  eso  los

subíndices son 2𝑖 y 2𝑖 + 1. Veamos por qué se utilizan estas funciones. Si fijamos el valor de 𝑖 en 2 y

pensamos que 𝑝𝑜𝑠 es una variable continua, podemos graficar esa primera curva como una función

de 𝑝𝑜𝑠 :

Figura 2. Cuarta función de posición.

Luego,  tras  evaluar  esta  función  en  𝑝𝑜𝑠 = 0,1,2,3 … ,6  obtendremos  la  cuarta  entrada  de  nuestros

vectores de posición para cada elemento de la secuencia. Es decir, la altura de ese seno codifica la

posición  de  cada  elemento  de  la  secuencia,  pues  elementos  en  posiciones  diferentes  de  la

secuencia tendrán valores de codificación distintos. Sin embargo, hay un problema.  Dado que la

3

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

Fundamentos de transformers para NLP| Codificación Posicional

curva sinusoidal se repite en intervalos, podemos ver en la Figura 2 que 𝑃1,4 y 𝑃4,4 tienen los mismos

valores de codificación, a pesar de estar en dos posiciones muy diferentes (las posiciones 1 y 4 en

la secuencia respectivamente). Aquí es donde entra en juego la parte 𝑖 en la ecuación.

 Si  ahora,  variamos  el  valor  de  𝑖  y  graficamos  las  funciones  resultantes  obtenemos  varias  curvas

sinusoidales de diferentes frecuencias como se muestra en la Figura 3.

.

                                                           Figura 3. Funciones de posición.

La idea detrás de tener varias curvas sinusoidales con diferentes frecuencias es que si tenemos dos

elementos  que  están  muy  cerca  en  la  secuencia,  necesitamos  senos  con  altas  frecuencias  para

detectar que están cerca y que sus valores correspondientes en la curva sinusoidal sean diferentes.

Esto se muestra en la Figura 3 donde podemos ver que para bajas frecuencias a los elementos 𝑒2 y

𝑒4 se  les asigna información posicional muy cercana, mientras que  en altas frecuencias las curvas

sinusoidales les asignan valores posicionales distintos. Cada frecuencia nos ayuda a distinguir qué

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

4

Fundamentos de transformers para NLP| Codificación Posicional

tan  lejos  están  los  elementos  de  la  secuencia.  Esto  nos  ayuda  a  solucionar  el  problema

anteriormente mencionado.

De  esta  forma,  logramos  asignarle  a  cada  vector  𝑒𝑝𝑜𝑠    de  entrada  un  vector  𝑃𝑝𝑜𝑠  que  codifica  la

posición  en  la  que  se  encuentra  ese  elemento  en  la  secuencia.  Por  ejemplo,  en  la  Figura  4  se

muestra el vector posicional que se obtiene para el tercer elemento de la secuencia. Las entradas

en posiciones impares de este vector se calculan de manera similar a las que mostramos, pero con

funciones cosenos.

                  Figura 4. Vectores posicionales.

Codificación Posicional en la práctica

En la práctica, la dimensión de input embedding puede ser muy alta y necesitamos cientos o miles

de funciones sinusoidales para calcular el vector posicional para un elemento de una secuencia. En

la Figura 5 se muestra lo que se conoce como una matriz de codificación posicional, es una forma

visual de representar la codificación posicional cuando estamos trabajando con input embeddings

de dimensiones muy altas o con secuencias de texto muy largas. En el eje x se muestra la posición

5

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

Fundamentos de transformers para NLP| Codificación Posicional

del elemento en la secuencia, en este caso una secuencia de 100 tokens. En el eje y se muestra la

entrada del vector de posición, en este caso tenemos un input embedding de dimensión 300. El

mapa  de  colores  nos  muestra  el  valor  de  la  función  sinusoidal  para  una  entrada  del  vector  de

posición de un elemento que está en una posición dada en la secuencia de palabras. Por eso los

valores en el mapa de color están entre -1 y 1.

                                                   Figura 5. Matriz de codificación posicional

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

6

Fundamentos de transformers para NLP| Codificación Posicional

Bibliografía

Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., ... & Polosukhin, I. (2017).

Attention is all you need. Advances in neural information processing systems, 30.

Saeed,  M.  (2023).  A  gentle  introduction  to  positional  encoding  in  transformer  models,  part  1.

Retrieved  from  https://machinelearningmastery.com/a-gentle-introduction-to-positional-

encoding-in-transformer-models-part-1/

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

7

Fundamentos de transformers para NLP| Codificación Posicional

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

8

