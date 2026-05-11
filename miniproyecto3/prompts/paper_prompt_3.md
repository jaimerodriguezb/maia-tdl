# Paper

The goal is generate a paper about the project:
- Concept/implementation matching
    - Understand the papers mentioned in /home/jaime/Projects/repos/maia-tdl/m5/content/Lecturas-Recomendados-de-la-semana-5.pdf
    - Find the matching points with this project and the notebook, and use them when needed in the paper.
    - Take care of the enumerating the references, in the same order they are cited in this paper.
- Guidelines
    - Use latex template in /home/jaime/Projects/repos/maia-tdl/miniproyecto3/paper/latex_template
    - The paper file is /home/jaime/Projects/repos/maia-tdl/miniproyecto3/paper/miniproyecto3_paper_X where X is the version, matching this prompt file sufix _X (now on, this is the suffix_rule).
    - Follow the templates, do not include additional sections, e.g. Abstract.
    - Do not modify the template files, instead create new ones.
    - Use the code, results, analysis in /home/jaime/Projects/repos/maia-tdl/miniproyecto3/notebook/miniproyecto3_X.ipynb (follow the suffix_rule), aka "the notebook", as the main reference.
    - Extract from the notebook the images for model architecture, tables, training curves; save them in /home/jaime/Projects/repos/maia-tdl/miniproyecto3/paper
    - Write in plain Spanish, reduce the use of adjectives and fancy wording.
    - The paper is max 3 pages, page 1 and 2 with the content and the third page is only for references.
    - Do not include snippets code in the paper, better explain the approach or the purpose of the code.
    - Consider the feedbak from the previous project, be aware it was a different problem and CNN instead of RNN, similar approach though: /home/jaime/Projects/repos/maia-tdl/miniproyecto1/feedback_paper.txt.
    - Label the tables as Tabla #., use arabic numbers.
    - Label figures as Fig. #., use arabic as well.
    - To get "Tabla #" table captions in ieeeconf: the class controls table labels via \fnum@table (NOT \tablename — \tablename has no effect). Outside a class/package file, @ is not a letter, so \fnum@table requires \makeatletter. Use this block in the preamble:
        \makeatletter
        \AtBeginDocument{%
          \def\fnum@table{Tabla~\thetable}%
          \renewcommand{\thetable}{\arabic{table}}%
        }
        \makeatother
      Without \makeatletter, \def\fnum@table silently defines \fnum instead (@ terminates the command name), and the fix has no effect.
    - Compile the .tex file twice with pdflatex. The first pass writes citation keys to the .aux file; the second pass resolves them. A single compile always shows [?] instead of citation numbers.
- Paper content:
    Title
        Clasificación Multi-Etiqueta de Artículos de Noticias de la BBC usando Transformers
    Authors
        Yezid Garcia, código: 200810710
        Juan Martin Santos, código: 202013610
        Jaime Rodriguez, código: 200717791
    Introduction
        Describe the problem to solve.
        Describe the content in the paper.
    Methodologoy
        Start with a high level description of the methodlogy, something like this: "Para el desarrollo del proyecto se siguió el ciclo tradicional de aprendizaje automático: entendimiento del problema, recopilación y preparación de los datos, diseño y entrenamiento del modelo, evaluación sobre un conjunto de prueba independiente, y análisis de los resultados obtenidos."
        Mention  the metrics.
        Do not include code, if needed, describe what the piece of code makes.
        Show the model architecture based on the notebook.
        Mention the train, test, validation data sets, and percentages.
    Quantitative results
        High level description of the experiment.
        Describe results.
        Include the training curves from the notebook.
        Include comparison between different models/configurations.
    Qualitative results
        Based on the notebook's ones.
    Dicussions
        Use continuous and fluent wording, do not split the dicussion in sections, mention the limitations and future work as part of the wording.
        Include the references.
    References
