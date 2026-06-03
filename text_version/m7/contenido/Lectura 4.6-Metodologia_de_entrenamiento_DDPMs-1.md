Modelos de difusión | Metodología de entrenamiento
Metodología de entrenamiento
de un Modelo Probabilístico de
Difusión
Problema de aprendizaje
El objetivo de un modelo de difusión es generar datos sintéticos realistas, que se parezcan a los datos
de entrenamiento. Para hacer esto, tomamos una gran cantidad de datos con los que vamos a
entrenar, por ejemplo, imágenes. Si tenemos muchas imágenes, podemos pensar que estas
imágenes son todas muestreadas de una distribución que llamamos 𝑞(𝑥 ). Podemos considerar que
0
esta distribución modela las probabilidades de obtener una imagen pueda venir de nuestra base de
datos. Es decir, imágenes que ‘tienen sentido’ tienen altas probabilidades de ocurrencia, mientras
que imágenes no estructuradas como el ruido tienen bajas probabilidades de ocurrencia.
En principio, no conocemos esta distribución 𝑞(𝑥 ). Sólo tenemos una cantidad finita de muestras de
0
esta distribución que son nuestros datos de entrenamiento. Además, esta distribución puede ser
extremadamente compleja. Por ejemplo, para imágenes podríamos modelar una distribución en
dimensión 256x256x3, la cual sería altamente compleja. Los modelos probabilísticos de difusión nos
ayudan entonces a estimar esta distribución durante el proceso de entrenamiento. Una vez tengamos
una aproximación de 𝑞(𝑥 ), podremos tomar muestras de esta distribución y obtener imágenes
0
nuevas sintéticas, que en cierto sentido se parecerán a las imágenes de entrenamiento.
El proceso de difusión forward
El modelamiento de los procesos de difusión nos ayudará a aproximar esta distribución 𝑞(𝑥 ) de la
0
siguiente forma. Recuerde que en el proceso forward lo que hacemos es tomar uno de nuestros
datos que hemos asumido que son una muestra de la distribución 𝑞(𝑥 ), esto lo denotamos como
0
1
Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

Modelos de difusión | Metodología de entrenamiento
𝑥 ~𝑞(𝑥 ). Luego, por medio del proceso forward, corrompemos esta muestra con ruido en pasos
0 0
iterativos y generamos una secuencia de imágenes 𝑥 ,𝑥 ,…,𝑥 donde 𝑥 termina siendo una imagen
0 1 𝑇 𝑇
que es virtualmente ruido puro. Recuerde que esto lo modelamos de manera precisa como:
𝑞(𝑥 |𝑥 )=𝒩(𝑥 ; √1−𝛽 𝑥 , 𝛽𝐼). Es decir, conocemos exactamente la distribución que nos
𝑡 𝑡−1 𝑡 𝑡 𝑡−1 𝑡
modela qué imagen obtenemos en el tiempo 𝑡, dado que conocemos qué imagen tenemos en
tiempo 𝑡−1. En la Figura 1 se muestra de forma gráfica qué sucede con el proceso forward.
.
Figura 1. Durante el proceso forward transformamos la distribución inicial de los datos 𝑞(𝑥 ) que
0
puede ser muy compleja en una distribución normal estándar 𝑞(𝑥 ) que es más sencilla.
𝑇
Mientras avanzamos en el proceso forward y vamos añadiendo más ruido, vamos transformando la
distribución 𝑞(𝑥 ) en una distribución más sencilla. Como al final del proceso forward obtenemos
0
una imagen 𝑥 que es prácticamente ruido, decimos que esta última imagen sigue una distribución
𝑇
normal estándar. Esto lo denotamos como 𝑥 ~𝑞(𝑥 ), donde 𝑞(𝑥 )=𝒩(𝑥 ;0,𝐼).
𝑇 𝑇 𝑇 𝑇
El proceso reverso de difusión
La estrategia para aproximar 𝑞(𝑥 ) consistirá en aprender cómo ‘devolvernos’ por los caminos que
0
traza el proceso forward. Es decir, queremos partir de una imagen que sea ruido puro 𝑥 muestreada
𝑇
2
Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

