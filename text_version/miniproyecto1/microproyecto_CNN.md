Clasificación de MRI con Redes Neuronales Convolucionales para Tipos de

Cáncer

La resonancia magnética (MRI) desempeña un papel fundamental en la detección y

clasificación  de  los  diferentes  tipos  de  cáncer  cerebral.  La  aplicación  de  redes

neuronales convolucionales (CNN) ha incrementado notablemente la precisión en la

interpretación  de  estos  volúmenes,  al  ser  entrenadas  para  reconocer  patrones  y

características  distintivas  asociadas  a  cada  tipo  de  tumor.  Las  resonancias

magnéticas  (MRI)  generan  volúmenes  tridimensionales  compuestos  por  múltiples

capas, donde cada una corresponde a una imagen bidimensional del tejido analizado.

Procesar  un  volumen  completo  implica  manejar  una  gran  cantidad  de  datos

simultáneamente,  lo  que  puede  ser  computacionalmente  costoso  y  requerir

considerable tiempo y recursos. Para este proyecto se trabajará exclusivamente con

imágenes  individuales  extraídas  de  las  capas  de  los  MRI,  en  lugar  de  procesar  el

volumen  completo. Esta estrategia simplifica la tarea al transformar  el problema en

una  clasificación  de  imágenes  bidimensionales,  reduciendo  significativamente  la

carga computacional.

Redes Neuronales Convolucionales

Las  CNN  son  especialmente  adecuadas  para  el  análisis  de  imágenes  debido  a  su

capacidad para captar características locales a través de convoluciones. Estas redes

pueden  ser  entrenadas  para  clasificar  las  imágenes  extraídas  de  los  MRI  en  cuatro

categorías: glioma, meningioma, pituitary (hipófisis) y tejido sano. Por ejemplo:

-  Glioma: Detecta masas anómalas con bordes irregulares y heterogeneidad en

el tejido cerebral.

-  Meningioma: Identifica tumores bien delimitados originados en las meninges.

-  Pituitary: Clasifica adenomas hipofisarios en la región selar.

-  Tejido sano: Diferencia el tejido cerebral normal sin anomalías presentes.

Procesamiento de Imágenes

El  procesamiento  de  imágenes  mediante  redes  neuronales  convolucionales  (CNN)

involucra múltiples capas de convolución, activación y pooling, que permiten extraer y

analizar  características  relevantes  de  las  imágenes.  Estas  técnicas  facilitan  una

distinción  precisa  entre  distintos  tipos  de  tumores  y  el  tejido  sano,  mejorando  la

exactitud del diagnóstico médico.

Ventajas y Aplicaciones

Implementar  CNN para la clasificación de las  imágenes extraídas de  los MRI ofrece

varias ventajas:

-  Eficiencia en el diagnóstico: Acelera el proceso de evaluación de imágenes,

permitiendo  a  los  profesionales  médicos  enfocarse  en  otros  aspectos  del

tratamiento.

-  Consistencia  en  la  clasificación:  Proporciona  una  clasificación  uniforme  y

precisa, reduciendo la variabilidad entre evaluadores.

-  Asistencia  para  profesionales  menos  experimentados:  Ofrece  una

herramienta valiosa para radiólogos en formación o con menos experiencia.

-  Mejora  en  la  calidad  del  diagnóstico:  Optimiza  la  detección  temprana  y  el

tratamiento adecuado de diferentes tipos de cáncer cerebral.

A.  Objetivo

-  Desarrollar un método basado en redes neuronales convolucionales que permita

clasificar con exactitud imágenes extraídas de MRIs en una de las 4 categorías.

B.  Conjunto de datos

-  Los datos corresponden a un dataset de 7023 imágenes extraídas de MRIs tomados

desde distintos ángulos y disponibles para dominio público. El dataset es accesible

en el siguiente enlace.

C.  Actividades por realizar

1.  Preparación  de  las  imágenes  para  el  entrenamiento  y  prueba  del  modelo.

Construya  un  pipeline  para  cargar  las  imágenes  y  dividirlas  en  conjuntos  de

entrenamiento y prueba.

2.  Desarrollo de la arquitectura de red neuronal convolucional para clasificación

de las imágenes de MRI en una de las 4 categorías. La arquitectura es de libre

elección, se recomienda utilizar bloques de convolución y max pooling o usar

redes existentes y hacerles finetunning para este problema.

