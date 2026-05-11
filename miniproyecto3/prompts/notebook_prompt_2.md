# Context

This is a project to put in practice the RNN to process natural language.


# Goal

- Create a transformer-based model able to classify news text in four categories: "Sport", "Bussiness", "Politics", "Tech", etc.
- The project description is in /home/jaime/Projects/repos/maia-tdl/miniproyecto3/Miniproyecto_3.pdf

# Dataset

Get the data set using this:
kagglehub.dataset_download("jacopoferretti/bbc-articles-dataset")

This are the dataset features: 
- text
- labels
- no_sentences
- flesch reading ease score
- dale-chall readability score
- text_rank_summary
- lsa_summary

The dataset has 5 categories:
- business
- entertainment
- politics
- sport
- tech


# What you will do

## Create an ipynb script named miniproyecto3_2.ipynb.

- Ceate the script /home/jaime/Projects/repos/maia-tdl/miniproyecto3/notebook/miniproyecto3_2.ipynb
- Use as guide the notebook, now on named as sample_notebook: /home/jaime/Projects/repos/maia-tdl/m5/LaboratorioTransformersDeLenguajeV3/release/Laboratorio1TransformersDeLenguajeV3/LaboratorioTransformersDeLenguajeV3.ipynb
- Keep code as simple as possible, nothing fancy, the comments in plain spanish, no adjectives.

## Add a doc header doc cell, following this:
```
# Miniproyecto: Clasificación Multi-Etiqueta de Artículos de Noticias de la BBC usando Transformers

**Curso:** Técnicas de Deep Learning  

**Dataset:** "jacopoferretti/bbc-articles-dataset" (Kaggle) — 2225 documentos, 5 clases

**Grupo:** 24

**Integrantes:** Jaime Rodriguez, Juan Martin Santos, Yezid Garcia

## Descripción del problema

Se necesita desarrollar un modelo basado en transformers capaz de clasificar textos de noticias en cuatro categorias como "Sport", "Bussiness", "Politics", "Tech", entre otros. Para esto se toma como base el data set de Kaggle "The BBC Articles Dataset with Extra Features" curado por Jacopo Ferretti.

## Tabla de contenido

1. [](#1)
...
```

## Add a doc cell for imports, following:
```
## 1. Importación de Librerías y Configuración

<<Generate here a single paragraph describing the needed librearies>>
```

## Add a code cell for imports

## Add a doc cell for describing the dataset, follofing this:
```
# Dataset

<<Describe here how to get the dataset, accordingly to the instruction in the next section, also describe the dataset.>>
```

## Add the needed code cells to download the data set

- Use: kagglehub.dataset_download("jacopoferretti/bbc-articles-dataset")
- Load the data set. Target the file bbc_text_cls.csv by name from the downloaded path, do not rely on file order.
- Show sample of the data set.
- Show the distribution of categories.
- Check for any imputable row.


## Add a doc cell for text processing follofing this:
```
# Procesamiento de texto

<<Describe here how to process the text, accordingly to the instruction in the next section.>>

```

## Add the needed code cells for text processing

- Pipeline to clean and tokenize the text:
    - Clean the text.
    - Tokenize, use padding and masking, for this follow the sample_notebook section 4, as a reference.
    - Prepare sequences using pretrained-BERT-derived embeddings.
    - Make sure the text and labels are in the proper format for a multi-class classification model.
- In the BBCDataset class, pre-tokenize all texts in __init__ using batch tokenization. Do not tokenize in __getitem__.

## Create a Transformer architecture

The architecture will have two blocks:
- The first one to process the trained, using DistilBERT
- The second one will predict the category.

Generate a doc cell following this:
```
# Implementación de la Arquitectura de Transformers

<<Generate a short but complete description of the architecture accordingly to the instruction in the current and following related sections.>>
```

## Transformer architecture, load the pretrained DistilBERT model

- Follow the sample_notebook section 3.


## Transformer architecture, create a first block to preprocess the text

- Follow sample_notebook section 5.


## Transformer architecture, create the second block to predict the category

- Use the method BertForSequenceClassification available in the transformers library.
- Use softmax as activation function.

## Generate a view of the RNN architecture using only the standard functions.

## Training and evaluation of the model

Create a doc cell describing this process accordingly with the instructions in the next section.

```
#Entrenamiento y Evaluación del Modelo

<<Description of the training process.>>
```

## Training and evaluation of the model, code

- Split data set in training, validation and test.
- Train the model usng the training data set.
- Train the model for 5 epocs.
- Use a linear learning rate scheduler with warmup (10% of total steps).
- Apply gradient clipping (max_norm=1.0) before each optimizer step.
- Save the model checkpoint with the best validation loss.
- Evaluate it with the test dataset.
- Include a section (doc and code cells) to show the training curves

### Cuantitative results

Generate a doc cell following this:
```
# Resultado cuantitativo

<<Discribe the results per metric in a table and describe the results in a short paragraph>>
```

### Generate the code cell to print the results

- Report the results, include precission, recall and F1-score metrics.
- Include a precision analysis per category, highlight what categories the model behaves better of worse.

## Generate a doc cell with Cualitative analysis

Include the improvements from the version 1 of the notebook /home/jaime/Projects/repos/maia-tdl/miniproyecto3/notebook/miniproyecto3_1.ipynb
Icnlude the meta-improvements of the project based on the changes the current version of the promt vs /home/jaime/Projects/repos/maia-tdl/miniproyecto3/prompts/notebook_prompt_1.md

Follow this:
```
# Análisis cualitativo

<<Mention this is the the second version of the project notebook and write a general description of the differences between version a 1 and 2.>>

**<<Conclusion summary>>.** <<short but meaningful description>>.
...

```


# Coding standard
- When extending the framework classes and overwriting functions add short comment describing the purpose.
- Include # type and docstring per function and classes, make it short, no adjectives, but meaningful.
- In code cells, for the comments use the simplest wording and no special characeters as accent marks.
- Include a doc cell describing the cleaning and tokenization cell, include samples of the input vs the output.

Go!