Modelos de difusión | Metodología de entrenamiento
de 𝑞(𝑥 ) y ‘revertir’ el proceso forward. Es decir, generar una secuencia de imágenes 𝑥 ,𝑥 ,...,𝑥
𝑇 𝑇 𝑇−1 0
donde vamos quitando el ruido progresivamente siguiendo los caminos reversos del proceso
forward. La última imagen de esta secuencia 𝑥 , será una imagen que ha sido muestreada de la
0
distribución 𝑞(𝑥 ), es decir, una nueva imagen que sigue la misma distribución ideal de nuestros
0
datos. Esto lo podemos garantizar porque quitamos el ruido de una manera muy precisa: siguiendo
el camino reverso del proceso forward. Esto se ilustra en la Figura 2.
Figura 2. Los caminos amarillos ilustran el proceso reverso, en los cuales partimos de un dato
𝑥 muestreado de 𝑞(𝑥 ) y queremos llegar a un dato 𝑥 muestreado de la distribución 𝑞(𝑥 ).
𝑇 𝑇 0 0
Sin embargo, para poder devolvernos por el camino reverso necesitamos conocer el kernel reverso.
Es decir, necesitamos conocer las distribuciones 𝑞(𝑥 |𝑥 ) que nos indican cómo devolvernos por el
𝑡−1 𝑡
camino inverso. Sin embargo, no conocemos estas distribuciones y por eso necesitamos una forma
de aproximarlas.
Aproximación del proceso reverso de difusión
El poder de los modelos de difusión consiste en que no añadimos mucho ruido en un solo paso, si
no que añadimos muy poco ruido en cada paso, eventualmente realizando muchos pasos. El efecto
acumulativo de todas estas pequeñas cantidades de ruido es lo que hace que la imagen final 𝑥 sea
𝑇
prácticamente ruido puro. Sin embargo, en un paso individual del proceso hemos añadido muy poco
3
Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

Modelos de difusión | Metodología de entrenamiento
ruido, por lo que intuitivamente es más fácil predecir ‘cuál es el ruido que debemos quitar en ese
paso’. Es decir, es más fácil modelar la distribución reversa en un solo paso 𝑞(𝑥 |𝑥 ) que es la
𝑡−1 𝑡
distribución que queremos aproximar. Esto nos motiva la siguiente aproximación:
Proponemos aproximar a 𝑞(𝑥 |𝑥 ) con una distribución gaussiana que llamamos 𝑝 (𝑥 |𝑥 ) y que
𝑡−1 𝑡 𝜃 𝑡−1 𝑡
va a depender de un parámetro 𝜃. Es decir, 𝑝 (𝑥 |𝑥 )=𝒩(𝑥 ; 𝜇 (𝑥 ,𝑡), 𝛴 (𝑥 ,𝑡)). Esto significa
𝜃 𝑡−1 𝑡 𝑡−1 𝜃 𝑡 𝜃 𝑡
que 𝑝 (𝑥 |𝑥 ) va a seguir una distribución gaussiana con media 𝜇 (𝑥 ,𝑡) y con matriz de covarianza
𝜃 𝑡−1 𝑡 𝜃 𝑡
𝛴 (𝑥 ,𝑡). Estos parámetros de esta distribución van a depender a su vez del parámetro 𝜃. Nuestro
𝜃 𝑡
objetivo ahora será encontrar el parámetro 𝜃 que mejor nos ayude a aproximar la distribución
𝑞(𝑥 |𝑥 ) y así tendremos que 𝑝 (𝑥 |𝑥 )≈ 𝑞(𝑥 |𝑥 ).
𝑡−1 𝑡 𝜃 𝑡−1 𝑡 𝑡−1 𝑡
Una vez encontremos este parámetro, tendremos finalmente una aproximación la distribución ideal
de los datos 𝑞(𝑥 ) dada por 𝑝 (𝑥 ) que será la distribución de los últimos datos de nuestra secuencia
0 𝜃 0
inversa aproximada. Es decir, la distribución de los datos, después de que les quitamos el ruido con
nuestras aproximaciones 𝑝 (𝑥 |𝑥 ).
𝜃 𝑡−1 𝑡
Problema de optimización y función de pérdida
Como en todo problema de aprendizaje profundo, queremos encontrar una función de pérdida.
Como nuestro problema fundamental es que nuestra aproximación de 𝑝 (𝑥 ) sea lo más cercana a
𝜃 0
𝑞(𝑥 ), necesitamos una medida de ‘qué tan distintas son dos distribuciones de probabilidad’. Una de
0
estas nociones es la Divergencia de Kullbalck-Leibler o Divergencia KL entre dos distribuciones. Esta
cantidad se denota como:
𝐷 (𝑞(𝑥 ) || 𝑝 (𝑥 )).
𝐾𝐿 0 𝜃 0
Por ahora, es suficiente pensar que esta cantidad mide ‘qué tan lejos’ están dos distribuciones. Por
lo tanto, esta es precisamente la cantidad que queremos minimizar. Queremos que 𝑝 (𝑥 ) y 𝑞(𝑥 )
𝜃 0 0
estén lo más cerca posible.
Tras una serie de simplificaciones, es posible mostrar que esta ecuación se simplifica drásticamente
y que esencialmente el problema se reduce a encontrar el parámetro 𝜃 que minimice la distancia
entre las distribuciones 𝑝 (𝑥 |𝑥 ) y 𝑞(𝑥 |𝑥 ,𝑥 ). Es decir, que para cada paso de nuestro proceso
𝜃 𝑡−1 𝑡 𝑡−1 𝑡 0
reverso queremos que nuestra aproximación de ese paso reverso 𝑝 (𝑥 |𝑥 ) sea lo más cercana a el
𝜃 𝑡−1 𝑡
verdadero paso reverso 𝑞(𝑥 |𝑥 ,𝑥 ) cuando ya conocemos 𝑥 . Esto hace que ahora, nuestro
𝑡−1 𝑡 0 0
proceso de aprendizaje sea más sencillo, pues recuerde que no conocemos 𝑞(𝑥 |𝑥 ), pero cuando
𝑡−1 𝑡
condicionamos esta distribución a 𝑥 , es como si tuviéramos una ‘referencia’ hacia donde llegar. Es
0
4
Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

