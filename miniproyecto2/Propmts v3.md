
Prompt

# Context
This is a project to put in practice the RNN to process natural language.

# Goal
Develop a model based on RNN using torch, to predict with high accuracy the sentiment about a movie, that can be 0 (Negative) or 1 (Positive).

# Dataset
Contains the description review and the label, get it here /home/jaime/Projects/repos/maia-tdl/tdl/miniproyecto2/movie.csv

# What you will do
1. Create an ipynb script named miniproyecto2_draft_2.ipynb.
2. Keep code as simple as possible, nothing fancy, the comments in plain spanish, no adjectives.
3. Create cells to:
- Imports.
- Load the data set.
- Show sample of the data set.
- Calculate the distribution of categories 0,1.
- Check for any imputable row.
- Pipeline to clean and tokenize the text, clean stopwords for english, WordNetLematizer, GloVe pretrained.
4. Split data set in training, validation and test.
5. Dataset:
    - Longer squences, create indexes with max lengt of 300 to have more context when the review is long.
    - Fine tune the embeddings by freezing the initial epochs and unfreezing them later.
    - Use num_workers=4 for the data loaders.
    - Use batch size of 128.
5. Create a RNN using LSTM bidirectional, include layers:
    - Embeding.
    - Recurrents, with dimsion of 128.
    - Output dense layer with sigmoid function, calculating and average of the hidden states to get the relevant tokens in any position fo the review.
    - Generate a view of the RNN architecture using only the standar functions.
6. Train the model:
    - Early stopping, monitoring val_loss and stop when the model is not improving any more.
    - Use Learning rate scheduler ReduceLROnPlateau.
    - Use gradient clipping, torch.nn.utils.clip_grad_norm_ with max_norm=1.0 to stabilize the training.
    - Include precission, recall and F1-score metrics.

# Coding standard

- Include # type and docstring per function and classes, make it short, no adjectives, but meaningful.
- When extending the framework classes and overwriting functions add short comment describing the purpose.
- Include a doc cell describing the cleaning and tokenization cell, include samples of the input vs the output.

# Paper

The goal is generate a paper about the project, in two diferent files format with the same content:
- Guidelines
    - The base directory is /home/jaime/Projects/repos/maia-tdl/miniproyecto2
    - Use latex and docx templates in /home/jaime/Projects/repos/maia-tdl/miniproyecto2/paper_template, to generate the following files:
        - miniproyecto2_paper_5.docx
        - miniproyecto2_paper_5.pdf (from latex).
    - Follow the templates, do not include additional sections, e.g. Abstract.
    - Do not modify the template files, instead create new ones.
    - Use the code, results, analysis in /home/jaime/Projects/repos/maia-tdl/miniproyecto2/miniproyecto2_documentado.ipynb, aka "the notebook", as the main reference.
    - Write in plain Spanish, reduce the use of adjectives and fancy wording.
    - The paper is max 3 pages, page 1 and 2 with the content and the third page is only for references.
    - Consider the feedbak from the previous project, be aware it was a different problem and CNN instead of RNN, similar approach though: /home/jaime/Projects/repos/maia-tdl/miniproyecto1/feedback_paper.txt.
    - Do not include snippets code in the paper, better explain the approach or the purpose of the code.
    - Take into account the general guidelines for the paper in the templates.
    - Label the tables as Tabla #., use arabic numbers.
    - Label figures as Fig. #., use arabic as well.
    - Enumerate the references in the same order they appear in the article.
- Content:
    Title
        Clasificación de Sentimientos de Reseñas de Películas en IMDb con Redes Neuronales Recurrentes
    Authors
        Yezid Garcia, código: 200810710
        Juan Martin Santos, código: 202013610
        Jaime Rodriguez, código: 200717791
    Introduction
        Describe the problem to solve.
        Describe the content in the paper.
    Methodologoy
        High level description of the methodlogy.
        Mention  the metrics
        Do not include code, if needed, describe what the piece of code makes
        Mention the train, test, validation data sets, and percentages
    Quantitative results
        High level description of the experiment.
        Describe results
        Include comparison between different models/configurations
    Qualitative results
        Based on the notebook's ones.
    Dicussions
        Use continuous and fluent wording, do not split the dicussion in sections, mention the limitations and future work as part of the wording.
        Include the references.
    References
        Take care of the enumeration of the references, in the same order they appear in the paper.
        In the paper use the references in /home/jaime/Projects/repos/maia-tdl/miniproyecto2/references.txt.

Go
