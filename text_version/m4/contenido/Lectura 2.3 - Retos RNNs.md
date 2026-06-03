Redes neuronales recurrentes | Retos

Retos de las redes neuronales
recurrentes

Una de las mayores ventajas de las redes neuronales recurrentes (RNN) es que son especialmente

aptas  para  el  procesamiento  de  datos  secuenciales/temporales,  como  precios  de  acciones,

secuencias  de  video  y  el  procesamiento  de  lenguaje  natural.  Sin  embargo,  el  entrenamiento  de

estas redes conlleva varios desafíos. Uno de los principales es el problema de los gradientes que

desaparecen o explotan durante el proceso de entrenamiento. A continuación, vamos a profundizar

en cada uno de estos retos.

Desvanecimiento del gradiente

El desvanecimiento del gradiente es un problema común en la optimización de redes neuronales,

que  se  produce  cuando  los  gradientes  se  vuelven  cada  vez  más  pequeños  a  medida  que  se

propagan hacia las capas anteriores de la red. Este fenómeno se debe en parte al uso de funciones

de activación no lineales como la función sigmoide, que tienen una derivada que oscila entre 0 y

0.25. A medida que se propagan los gradientes a través de la red, las derivadas se multiplican y, por

lo  tanto,  los  gradientes  se  vuelven  cada  vez  más  pequeños.  Esto  puede  hacer  que  las  capas

anteriores de la red tengan un impacto cada vez menor en la actualización de los pesos, lo que limita

la capacidad de la red para aprender patrones complejos.

El problema del desvanecimiento del gradiente es especialmente relevante en las redes neuronales

recurrentes (RNN), que se utilizan comúnmente para procesar datos temporales. En estas redes, las

entradas se procesan secuencialmente, y la salida de cada paso de tiempo se utiliza como entrada

para el siguiente paso de tiempo. Esto significa que los gradientes se propagan hacia atrás a través

del tiempo, lo que puede agravar el problema del desvanecimiento del gradiente. Si los gradientes

se vuelven cada vez más pequeños a medida que se propagan hacia atrás en el tiempo, las capas

anteriores de la red pueden tener un impacto cada vez menor en la actualización de los pesos, lo

que limita la capacidad de la red para aprender patrones complejos a largo plazo.

Existen varias técnicas que  se  han propuesto para abordar el problema del desvanecimiento del

gradiente en las redes neuronales recurrentes. Una de las más populares es la red de memoria a

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

1

Redes neuronales recurrentes | Retos

largo plazo (LSTM), que utiliza puertas para controlar el flujo de información a través de la red. Estas

puertas permiten que la red almacene información relevante durante varios pasos de tiempo, lo que

ayuda  a  mitigar  el  problema  del  desvanecimiento  del  gradiente.  Otra  técnica  popular  es  la  red

neuronal de memoria a corto plazo (GRU), que es similar a la LSTM, pero utiliza menos parámetros.

Además de estas técnicas específicas de arquitectura, también existen técnicas de optimización que

se pueden utilizar para abordar el problema del desvanecimiento del gradiente. Por ejemplo, el uso

de técnicas de normalización como la normalización por lotes o la normalización por capas puede

ayudar a estabilizar el entrenamiento y evitar que los gradientes se vuelvan demasiado grandes o

demasiado pequeños. También se pueden utilizar técnicas de regularización como la eliminación

aleatoria o la eliminación de peso para reducir la complejidad de la red y limitar la propagación de

gradientes indeseados.

Explosión de gradientes

La  explosión  de  gradientes  es  el  problema  opuesto  al  desvanecimiento  de  gradientes.  Sucede

cuando el valor del gradiente se vuelve extremadamente grande durante el entrenamiento de la

red neuronal, lo  que  hace que  los pesos se  actualicen en grandes magnitudes y se  produzca un

comportamiento  inestable  de  la  red.  Este  problema  es  especialmente  común  en  RNNs  con

retroalimentación  de  corto  plazo,  donde  los  pesos  de  las  conexiones  recurrentes  se  multiplican

repetidamente en el tiempo, lo que puede provocar que los valores del gradiente se disparen.

Al  igual  que  con  el  desvanecimiento  de  gradientes,  la  explosión  de  gradientes  puede  provocar

problemas de aprendizaje y una mala generalización. Si los valores de los gradientes son demasiado

grandes,  la  red  puede  actualizar  sus  pesos  agresivamente  y  terminar  divergiendo  en  lugar  de

converger  a  una  solución  óptima.  Esto  puede  ser  especialmente  problemático  en  RNNs  que  se

utilizan  para  tareas  de  predicción,  donde  un  modelo  inestable  puede  producir  predicciones

incorrectas y ser perjudicial para el rendimiento general del sistema.

Una de las formas más comunes de abordar el problema de la explosión de gradientes es mediante

el  recorte  de  gradientes.  El  recorte  de  gradientes  es una  técnica  que  limita  el  valor  máximo  del

gradiente durante el entrenamiento para evitar que los valores se vuelvan demasiado grandes. El

recorte de gradientes se puede implementar en varios puntos durante el proceso de entrenamiento,

como después de calcular el gradiente, después de normalizar el gradiente o después de actualizar

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

2

Redes neuronales recurrentes | Retos

los pesos. Al limitar los valores del gradiente, se puede reducir la probabilidad de que se produzca

una explosión de gradientes y mejorar la estabilidad del modelo.

Otra  forma  de  abordar  el  problema  de  la  explosión  de  gradientes  es  mediante  el  uso  de

arquitecturas  de  red  más  complejas,  como  las  redes  neuronales  recurrentes  LSTM  y  GRU.  Estas

arquitecturas  tienen  conexiones  recurrentes  con  compuertas  que  controlan  la  cantidad  de

información que se almacena en la memoria a largo plazo de la red, lo que puede ayudar a mitigar

los  efectos  de  la  explosión  de  gradientes  y  mejorar  el  rendimiento  del  modelo.  Además,  estas

arquitecturas  también  pueden  incluir  técnicas  como  el  apagado  aleatorio  y  el  dropout  para

regularizar el modelo y prevenir el sobreajuste.

Bibliografía

Graves, A., & Graves, A. (2012). Long short-term memory. Supervised sequence labelling with recurrent neural

networks, 37-45.

Chung, J., Gulcehre, C., Cho, K., & Bengio, Y. (2014). Empirical evaluation of gated recurrent neural networks on

sequence modeling. arXiv preprint arXiv:1412.3555.

Ioffe,  S.,  &  Szegedy,  C.  (2015,  June).  Batch  normalization:  Accelerating  deep  network  training  by  reducing

internal covariate shift. In International conference on machine learning (pp. 448-456). pmlr.

Ba, J. L., Kiros, J. R., & Hinton, G. E. (2016). Layer normalization. arXiv preprint arXiv:1607.06450.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

3

Redes neuronales recurrentes | Retos

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