Modelos de difusión | Metodología de entrenamiento
decir, tomamos una imagen 𝑥 de nuestra base de datos y la usamos como referencia para guiar el
0
proceso inverso. No conocemos exactamente el camino inverso que debemos aproximar, pero por
lo menos, sabemos a qué punto queremos llegar. Y como tenemos tantos datos, podemos explotar
esta propiedad para entrenar nuestro modelo. Esta idea se ejemplifica en la Figura 3.
Figura 3. Los caminos amarillos ilustran el proceso reverso cuando tenemos una imagen de
referencia 𝑥 .
0
Siguiendo los caminos reversos
Se puede mostrar, que esta distribución reversa real para la cual tenemos una referencia
𝑞(𝑥 |𝑥 ,𝑥 ) sí la conocemos, la podemos parametrizar y también es una gaussiana. Se puede
𝑡−1 𝑡 0
mostrar que podemos caracterizar esta distribución como
𝑞(𝑥 |𝑥 ,𝑥 ) = 𝒩(𝑥 ; 𝜇̃(𝑥 ,𝑥 ), 𝛴̃(𝑡)).
𝑡−1 𝑡 0 𝑡−1 𝑡 0
Donde la media de esta distribución 𝜇̃(𝑥 ,𝑥 ) depende únicamente de los parámetros 𝛽 que
𝑡 0 𝑡
definimos para el proceso forward y de 𝑥 y 𝑥 donde 𝑥 va a ser una muestra de nuestro conjunto
0 𝑡 0
de datos y 𝑥 es esa misma muestra tras ser contaminada por ruido en el tiempo 𝑡. De igual forma, la
𝑡
matriz de covarianza de esta distribución 𝛴̃(𝑡) depende únicamente de los parámetros 𝛽 del proceso
𝑡
forward y del tiempo 𝑡.
5
Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

Modelos de difusión | Metodología de entrenamiento

