
Prompt

# Context
This is a project to put in practice the RNN to process natural language.

# Goal
Develop a model based on RNN using torch, to predict with high accuracy the sentiment about a movie, that can be 0 (Negative) or 1 (Positive).

# Dataset
Contains the description review and the label, get it here /home/jaime/Projects/maia/local/tdl/miniproyecto2/movie.csv

# What you will do
1. Create an ipynb script named miniproyecto2_draft.ipynb.
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
    - Longer squences, create indexes with max lengt of 400 to have more context when the review is long.
    - Fine tune the embeddings by freezing the initial epochs and unfreezing them later.
5. Create a RNN using LSTM bidirectional, include layers:
    - Embeding.
    - Recurrents, with dimsion of 256.
    - Output dense layer with sigmoid function, calculating and average of the hidden states to get the relevant tokens in any position fo the review.
    - Generate a view of the RNN architecture.
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

The goal is generate a paper abuot the project:
- Use latex template in /home/jaime/Projects/maia/local/tdl/miniproyecto2/paper_template
- Do not modify the template files, instead create new ones, the paper file name is miniproyecto2_paper
- Use a script to extract the needed images as RNN architecure, training curves, etc.
- Write in plain Spanish.
- Reduce the use of adjectives and fancy wording.
- Use the results and code implemented in the /home/jaime/Projects/maia/local/tdl/miniproyecto2/miniproyecto2_draft.ipynb
- The paper is max 2 pages and the references go in the third page.

Go
