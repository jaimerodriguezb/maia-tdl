Intuición detrás de los Modelos probabilísticos de difusión

Intuición detrás de los Modelos
probabilísticos de difusión

Los  modelos  probabilísticos  de  difusión  están  orientando  el  avance  tecnológico  y  han

revolucionado  la  forma  en  que  abordamos  las  tareas  generativas  complejas  con  Inteligencia

Artificial. Estos modelos se basan en los principios matemáticos de la teoría gaussiana, la varianza,

las  ecuaciones  diferenciales  y  las  secuencias  generativas.  Empresas  líderes  en  tecnología  como

Nvidia, Google, Adobe y OpenAI han situado a los modelos de difusión en el centro de la escena.

Ejemplos  notables  incluyen  DALL.E  21,  Stable  Diffusion2  y  Midjourney3,  están  cambiando

radicalmente el panorama de la generación.

Los modelos de difusión se inspiran en la termodinámica no equilibrada, un concepto de la física

que se relaciona con procesos que no están en equilibrio. Por ejemplo, considera que tienes una

sustancia en un estado ordenado y estable, como un  bloque de hielo. Si gradualmente se aplica

calor  y  agitación  al  bloque  de  hielo  este  comienza  a  volverse  más  caótico  y  desordenado.

Eventualmente,  se  convierte  en  un  líquido,  y  si  continúas  aplicando  calor  y  agitación,  puede

convertirse en un gas aún más caótico.

Este  tipo  de  procesos  se  puede  pensar  como  la  inspiración  de  los  modelos  de  difusión

considerando datos en lugar de sustancias, por ejemplo, datos como imágenes. En los modelos de

difusión  se  comienza  con  datos  altamente  organizados  y  luego  se  agrega  gradualmente  "ruido"

aleatorio, similar al calor y la agitación en la termodinámica, la agregación de ruido se realiza a lo

largo de pasos sucesivos. Como resultado los datos se vuelven cada vez más difíciles de distinguir

y parecen aleatorios.

Luego, estos modelos aprenden a deshacer este proceso de difusión, es decir, a eliminar el ruido y

recuperar  los  datos  originales.  En  esencia,  están  tomando  datos  que  parecen  aleatorios  y

volviéndolos a ordenar de manera significativa. Esto es útil para generar datos deseados a partir de

1 https://openai.com/dall-e-2
2 https://stablediffusionweb.com/
3 https://www.midjourney.com/

1

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

Intuición detrás de los Modelos probabilísticos de difusión

un  estado  inicial  de  "caos"  aparente,  lo  que  puede  tener  aplicaciones  en  la  generación  y

manipulación de información.

Como se presenta en la Figura 1, si tomamos una imagen y le añadimos ruido aleatorio, en este

caso,  ruido  gaussiano,  durante  una  cierta  cantidad  de  pasos,  terminaremos  con  una  imagen

indistinguible que parece ruido aleatorio. Ahora bien, si somos capaces de llegar de una imagen a

ruido gaussiano, podemos pensar en la posibilidad de hacer el proceso contrario, donde a partir

de ruido aleatorio vamos quitando pequeñas cantidades de ruido hasta llegar a una imagen limpia

y realista. El proceso en el que se le añade ruido a la imagen original es conocido como proceso

hacia adelante o forward process en inglés. Por otra parte, el proceso que va quitando ruido poco a

poco hasta llegar a una imagen realista es conocido como proceso inverso o backward process en

inglés.

Proceso “hacia adelante”

Proceso reverso

Figura 1. Representación de un modelo de difusión.

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

2

Intuición detrás de los Modelos probabilísticos de difusión

Bibliografía

Ramesh, A., Dhariwal, P., Nichol, A., Chu, C., & Chen, M. (2022). Hierarchical text-conditional image

generation with clip latents. arXiv preprint arXiv:2204.06125.

Rombach,  R.,  Blattmann,  A.,  Lorenz,  D.,  Esser,  P.,  &  Ommer,  B.  (2022).  High-resolution  image

synthesis  with  latent  diffusion  models.  In Proceedings  of  the  IEEE/CVF  Conference  on

Computer Vision and Pattern Recognition (pp. 10684-10695).

Oppenlaender, J. (2022, November). The Creativity of Text-to-Image Generation. In Proceedings of

the 25th International Academic Mindtrek Conference (pp. 192-202).

Universidad de los Andes | Vigilada Mineducación Reconocimiento como
Universidad: Decreto 1297 del 30 de mayo de 1964.
Reconocimiento personería jurídica: Resolución 28 del 23 de febrero de 1949 Minjusticia.

3

Intuición detrás de los Modelos probabilísticos de difusión

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

4