Como queremos que 𝑝 (𝑥 |𝑥 ) y 𝑞(𝑥 |𝑥 ,𝑥 ) estén lo más cerca posible y sabemos que ambas
|     | 𝜃 𝑡−1 𝑡 | 𝑡−1 𝑡 0 |     |     |
| --- | ------- | ------- | --- | --- |
son distribuciones gaussianas, el problema se reduce a que sus medias y matrices de covarianza sean
lo más parecidas posible. Empecemos por las matrices de covarianza:
Como 𝛴̃(𝑡) únicamente depende del tiempo y de los parámetros 𝛽, podemos hacer que la matriz
𝑡
|                    | ) sea exactamente 𝛴̃(𝑡). Es decir, hacemos 𝛴 |     | ,𝑡)= 𝛴̃(𝑡) y así ya  |     |
| ------------------ | -------------------------------------------- | --- | -------------------- | --- |
| de covarianza de 𝑝 | 𝜃 (𝑥 𝑡−1 |𝑥 𝑡                                |     | 𝜃 (𝑥 𝑡               |     |
encontramos la matriz de covarianza para 𝑝 (𝑥 |𝑥 ) que mejor aproxima a la matriz de covarianza
𝜃 𝑡−1 𝑡
| de 𝑞(𝑥 |𝑥 ,𝑥 ).   |     |     |     |     |
| ----------------- | --- | --- | --- | --- |
| 𝑡−1 𝑡 0           |     |     |     |     |
Para hallar la media 𝜇 𝜃 (𝑥 𝑡 ,𝑡) de 𝑝 𝜃 (𝑥 𝑡−1 |𝑥 𝑡 ) que mejor aproxime a 𝜇̃(𝑥 𝑡 ,𝑥 0 ) se puede mostrar es
equivalente a resolver el siguiente problema de optimización (recuerde que esta media depende del
parámetro 𝜃):
1
|     | 𝜃∗ = 𝑎𝑟𝑔𝑚𝑖𝑛  | ‖𝜇 (𝑥 ,𝑡)−𝜇̃(𝑥 | ,𝑥 )‖.  |     |
| --- | ------------ | -------------- | ------- | --- |
𝜃 𝑡 𝑡 0
2𝜎̃(𝑡)2
𝜃
Donde 𝜎̃(𝑡)2𝐼=𝛴̃(𝑡). Esta será nuestra versión final de la función de pérdida. Si logramos hallar el
parámetro 𝜃 que minimice esa cantidad, estaríamos encontrando la distribución 𝑝 (𝑥 |𝑥 ) que
𝜃 𝑡−1 𝑡
| mejor se aproxime a 𝑞(𝑥 | |𝑥 ,𝑥 ).    |     |     |     |
| ----------------------- | ----------- | --- | --- | --- |
|                         | 𝑡−1 𝑡 0     |     |     |     |
|                         |             |     |     |     |

Solución del problema de optimización
Lo que haremos será parametrizar la media 𝜇 (𝑥 ,𝑡) con una red neuronal. Es decir, diseñaremos una
𝜃 𝑡
red neuronal que tome como entradas la imagen ruidosa 𝑥  y el tiempo 𝑡 y la red neuronal intentará
𝑡
predecir  el  valor  de  la  media  𝜇 (𝑥 ,𝑡). Luego,  podemos  pensar  que  𝜃  representa  todos  los
𝜃 𝑡
parámetros  de  esta  red  neuronal.  Para  el  caso  de  imágenes,  utilizaremos  una  red  neuronal
convolucional y 𝜃 representará los pesos, sesgos y kernels de esta red neuronal.
Entonces lo que hacemos es lo siguiente: le damos como entrada a nuestra red neuronal una imagen
ruidosa 𝑥  y el tiempo 𝑡. Esta muestra 𝑥  la podemos obtener tomando una muestra 𝑥  de nuestra
| 𝑡   |     | 𝑡   |     | 0   |
| --- | --- | --- | --- | --- |
base datos y aplicarle el proceso forward hasta el tiempo 𝑡. Luego, la red neuronal nos da como
salida un valor estimado de 𝜇 (𝑥 ,𝑡). Luego, como conocemos 𝑥 ,𝑥  y todos los parámetros del
|     | 𝜃 𝑡 |     | 𝑡 0 |     |
| --- | --- | --- | --- | --- |
proceso forward 𝛽, podemos calcular de forma directa los valores de 𝜇̃(𝑥 ,𝑥 ) y de 𝜎̃(𝑡)2 y así,
|     | 𝑡   |     | 𝑡 0 |     |
| --- | --- | --- | --- | --- |
6
Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

Modelos de difusión | Metodología de entrenamiento
podremos calcular la pérdida en la que incurre nuestra red neuronal para esa predicción de 𝜇 (𝑥 ,𝑡)
𝜃 𝑡
utilizando nuestra función de pérdida
1
‖𝜇 (𝑥 ,𝑡)−𝜇̃(𝑥 ,𝑥 )‖.
2𝜎̃(𝑡)2 𝜃 𝑡 𝑡 0
Esto se ilustra en la Figura 4:
Figura 4. La red neuronal toma como entrada un dato contaminado con ruido hasta el tiempo 𝑡 y da
como salida una estimación del valor de 𝜇 (𝑥 ,𝑡). En esta figura 𝜃 representa todos los parámetros
𝜃 𝑡
de la red que pueden ser pesos, sesgos o kernels en una red neuronal convolucional.
Luego, utilizamos los algoritmos de retropropagación y descenso de gradiente para actualizar los
parámetros 𝜃 de la red y repetimos este proceso con toda nuestra base de datos hasta que
disminuyamos lo suficiente nuestra función de pérdida. Tras esto, detenemos el entrenamiento y ya
obtendríamos nuestros parámetros 𝜃 que hacen que 𝜇̃(𝑥 ,𝑥 ) y 𝜇 (𝑥 ,𝑡) estén lo más cerca posible
𝑡 0 𝜃 𝑡
y que por lo tanto 𝑝 (𝑥 |𝑥 ) y 𝑞(𝑥 |𝑥 ,𝑥 ) estén lo más cerca posible que era precisamente lo que
𝜃 𝑡−1 𝑡 𝑡−1 𝑡 0
queríamos. Siguiendo todo el hilo de argumentos, con esto tendremos finalmente una buena
aproximación a la distribución ideal de los datos 𝑞(𝑥 ) dada por 𝑝 (𝑥 ).
0 𝜃 0
7
Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

Modelos de difusión | Metodología de entrenamiento
Bibliografía
Ho, J., Jain, A., & Abbeel, P. (2020). Denoising diffusion probabilistic models. Advances in Neural
Information Processing Systems, 33, 6840-6851.
8
Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

Modelos de difusión | Metodología de entrenamiento
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
9
Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.