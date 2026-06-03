---
markmap:
  colorFreezeLevel: 2
  maxWidth: 320
  initialExpandLevel: 2
---

# ML Techniques
## Acronym: _ML_ <span id="ml-target"></span> = Machine Learning
- Algorithms that improve performance on tasks through experience rather than explicit programming. Encompasses supervised, unsupervised, and reinforcement learning, with deep learning as the dominant sub-field for perception and language tasks.
## Foundations
### History & Biological Inspiration
- description
  - The study of neural computation traces from neuroscience findings in the 1950s–60s, through early artificial models in the 1980s, to the deep learning renaissance triggered by large datasets and GPU compute in the 2010s. Each milestone refined our understanding of how hierarchical feature learning can be implemented in software.
- Wiesel & Hubel — simple vs. complex cells
  - Nobel Prize-winning experiments on cat visual cortex showing that neurons respond selectively to oriented edges (simple cells) and to those edges regardless of position (complex cells). This hierarchical structure directly inspired convolutional neural networks.
- Neocognitron (Fukushima)
  - Fukushima's 1980 architecture introduced alternating feature-extraction and subsampling layers, anticipating the conv–pool pattern of modern [CNNs](#cnns-target). It was the first system to learn position-invariant pattern recognition without explicit supervision.
- Perceptron → Multi-layer networks
  - Rosenblatt's perceptron (1958) was a single-layer linear classifier; adding hidden layers with non-linear activations created the multi-layer perceptron (MLP) capable of learning arbitrary functions. The backpropagation algorithm (1986) made training deep MLPs practical.
- ImageNet moment (2012)
  - AlexNet's top-5 error rate of 15.3% on ImageNet — more than 10 points below the previous best — demonstrated that deep [CNNs](#cnns-target) trained on GPUs vastly outperform hand-crafted feature pipelines. This result sparked the modern deep learning era and redirected the entire field.

### Neural Network Basics
#### Description — core building blocks
- Neural networks are parameterised functions composed of layers that transform inputs through learned weight matrices and element-wise non-linearities. Understanding activations, learning dynamics, and the distinction between parameters and hyperparameters is essential before studying any specialised architecture.
#### Activation Functions
- description
  - Non-linear functions applied after each linear transformation, enabling networks to learn complex, non-linear mappings from inputs to outputs. Without them every layer collapses to a single matrix multiplication and the network loses expressive power.
- ReLU
  - Acronym: _ReLU_ <span id="relu-target"></span> = Rectified Linear Unit
    - The default activation for hidden layers in modern deep nets. Computationally cheap, reduces the vanishing-gradient problem compared to sigmoid and tanh, and produces sparse activations that improve generalisation.
  - Maths: f(x) = max(0, x) — zero for negatives, identity for positives
- Sigmoid
  - description
    - A smooth S-shaped function that maps any real number to the range (0, 1), making it suitable for binary output layers and gating mechanisms. Its saturating tails produce near-zero gradients for very large or small inputs, causing the vanishing-gradient problem in deep networks.
  - Maths: σ(x) = 1 / (1 + e⁻ˣ) — squashes input to (0, 1), used in gates and binary output
- Tanh
  - description
    - Zero-centred variant of sigmoid that maps inputs to (−1, 1), giving stronger gradients near the origin than sigmoid. Still suffers from saturation at extreme values, but its zero-centred outputs reduce the zig-zag dynamics of gradient descent in early layers.
  - Maths: tanh(x) = (eˣ − e⁻ˣ) / (eˣ + e⁻ˣ) — zero-centred, squashes to (−1, 1)
- Softmax
  - description
    - Converts a vector of raw scores (logits) into a proper probability distribution by exponentiating each score and dividing by their sum. Used exclusively at the output layer of multi-class classifiers to produce interpretable class probabilities.
  - Maths: softmax(zᵢ) = eᶻⁱ / Σⱼ eᶻʲ — converts score vector to probability distribution
#### Learning Dynamics
- description
  - The forward–backward cycle that iteratively reduces training loss: inputs flow forward through the network to produce predictions, errors are propagated backward via the chain rule to compute gradients, and an optimizer updates the weights.
- Forward pass
  - The computation of a network's output given an input by sequentially applying weight matrices and activation functions from the input layer to the output layer. The activations produced at each layer are cached for use during backpropagation.
- Backpropagation
  - description
    - Efficient algorithm for computing gradients of the loss with respect to every parameter by applying the chain rule layer by layer from output back to input. It reuses cached forward-pass activations to avoid redundant computation, making gradient calculation as cheap as a second forward pass.
  - Maths: ∂L/∂w = (∂L/∂a) · (∂a/∂z) · (∂z/∂w) — chain rule decomposes gradient layer by layer
- Gradient descent
  - description
    - Iterative optimisation strategy that moves each parameter in the direction opposite to its gradient, thereby reducing the loss function step by step. The update size is controlled by the learning rate; stochastic variants sample mini-batches for computational efficiency.
  - Maths: θ ← θ − η · ∇_θ L — shifts each parameter opposite to its gradient by step size η
- Learning rate
  - Scalar hyperparameter η that controls how large each parameter update step is during gradient descent. Too large a value causes the loss to diverge; too small a value slows convergence dramatically — choosing or scheduling it well is one of the most impactful tuning decisions.
#### Key Distinctions
- description
  - Conceptual pairs that frequently cause confusion: parameters are learned during training, while hyperparameters are set before training; underfitting and overfitting are opposite failure modes that guide model complexity choices.
- Parameters vs. Hyperparameters
  - Parameters (weights and biases) are the values the network learns from data by minimising the loss function. Hyperparameters (learning rate, batch size, number of layers, regularisation strength) are design choices fixed before training that govern how learning proceeds.
- Underfitting vs. Overfitting
  - Underfitting occurs when the model is too simple to capture the data's true patterns, showing high error on both training and validation sets. Overfitting occurs when the model memorises training noise rather than generalising, showing low training error but high validation error.

### Loss Functions
- description
  - Scalar functions that measure the discrepancy between model predictions and true labels, providing the training signal for gradient descent. The choice of loss function must match the output type: regression, binary classification, multi-class classification, or distribution matching.
- Mean Squared Error (MSE)
  - Acronym: _MSE_ <span id="mse-target"></span> = Mean Squared Error
    - Standard regression loss that squares individual errors, penalising large mistakes disproportionately. Differentiable everywhere and interpretable as variance of residuals, but sensitive to outliers.
  - Maths: L = (1/n) Σᵢ (ŷᵢ − yᵢ)² — averages squared errors, penalises large deviations more
- Cross-entropy
  - description
    - Measures the average number of bits needed to represent the true label distribution using the model's predicted distribution. Widely used for multi-class classification with softmax outputs; it directly maximises the log-probability assigned to the correct class.
  - Maths: L = −Σᵢ yᵢ log(ŷᵢ) — penalises low confidence on the correct class
- Binary cross-entropy
  - description
    - Specialised form of cross-entropy for two-class problems where the output is a single sigmoid probability. It penalises the model heavily when it assigns low probability to the correct binary label, and is also used as the discriminator loss in vanilla [GANs](#gans-target).
  - Maths: L = −[y log(ŷ) + (1−y) log(1−ŷ)] — divergence between predicted probability and binary label
- KL Divergence
  - Acronym: _KL_ <span id="kl-target"></span> = Kullback-Leibler (information-theoretic divergence measure)
    - Asymmetric measure of how much information is lost when approximating distribution P with Q. Used in [VAE](#vae-target) as the regularisation term keeping the latent space close to a Gaussian prior, and as the foundation of cross-entropy loss.
  - Maths: D_KL(P ‖ Q) = Σₓ P(x) log(P(x)/Q(x)) — how much P diverges from reference Q

## Convolutional Neural Networks (CNNs)
### Acronym: _CNNs_ <span id="cnns-target"></span> = Convolutional Neural Networks
- Deep neural networks that apply learnable filters across spatial dimensions to detect local patterns such as edges, textures, and shapes. Weight sharing across positions drastically reduces parameters and provides translation invariance, making [CNNs](#cnns-target) the dominant architecture for image tasks.
### Core Components
- description
  - The architectural building blocks that give [CNNs](#cnns-target) their power: convolution layers extract local features, pooling layers downsample spatially, and fully-connected layers combine those features into a final prediction. Each component serves a distinct role in transforming raw pixels into class scores.
- Convolution filters (kernels)
  - Small weight matrices (e.g., 3×3 or 5×5) slid across the input image, computing dot products at each position to produce a feature map. Each filter learns to detect a specific local pattern — early layers detect edges, deeper layers detect complex shapes.
- Stride & Padding
  - Stride controls how many pixels the filter moves between applications, trading spatial resolution for computational cost. Padding adds zeros around the input border so that filters at the edges see as much context as interior filters and the output size can be preserved.
- Max Pooling / Avg Pooling
  - Downsampling operations that reduce spatial dimensions by taking the maximum or average value over a local window. Max pooling retains the strongest activation in each region, providing a degree of translation invariance and reducing the number of parameters in subsequent layers.
- Fully-connected layers
  - Dense layers placed at the top of a [CNN](#cnns-target) that take the flattened feature maps from the convolutional stack and combine them into a final output vector. They learn global relationships between all detected features and typically constitute the majority of a [CNN](#cnns-target)'s parameters.
- ReLU activations
  - Applied element-wise after each convolution (and often after each fully-connected layer) to introduce non-linearity. In [CNNs](#cnns-target), [ReLU](#relu-target) is preferred over sigmoid or tanh because it does not saturate for positive inputs and trains faster in deep stacks.

### Landmark Architectures
- description
  - Sequence of models that progressively pushed image recognition forward, each introducing a key design insight that became standard practice. Studying them shows how the field progressed from shallow feature engineering to deep end-to-end learning.
- AlexNet — 8 layers, ImageNet 2012
  - The first deep [CNN](#cnns-target) to win ImageNet decisively, demonstrating that GPU-trained networks with [ReLU](#relu-target) activations and dropout regularisation vastly outperform hand-crafted features. Its five convolutional layers and three fully-connected layers became the template for the next generation of architectures.
- VGG — uniform 3×3 filters
  - Acronym: _VGG_ <span id="vgg-target"></span> = Visual Geometry Group (Oxford research group that designed the architecture)
    - Architecture from Oxford's [VGG](#vgg-target) lab (2014) that showed depth could be increased by stacking only 3×3 filters uniformly. Straightforward to replicate and widely used as a feature extractor, though parameter-heavy due to large fully-connected layers.
- ResNet — skip connections
  - Acronym: _ResNet_ <span id="resnet-target"></span> = Residual Network — skip connections allow identity shortcuts through layers
    - Introduced skip connections that add the input of a block directly to its output, enabling gradients to flow through hundreds of layers without vanishing. Won ImageNet 2015 and became the foundation for nearly all modern deep vision architectures.
- Inception — multi-scale filters
  - Applies filters of multiple kernel sizes (1×1, 3×3, 5×5) in parallel within the same layer, then concatenates their outputs. This multi-scale approach lets the network decide which spatial scale is most informative for each feature, achieving high accuracy with fewer parameters than [VGG](#vgg-target).

### Training for Vision
- description
  - Practical techniques applied during training to improve generalisation and stability of [CNN](#cnns-target) models on visual data. Combining several of these methods is standard practice when working with limited or noisy image datasets.
- Data augmentation
  - Artificially expands the training set by applying random transformations (flips, crops, rotations, colour jitter) to each image at training time. Prevents the model from memorising specific pixel values and significantly reduces overfitting, especially when labelled data is scarce.
- Batch normalization
  - Normalises each mini-batch's activations to zero mean and unit variance, then applies learnable scale and shift parameters. It stabilises and accelerates training, reduces sensitivity to initialisation, and acts as a mild regulariser, making it standard in nearly all modern [CNNs](#cnns-target).
- Dropout
  - Randomly zeros out a fraction of neuron activations during each training step, forcing the network to learn redundant representations. At test time all neurons are active and their outputs are scaled, resulting in an implicit ensemble that generalises better.
- Transfer learning & fine-tuning
  - Initialises a new model with weights pre-trained on a large dataset (e.g., ImageNet) and then adapts those weights to a target task with a smaller dataset. Fine-tuning the later layers — which encode task-specific features — while keeping early layers frozen is the most common strategy.

### Applications
- description
  - [CNNs](#cnns-target) are the backbone of most modern computer vision systems, from consumer apps to medical imaging and autonomous driving. Their translation invariance and hierarchical feature learning generalise across any task that involves local spatial patterns.
- Image classification
  - Assigns a single label (or ranked list of labels) to an entire input image. The canonical [CNN](#cnns-target) task, popularised by ImageNet competitions, that drives most architecture research.
- Object detection
  - Locates and classifies multiple objects within an image, outputting bounding boxes alongside class labels. Frameworks such as YOLO and Faster R-CNN extend classification [CNNs](#cnns-target) with region-proposal or anchor-based heads.
- Semantic segmentation
  - Assigns a class label to every pixel in an image, producing a dense prediction map. Used in autonomous driving, medical imaging, and satellite analysis where understanding per-pixel context is required.
- Time series (1D conv)
  - Applies one-dimensional convolutional filters along the time axis to detect local temporal patterns in signals such as audio, sensor readings, or financial data. Faster to train than [RNNs](#rnns-target) for many sequence tasks and easier to parallelise.

## Recurrent Neural Networks (RNNs)
### Acronym: _RNNs_ <span id="rnns-target"></span> = Recurrent Neural Networks
- Neural networks designed for sequential data where a hidden state carries information forward across timesteps using shared weights. They can model arbitrary-length sequences in theory, but struggle with long-range dependencies due to vanishing gradients — the problem [LSTM](#lstm-target) and [GRU](#gru-target) were designed to solve.
### Architectures
- description
  - The main RNN variants trade off between simplicity, parameter count, and ability to retain information over long sequences. Vanilla [RNNs](#rnns-target) are the conceptual baseline; [LSTM](#lstm-target) and [GRU](#gru-target) add gating mechanisms that give the network explicit control over what to remember.
- Vanilla RNN
  - The simplest recurrent architecture: at each timestep the hidden state is computed from the current input and the previous hidden state via a single linear transformation and a tanh activation. Despite its elegance, the shared weight matrix causes gradients to vanish or explode over long sequences, limiting its practical utility.
- LSTM — input / forget / output gates
  - Acronym: _LSTM_ <span id="lstm-target"></span> = Long Short-Term Memory — gated RNN that selectively retains long-range dependencies
    - An RNN cell with three learnable gates (input, forget, output) controlling what is written to, erased from, and read from a dedicated cell state. The gating mechanism preserves or discards information over many timesteps, solving the vanishing-gradient problem for most practical sequence lengths.
- GRU — update / reset gates
  - Acronym: _GRU_ <span id="gru-target"></span> = Gated Recurrent Unit — streamlined [LSTM](#lstm-target) with fewer parameters
    - Merges the [LSTM](#lstm-target) cell state and hidden state into one and uses only two gates (update and reset). Fewer parameters than [LSTM](#lstm-target) with comparable performance on most tasks, making it preferred when compute is constrained.

### Challenges
#### Description — training difficulties
- Recurrent networks suffer from two fundamental optimisation problems that arise from multiplying the same weight matrix repeatedly across timesteps. Both problems make it hard to learn dependencies spanning more than a few dozen steps in vanilla [RNNs](#rnns-target).
#### Vanishing Gradient
- Gradients shrink through time
- Solutions: [LSTM](#lstm-target)/[GRU](#gru-target) gating, layer norm
#### Exploding Gradient
- Gradients grow unbounded
- Solution: gradient clipping

### Applications
- description
  - [RNNs](#rnns-target) and their gated variants are applied wherever the input is a sequence of variable length or where temporal order carries meaning. They were the dominant sequence-modelling architecture before Transformers.
- Natural Language Processing
  - [RNNs](#rnns-target) were the first effective neural approach to [NLP](#nlp-target) tasks such as language modelling, machine translation, and sentiment analysis, processing text one token at a time while maintaining a context state.
- Time series forecasting
  - Predicts future values of a signal (stock prices, weather, energy consumption) by conditioning on historical timesteps stored in the hidden state.
- Speech recognition
  - Converts a variable-length audio sequence into a word sequence by modelling acoustic features across time. Bidirectional [LSTMs](#lstm-target) are particularly effective because each output token benefits from both past and future acoustic context.
- Anomaly detection
  - Trains the RNN on normal sequence patterns and flags timesteps where the prediction error exceeds a threshold, indicating unusual behaviour in sensor streams, network traffic, or financial transactions.

## Attention & Transformers
### Self-Attention Mechanism
- description
  - A mechanism that allows every position in a sequence to directly attend to every other position, computing a weighted sum of values based on pairwise relevance scores between queries and keys. This replaces recurrence with parallelisable matrix operations, enabling much faster training on long sequences.
- Query (Q) — what to look for
- Key (K) — what to match against
- Value (V) — what to aggregate
- Scaled dot-product: softmax(QKᵀ/√dₖ)·V
  - description
    - Computes compatibility between each query and all keys via dot products, divides by √dₖ to keep gradients from vanishing in high dimensions, applies softmax to get a probability distribution, then aggregates values by those weights. This single operation replaces the sequential dependency of recurrence.
  - Maths: A(Q,K,V) = softmax(QKᵀ / √dₖ) · V — relevance scores scaled to prevent vanishing gradients
- Multi-head attention — parallel views
  - description
    - Runs h independent attention operations with different learned projections of Q, K, and V, then concatenates and projects the results. Each head can specialise in a different type of relationship (syntax, coreference, position), giving the model richer representational capacity than a single attention pass.
  - Maths: MultiHead(Q,K,V) = Concat(head₁,…,headₕ) Wᴼ where headᵢ = Attention(Q Wᵢᴼ, K Wᵢᴷ, V Wᵢᵛ)

### Text Representations
- description
  - The way raw text is converted into numeric vectors before being fed into a neural network. The quality and structure of these representations have a large effect on downstream task performance.
- One-hot encoding
  - Represents each word as a sparse binary vector of length equal to the vocabulary size, with a single 1 at the word's index. Simple and exact, but carries no semantic information — two related words are as distant from each other as two unrelated ones.
- Word2Vec embeddings
  - Dense low-dimensional vectors (typically 100–300 dimensions) learned by predicting a word from its context (CBOW) or predicting context from a word (Skip-gram). Semantically similar words cluster together in the embedding space, enabling arithmetic like king − man + woman ≈ queen.
- Dense semantic vectors
  - General term for any fixed-dimensional, real-valued representation that encodes meaning into a compact space. Produced by trained embedding layers, pre-trained language models, or dimensionality reduction methods such as PCA or UMAP.
- Sentence Transformers
  - Fine-tuned Transformer models that produce a single fixed-length embedding for an entire sentence or paragraph, optimised for semantic similarity tasks. Used for semantic search, clustering, and retrieval-augmented generation.

### Positional Encoding
- description
  - Since self-attention is permutation-invariant, positional encodings inject information about each token's position in the sequence before attention is applied. Without them, a Transformer would treat "dog bites man" and "man bites dog" identically.
- Sinusoidal (sin/cos functions)
  - description
    - Fixed (non-learned) encoding that assigns each position a unique signature using sine and cosine waves of geometrically decreasing frequencies. The relative position between any two tokens can be recovered by a linear transformation, helping the model generalise to sequence lengths not seen during training.
  - Maths: PE(pos, 2i) = sin(pos / 10000^(2i/d)) ; PE(pos, 2i+1) = cos(pos / 10000^(2i/d))
- Learnable positional embeddings
  - Treats each position index as a token and learns its embedding jointly with the rest of the model parameters. More flexible than sinusoidal encodings but cannot extrapolate to positions beyond the maximum length seen during training.
- Absolute vs. relative positions
  - Absolute encodings assign a fixed vector to each position index independently; relative encodings instead encode the distance between pairs of tokens directly into the attention computation. Relative encodings (e.g., RoPE, ALiBi) tend to generalise better to longer sequences at inference time.

### Language Transformers (NLP)
#### Acronym: _NLP_ <span id="nlp-target"></span> = Natural Language Processing
- The field of AI concerned with enabling computers to understand, generate, and manipulate human language. Modern [NLP](#nlp-target) is dominated by pre-trained Transformer models fine-tuned on downstream tasks such as classification, translation, summarisation, and question answering.
#### Architecture
- description
  - The standard Transformer block alternates between a multi-head self-attention sublayer and a position-wise feed-forward sublayer, with layer normalisation and residual connections wrapping each. Stacking N such blocks gives the model depth while residual connections ensure stable gradient flow.
- Encoder — bidirectional context
  - Processes the entire input sequence simultaneously with full bidirectional attention, so each token's representation is informed by all tokens to its left and right. Used in models like [BERT](#bert-target) for tasks requiring deep understanding of the input (classification, NER, question answering).
- Decoder — autoregressive generation
  - Generates output tokens one at a time, with each position attending only to previously generated tokens via causal (masked) self-attention. A cross-attention sublayer additionally attends to the encoder's output, enabling sequence-to-sequence tasks like translation.
- Layer normalization
  - Normalises activations across the feature dimension (rather than the batch dimension) after each sublayer, stabilising training in deep Transformers where batch sizes are often small. Applied before (Pre-LN) or after (Post-LN) each sublayer depending on the variant.
- Feed-forward sublayers
  - Two-layer MLP applied independently at each position after the attention sublayer, with an expansion ratio (typically 4×) that provides most of the model's per-token representational capacity. The same weights are shared across all positions, acting as a learned memory.
#### Pre-training & Fine-tuning
- description
  - Two-stage training paradigm: first train on a massive unlabelled corpus with a self-supervised objective to learn general language representations, then adapt to a specific task with a much smaller labelled dataset. This dramatically reduces the data and compute needed for each downstream application.
- Masked language modeling (BERT-style)
  - Acronym: _BERT_ <span id="bert-target"></span> = Bidirectional Encoder Representations from Transformers
    - A large Transformer encoder pre-trained by predicting randomly masked tokens (MLM) using full bidirectional context. Released in 2018, it set state-of-the-art on almost every [NLP](#nlp-target) benchmark and established the pre-train / fine-tune paradigm.
- Next-token prediction (GPT-style)
  - Acronym: _GPT_ <span id="gpt-target"></span> = Generative Pre-trained Transformer
    - A decoder-only Transformer trained to predict the next token in text. By training on large corpora it learns broad world knowledge and linguistic ability that can be specialised to tasks via fine-tuning or few-shot prompting.
- Downstream task adaptation
  - Adds a lightweight task-specific head (e.g., a linear classifier) on top of a pre-trained model and fine-tunes some or all of the model's weights on the labelled target dataset. Requires orders of magnitude less data than training from scratch because the pre-trained representations already encode rich linguistic knowledge.

### Vision Transformers (ViT)
- Acronym: _ViT_ <span id="vit-target"></span> = Vision Transformer — applies Transformer self-attention directly to flattened image patches
  - An architecture that splits an image into fixed-size patches, linearly embeds each patch, and processes them with standard Transformer self-attention. Removing convolutions entirely, [ViT](#vit-target) scales better than [CNNs](#cnns-target) when pre-trained on very large datasets and achieves state-of-the-art image classification results.
- Image → patches → linear embeddings
  - The image is divided into a grid of non-overlapping patches (typically 16×16 pixels), each patch is flattened into a vector and projected to the model's hidden dimension. This converts a 2D image into a sequence of tokens that the Transformer can process like a sentence.
- 2D positional encoding
  - Injects row and column position information into each patch embedding so the model knows the spatial layout of tokens. Without it, the Transformer would be indifferent to whether a patch came from the top-left or bottom-right of the image.
- Same attention mechanism as NLP
- Pre-trained on ImageNet-21k
  - Large-scale pre-training on 21 million labelled images gives [ViT](#vit-target) the statistical diversity needed to learn general visual features before fine-tuning. Without this scale, [ViT](#vit-target) underperforms [CNNs](#cnns-target) due to its lack of built-in inductive biases.
- Fine-tuned on downstream vision tasks
  - After pre-training, a classification head or task-specific decoder is attached and the entire model (or selected layers) is trained on the target dataset with a smaller learning rate. Fine-tuning converges quickly because pre-trained patch embeddings already encode rich visual representations.
- Challenges: resolution sensitivity, scale
  - [ViT](#vit-target)'s performance degrades when tested at resolutions different from those seen during pre-training because the number of patches changes and positional encodings must be interpolated. Additionally, [ViT](#vit-target) requires substantially more data and compute than comparably sized [CNNs](#cnns-target) to achieve competitive results.

## Generative Models
### Discriminative vs. Generative
- description
  - Discriminative models learn decision boundaries directly in input space (P(Y|X)), while generative models learn the joint or marginal data distribution (P(X,Y) or P(X)). Generative models are more data-hungry and complex, but can generate new samples, handle missing data, and model uncertainty more naturally.
- Discriminative: P(Y|X) — decision boundaries
- Generative: P(X,Y) — data structure
- Trade-offs: labeled data, complexity, versatility

### Latent Space
- description
  - A lower-dimensional continuous space learned by a generative model in which each point decodes to a plausible data sample. The structure of this space determines the quality of generated outputs and the ability to perform meaningful interpolation and attribute control.
- Abstract compressed representation
- Semantic clustering of similar concepts
- Interpolation between samples
- Controlled attribute manipulation

### Variational Autoencoders (VAE)
- Acronym: _VAE_ <span id="vae-target"></span> = Variational Autoencoder — generative model with a regularised probabilistic latent space
  - An encoder maps inputs to a probability distribution over a latent space (rather than a fixed point), and a decoder samples from that distribution to reconstruct inputs. [KL](#kl-target) regularisation forces the latent space to be smooth and structured, enabling interpolation and controlled generation.
- Encoder: Q_φ(Z|X) — posterior approximation
  - A neural network that takes an input x and outputs the parameters (mean and variance) of a Gaussian distribution over the latent variable z. Training it jointly with the decoder and [KL](#kl-target) penalty encourages the latent distribution to stay close to a standard Gaussian prior.
- Decoder: P_θ(X|Z) — generation
  - A neural network that takes a sample from the latent distribution and reconstructs the original input. At generation time, samples are drawn directly from the prior rather than from an encoded input, allowing the model to produce novel outputs.
- ELBO loss: reconstruction + KL term
  - Acronym: _ELBO_ <span id="elbo-target"></span> = Evidence Lower BOund ; [KL](#kl-target) = Kullback-Leibler divergence
    - The [ELBO](#elbo-target) is what the [VAE](#vae-target) actually optimises — a lower bound on the log-likelihood of the data. It balances a reconstruction term (how well the decoder reproduces the input) against a [KL](#kl-target) penalty (how close the inferred latent distribution is to the Gaussian prior).
  - Maths: L = E_q[log p_θ(x|z)] − D_KL(q_φ(z|x) ‖ p(z)) — maximise reconstruction while keeping latent close to Gaussian prior
- Smooth, structured latent space
- Applications: generation, anomaly detection

### Generative Adversarial Networks (GANs)
#### Acronym: _GANs_ <span id="gans-target"></span> = Generative Adversarial Networks
- A framework where two networks are trained adversarially: the generator tries to produce samples indistinguishable from real data, while the discriminator tries to tell them apart. At Nash equilibrium the generator captures the true data distribution. [GANs](#gans-target) produce sharp outputs but are notoriously hard to train stably.
#### Architecture
- description
  - The two-network setup that defines the adversarial training loop: the generator maps random noise to synthetic data, and the discriminator judges each sample as real or fake. The minimax objective ties their losses together so that one's improvement is the other's loss.
- Generator — creates synthetic samples from noise
  - A neural network (typically a deconvolutional or MLP architecture) that maps a random noise vector z to a synthetic sample in data space. Its goal is to fool the discriminator; as training progresses its outputs become indistinguishable from real data.
- Discriminator — real vs. fake classifier
  - A binary classifier trained to distinguish real training samples from samples produced by the generator. Provides the adversarial signal that drives the generator toward the true data distribution; in [WGAN](#wgan-target) it is replaced by a critic without a sigmoid output.
- Minimax adversarial game
  - The generator minimises — and the discriminator maximises — the same objective function, creating a zero-sum game. Convergence to the Nash equilibrium means the generator has learned the true data distribution and the discriminator outputs 0.5 everywhere.
#### Loss Functions
- description
  - The choice of loss function has a major impact on GAN training stability and sample quality. The original JS divergence suffers from vanishing gradients when distributions are disjoint; [WGAN](#wgan-target)'s Wasserstein distance and hinge loss are more robust alternatives.
- Jensen-Shannon Divergence (original)
  - description
    - Symmetric, bounded divergence measure used as the original [GAN](#gans-target) objective; minimising it is equivalent to the generator matching the real data distribution. In practice, training often collapses or oscillates because JS divergence saturates when the real and generated distributions have little overlap.
  - Maths: JSD(P‖Q) = ½ D_KL(P‖M) + ½ D_KL(Q‖M), M=½(P+Q) — symmetric similarity between real and generated distributions
- Wasserstein distance (WGAN — more stable)
  - Acronym: _WGAN_ <span id="wgan-target"></span> = Wasserstein Generative Adversarial Network
    - A [GAN](#gans-target) variant that replaces the JS divergence with the Wasserstein (earth-mover) distance as the training objective. Meaningful gradients even when real and generated distributions have disjoint support make training more stable and less prone to mode collapse.
  - Maths: W(P,Q) = inf_{γ∈Π(P,Q)} 𝔼[‖x−y‖] — earth-mover distance, stable gradients even with disjoint support
- Hinge loss
  - Variant of the [GAN](#gans-target) objective adapted from support vector machines that clips the discriminator's output using a margin, preventing it from providing excessively large gradients. Widely adopted in high-resolution image synthesis models (BigGAN, StyleGAN) for its training stability.
#### Challenges
- Mode collapse
- Training instability
- Non-convergence
#### Applications
- description
  - [GANs](#gans-target) have become the workhorse for high-fidelity image synthesis tasks where perceptual sharpness is prioritised over likelihood. Their adversarial training produces crisp, photorealistic outputs that [VAEs](#vae-target) and early diffusion models struggled to match.
- Image synthesis
  - Generates photorealistic images from random noise or conditional inputs such as class labels or text descriptions; models like StyleGAN produce faces indistinguishable from real photographs.
- Style transfer
  - Maps the visual style (texture, colour palette) of one image onto the content of another by separating and recombining feature statistics in a [CNN](#cnns-target) or generator network.
- Super-resolution
  - Reconstructs high-resolution details from low-resolution inputs by training a generator to produce plausible fine-grained textures that fool the discriminator.
- Video generation
  - Extends image [GANs](#gans-target) with temporal consistency constraints to synthesise coherent video sequences, enabling applications in film production, simulation, and data augmentation.

### Diffusion Models (DDPM)
#### Acronym: _DDPM_ <span id="ddpm-target"></span> = Denoising Diffusion Probabilistic Models
- A generative model defining a forward Markov chain that gradually adds Gaussian noise over T timesteps until data becomes pure noise, then trains a neural network to reverse this process step by step. At inference, sampling starts from noise and the network iteratively denoises it into a realistic sample.
#### Forward Process
- description
  - The fixed (non-learned) Markov chain that incrementally corrupts a data sample into isotropic Gaussian noise by adding small amounts of noise at each of T timesteps according to a pre-defined variance schedule β₁, …, βₜ.
- Gradual noise addition over T timesteps
- Markovian: q(xₜ|xₜ₋₁)
  - description
    - Each noisy state xₜ depends only on the immediately preceding state xₜ₋₁, enabling the entire chain to be reparameterised so that xₜ can be sampled directly from x₀ without iterating through all intermediate steps.
  - Maths: q(xₜ|xₜ₋₁) = N(xₜ ; √(1−βₜ) xₜ₋₁ , βₜ I) — adds scheduled Gaussian noise; after T steps xₜ ≈ N(0,I)
- Destroys data structure progressively
#### Reverse Process
- description
  - A learned Markov chain that runs backwards through time, starting from pure noise and iteratively predicting and removing the noise added at each forward step. The neural network must learn to approximate the true reverse conditional distribution at every timestep.
- Learns to denoise step-by-step
- p_θ(xₜ₋₁|xₜ) approximation
  - description
    - A neural network (typically a U-Net) parameterises the mean (and optionally the variance) of the Gaussian reverse transition at each timestep t. Because t is provided as input, a single network handles all timesteps, making training and inference tractable.
  - Maths: p_θ(xₜ₋₁|xₜ) = N(xₜ₋₁ ; μ_θ(xₜ,t) , Σ̃(t)) — neural network predicts mean of clean distribution
- Neural network predicts noise
#### Training
- description
  - The model is trained by randomly sampling a data point, a timestep, and a noise sample, then minimising the squared error between the network's noise prediction and the actual noise that was added. This simple objective is a simplified bound on the variational lower bound of the data likelihood.
- L2 loss on predicted vs. true noise
  - description
    - Optimises the network to predict the noise vector ε that was added to x₀ at timestep t, rather than directly predicting x₀. This reparameterisation was found empirically to produce better sample quality and simpler training dynamics.
  - Maths: L = ‖ μ_θ(xₜ, t) − μ̃(xₜ, x₀) ‖² — minimised across all timesteps
- Stable compared to [GANs](#gans-target)
#### Applications
- description
  - Diffusion models have become the state-of-the-art approach for high-quality image, audio, and video generation, surpassing [GANs](#gans-target) on perceptual metrics while being more stable to train.
- DALL-E 2
  - OpenAI's text-to-image diffusion model that conditions the reverse process on CLIP text embeddings to generate diverse, high-quality images from natural language descriptions.
- Stable Diffusion
  - Runs the diffusion process in the latent space of a [VAE](#vae-target) rather than pixel space, dramatically reducing compute while maintaining image quality; open-source and widely deployed.
- Midjourney
  - Commercial text-to-image service built on diffusion principles, known for its distinctive artistic style and high aesthetic quality in generated images.
- Image editing / inpainting
  - Uses the reverse diffusion process conditioned on a masked region to fill in missing or corrupted parts of an image with plausible, coherent content.

## Large Language Models (LLMs)
### Acronym: _LLMs_ <span id="llms-target"></span> = Large Language Models
- Very large Transformer-based language models pre-trained on billions of tokens using self-supervised objectives such as next-token prediction. Scale unlocks emergent capabilities — in-context learning, chain-of-thought reasoning, and zero-shot generalisation — that are absent in smaller models.
### GPT Family (OpenAI)
- Acronym: [GPT](#gpt-target) = Generative Pre-trained Transformer
  - OpenAI's decoder-only Transformer series scaled from [GPT](#gpt-target)-1 (2018) through [GPT](#gpt-target)-4 (2023). Each generation trained on larger corpora with more parameters; [GPT](#gpt-target)-3 demonstrated few-shot learning and [GPT](#gpt-target)-4 added multimodal inputs and substantially improved reasoning.
- Decoder-only Transformer
  - Architecture where every layer uses causal (left-to-right) self-attention so that each token only attends to previous tokens. This autoregressive constraint makes the model naturally suited to text generation and next-token prediction objectives.
- Next-token prediction pre-training
  - Self-supervised objective where the model is trained to predict the next token in a sequence given all previous tokens. Training on trillions of tokens from the web allows the model to implicitly learn grammar, facts, reasoning patterns, and coding skills.
- GPT-1 → GPT-2 → GPT-3 → GPT-4
  - A scaling progression from 117M parameters ([GPT](#gpt-target)-1) to an estimated trillion+ parameters ([GPT](#gpt-target)-4), with each version demonstrating qualitatively new capabilities. [GPT](#gpt-target)-2 showed fluent long-form text generation; [GPT](#gpt-target)-3 introduced few-shot prompting; [GPT](#gpt-target)-4 added multimodal reasoning.
- GPT-4: multimodal (text + image)
  - The first [GPT](#gpt-target) model to accept image inputs alongside text, enabling tasks such as image captioning, chart interpretation, and visual question answering. Its vision encoder is integrated with the language decoder through cross-attention or prefix conditioning.
- ChatGPT: RLHF fine-tuned
  - Acronym: _RLHF_ <span id="rlhf-target"></span> = Reinforcement Learning from Human Feedback — aligns model outputs to human preferences via reward modelling
    - A fine-tuning pipeline that collects human preference rankings over model outputs, trains a reward model from those rankings, then optimises the [LLM](#llms-target) against the reward model using policy-gradient RL (typically PPO). [RLHF](#rlhf-target) is the key step that turns a raw pre-trained model into a safe, helpful assistant.

### LLaMA (Meta)
- Acronym: _LLaMA_ <span id="llama-target"></span> = Large Language Model Meta AI — Meta's efficient open-weights model family
  - Meta's series of decoder-only Transformers released with open weights, achieving strong performance at smaller scales through careful data curation and training efficiency improvements. Open weights democratised [LLM](#llms-target) research by enabling fine-tuning outside large compute clusters.
- Efficient decoder-only Transformer
  - [LLaMA](#llama-target) applies several architectural improvements over vanilla [GPT](#gpt-target) — including pre-normalisation, SwiGLU activations, and rotary positional embeddings — to achieve better performance per parameter and more stable training at scale.
- Smaller size, competitive performance
  - [LLaMA](#llama-target)-2 13B matches or exceeds [GPT](#gpt-target)-3 175B on many benchmarks by training on more tokens with higher-quality data. This shows that data quality and training efficiency matter as much as raw parameter count.
- Open weights for research
  - Unlike [GPT](#gpt-target)-4, [LLaMA](#llama-target) weights are publicly released, enabling academic labs and independent researchers to study, fine-tune, and build upon the model without API access or commercial licensing costs.

### Multimodal Models
- description
  - Models that process and generate content across more than one modality (text, image, audio, video) by learning shared or cross-modal representations. They generalise the Transformer's sequence-processing paradigm to heterogeneous input types.
- Text + image inputs
  - Combines visual features (from a [CNN](#cnns-target) or [ViT](#vit-target) patch encoder) with text token embeddings in a unified sequence, allowing the model to answer questions about images, generate image captions, or produce images from text prompts.
- AudioGEN — text-to-audio (Meta)
  - Meta's autoregressive model that generates audio (music, sound effects, speech) conditioned on text descriptions by treating discrete audio tokens as a sequence prediction problem analogous to language modelling.
- Cross-modal embeddings
  - Shared embedding spaces (e.g., CLIP) where images and text describing the same concept are mapped to nearby vectors, enabling zero-shot image classification, semantic image search, and conditioning of generative models on language.

## Training Techniques
### Optimization
- description
  - The family of gradient-based algorithms used to minimise the training loss. Beyond vanilla gradient descent, modern optimizers adapt the step size per parameter and use momentum to navigate the loss landscape more efficiently.
- SGD (Stochastic Gradient Descent)
  - Acronym: _SGD_ <span id="sgd-target"></span> = Stochastic Gradient Descent — updates weights using mini-batch gradient estimates
    - The foundational optimisation algorithm for neural networks. A random mini-batch is drawn each step, the loss gradient is computed, and each parameter is nudged in the negative gradient direction. Mini-batches provide a noisy but computationally cheap estimate of the true gradient.
  - Maths: θ ← θ − η · ∇_θ L — parameter update opposite to gradient direction
- Adam / AdamW
  - Acronym: _Adam_ <span id="adam-target"></span> = Adaptive Moment Estimation ; AdamW adds decoupled weight decay
    - Maintains a running estimate of the first moment (mean) and second moment (variance) of gradients per parameter, giving each weight its own effective learning rate. AdamW separates the weight-decay penalty from the gradient update for cleaner regularisation.
  - Maths: mₜ=β₁mₜ₋₁+(1−β₁)gₜ ; vₜ=β₂vₜ₋₁+(1−β₂)gₜ² ; θₜ←θₜ₋₁−η·m̂ₜ/(√v̂ₜ+ε) — adapts lr per parameter using bias-corrected moments
- Learning rate scheduling
  - Adjusts the learning rate during training according to a pre-defined schedule (step decay, cosine annealing, cyclic LR). Lower learning rates in later stages help the model settle into a sharp minimum without overshooting.
- Warm-up strategies
  - Gradually ramps the learning rate from near zero to its target value over the first few thousand steps to stabilise early training. Particularly important for Transformers, where large early gradients can destabilise layer normalisation and attention weights.

### Regularization
- description
  - Techniques that penalise model complexity or introduce noise during training to reduce overfitting and improve generalisation to unseen data. Typically combined — dropout + weight decay + normalisation — for best results.
- Dropout
  - Randomly deactivates neurons with probability p during each training step, preventing units from co-adapting and forcing the network to learn distributed, redundant features. Equivalent to training an exponentially large ensemble of sub-networks.
- Batch normalization
  - Normalises each feature across the mini-batch to zero mean and unit variance, then applies learnable affine parameters. Reduces internal covariate shift, allowing higher learning rates and making training less sensitive to weight initialisation.
- Layer normalization
  - Normalises each sample's activations across the feature dimension rather than across the batch, making it independent of batch size. The standard choice for Transformers and recurrent networks where variable-length sequences make batch statistics unreliable.
- Weight decay (L2)
  - Adds a penalty proportional to the squared magnitude of each weight to the loss, shrinking large weights toward zero. Prevents individual parameters from dominating the network's outputs and acts as an implicit Occam's razor favouring simpler solutions.

### Transfer Learning Paradigm
- description
  - The practice of re-using representations learned on a large source task to bootstrap learning on a smaller target task. Drastically reduces the labelled data and compute required for each new application, and is the dominant training strategy across vision and [NLP](#nlp-target).
- Pre-train on large dataset
  - Trains a model from scratch on a massive dataset (ImageNet, Common Crawl) with a general objective such as image classification or next-token prediction. The resulting weights encode rich, reusable features that transfer broadly.
- Fine-tune on target task
  - Continues training the pre-trained model on a smaller, task-specific dataset with a lower learning rate, adapting the representations to the new domain. Only a fraction of the original data is typically needed because the model already understands low-level and mid-level features.
- Frozen vs. unfrozen layers
  - Freezing early layers (fixing their weights) preserves general low-level features while training only the later, task-specific layers; unfreezing all layers allows the entire network to adapt. The right balance depends on dataset size and how similar the source and target domains are.
- Few-shot & zero-shot capabilities
  - Large pre-trained models can solve new tasks with very few (few-shot) or no (zero-shot) labelled examples by leveraging in-context learning or prompt engineering. This emergent capability arises from the model's broad pre-training and is stronger in larger models.

### Frameworks
- description
  - Software libraries that implement automatic differentiation, GPU acceleration, and high-level model building APIs, abstracting the low-level details of deep learning engineering. The ecosystem around each framework (pretrained models, tutorials, deployment tools) often matters as much as the core API.
- PyTorch — dynamic graphs, research
  - Defines the computation graph dynamically (eager execution), making debugging intuitive with standard Python control flow. The preferred framework in academic research due to its flexibility and tight integration with the Hugging Face ecosystem.
- TensorFlow / Keras — production, deployment
  - TensorFlow uses static computation graphs (with eager mode optional) and Keras provides a high-level API on top; together they offer mature tooling for deploying models to mobile, web, and server environments via TensorFlow Serving and TFLite.
- Hugging Face Transformers
  - Open-source library providing thousands of pre-trained Transformer models ([BERT](#bert-target), [GPT](#gpt-target), T5, [ViT](#vit-target), Whisper, etc.) with a unified API for fine-tuning, inference, and dataset handling. Has become the de facto standard hub for sharing and deploying [NLP](#nlp-target) and multimodal models.

## Maths
### Activation Functions
#### ReLU
- Acronym: [ReLU](#relu-target) = Rectified Linear Unit
- f(x) = max(0, x)
- description
  - Zero for negatives, identity for positives — removes negative activations and adds non-linearity

#### Sigmoid
- σ(x) = 1 / (1 + e⁻ˣ)
- description
  - Squashes any real value into (0, 1) — used for binary outputs and [LSTM](#lstm-target)/[GRU](#gru-target) gates

#### Tanh
- tanh(x) = (eˣ − e⁻ˣ) / (eˣ + e⁻ˣ)
- description
  - Squashes values to (−1, 1) — zero-centred, preferred over sigmoid in hidden layers

#### Softmax
- softmax(zᵢ) = eᶻⁱ / Σⱼ eᶻʲ
- description
  - Converts a score vector into a probability distribution that sums to 1 — used at classification output

### Loss Functions
#### Mean Squared Error (MSE)
- Acronym: [MSE](#mse-target) = Mean Squared Error
- L = (1/n) Σᵢ (ŷᵢ − yᵢ)²
- description
  - Averages squared prediction errors — penalises large deviations more heavily, used in regression

#### Binary Cross-Entropy
- L = −[y log(ŷ) + (1−y) log(1−ŷ)]
- description
  - Measures divergence between predicted probability and binary label — used in binary classifiers and [GAN](#gans-target) discriminator

#### Categorical Cross-Entropy
- L = −Σᵢ yᵢ log(ŷᵢ)
- description
  - Penalises low confidence on the correct class — standard for multi-class softmax output

#### KL Divergence
- Acronym: [KL](#kl-target) = Kullback-Leibler divergence
- D_KL(P ‖ Q) = Σₓ P(x) log(P(x) / Q(x))
- description
  - How much distribution P diverges from reference Q — used in [VAE](#vae-target) and Diffusion model objectives

### Backpropagation & Optimisation
#### Chain Rule (Backprop)
- Acronym: _Backprop_ <span id="backprop-target"></span> = Backpropagation
- ∂L/∂w = (∂L/∂a) · (∂a/∂z) · (∂z/∂w)
- description
  - Recursively decomposes the loss gradient layer by layer from output back to weights

#### Gradient Descent Update
- θ ← θ − η · ∇_θ L
- description
  - Shifts each parameter opposite to its gradient by step size η — the core weight update rule

#### Adam Optimizer
- Acronym: [Adam](#adam-target) = Adaptive Moment Estimation
- mₜ = β₁ mₜ₋₁ + (1−β₁) gₜ  ← 1st moment (mean)
- vₜ = β₂ vₜ₋₁ + (1−β₂) gₜ²  ← 2nd moment (variance)
- θₜ ← θₜ₋₁ − η · m̂ₜ / (√v̂ₜ + ε)
- description
  - Adapts learning rate per parameter using bias-corrected gradient mean and variance estimates

### Attention Mechanism
#### Scaled Dot-Product Attention
- A(Q, K, V) = softmax(QKᵀ / √dₖ) · V
- description
  - Dot products between Q and K give relevance scores; scaling by √dₖ prevents vanishing gradients; V is aggregated by those weights

#### Multi-Head Attention
- headᵢ = Attention(Q Wᵢᴼ, K Wᵢᴷ, V Wᵢᵛ)
- MultiHead(Q,K,V) = Concat(head₁, …, headₕ) Wᴼ
- description
  - Runs h independent attention operations in parallel — each head learns different relational patterns

### Positional Encoding
#### Even dimensions — Sine
- PE(pos, 2i) = sin(pos / 10000^(2i/d))
- description
  - Encodes absolute position using a sine wave whose frequency decreases with dimension index i

#### Odd dimensions — Cosine
- PE(pos, 2i+1) = cos(pos / 10000^(2i/d))
- description
  - Paired with sine to give each position a unique, continuous signature across all dimensions

### Generative Model Equations
#### VAE — ELBO Loss
- Acronym: [VAE](#vae-target) = Variational Autoencoder
- Acronym: [ELBO](#elbo-target) = Evidence Lower BOund
- L = E_q[log p_θ(x|z)] − D_KL(q_φ(z|x) ‖ p(z))
- description
  - Maximises reconstruction quality (1st term) while keeping latent distribution close to a unit Gaussian prior (2nd term)

#### Forward Diffusion — DDPM
- Acronym: [DDPM](#ddpm-target) = Denoising Diffusion Probabilistic Models
- q(xₜ | xₜ₋₁) = N(xₜ ; √(1−βₜ) xₜ₋₁ , βₜ I)
- description
  - Adds scheduled Gaussian noise at each timestep t; βₜ controls noise magnitude — after T steps xₜ ≈ N(0,I)

#### Reverse Diffusion — DDPM
- Acronym: [DDPM](#ddpm-target) = Denoising Diffusion Probabilistic Models
- p_θ(xₜ₋₁ | xₜ) = N(xₜ₋₁ ; μ_θ(xₜ, t) , Σ̃(t))
- description
  - Learned denoising step; neural network predicts the mean of the clean distribution conditioned on noisy input and timestep

#### Diffusion Training Objective (Simplified)
- L = ‖ μ_θ(xₜ, t) − μ̃(xₜ, x₀) ‖²
- description
  - L2 distance between predicted and true reverse-process mean — minimised across all timesteps

#### GAN — Jensen-Shannon Divergence
- Acronym: [GAN](#gans-target) = Generative Adversarial Network
- JSD(P ‖ Q) = ½ D_KL(P ‖ M) + ½ D_KL(Q ‖ M), where M = ½(P+Q)
- description
  - Symmetric measure of similarity between real and generated distributions — minimised by the generator in original [GAN](#gans-target)

#### GAN — Wasserstein Distance (WGAN)
- Acronym: [GAN](#gans-target) = Generative Adversarial Network
- Acronym: [WGAN](#wgan-target) = Wasserstein Generative Adversarial Network
- W(P, Q) = inf_{γ ∈ Π(P,Q)} 𝔼_(x,y)~γ [‖x − y‖]
- description
  - Earth-mover distance between distributions — provides stable gradients even when P and Q have disjoint support, reducing mode collapse

## Projects & Labs
### Miniproyecto 1 — CNNs
- Hands-on project designing and training a convolutional neural network for image classification on a curated dataset. Covers the full pipeline from data loading and augmentation through architecture selection, training, and evaluation.
- Architecture design
  - Decisions about the number and size of convolutional layers, pooling strategy, activation functions, and the final classifier head. Good architecture choices balance model capacity with the size of the available training set to avoid overfitting.
- Image classification pipeline
  - End-to-end workflow including data preprocessing, batching, model training with cross-entropy loss and [SGD](#sgd-target)/[Adam](#adam-target), learning rate scheduling, and computing accuracy metrics on a held-out test set.

### Miniproyecto 2 — RNNs
- Project applying recurrent architectures to sequence modelling tasks using real-world datasets. Focuses on understanding how hidden states evolve over time and how gating mechanisms address the vanishing-gradient problem in practice.
- Sequential data modeling
  - Represents input sequences as ordered series of vectors fed into an RNN one timestep at a time, with the hidden state carrying context forward. The challenge is capturing dependencies that span many steps.
- Movie/sentiment analysis
  - Trains an [LSTM](#lstm-target) or [GRU](#gru-target) to classify the sentiment of movie reviews from text, requiring the model to aggregate sentiment signals across variable-length sequences. Introduces tokenisation, embedding layers, and sequence padding.

### Miniproyecto 3 — Transformers NLP
- Project fine-tuning a pre-trained [BERT](#bert-target)-style Transformer on a text classification task, demonstrating the pre-train / fine-tune paradigm in practice. Covers the Hugging Face Transformers API, tokenisation, and evaluation metrics for [NLP](#nlp-target).
- Fine-tuning BERT-style model
  - Attaches a classification head to a pre-trained encoder and continues training on the labelled target dataset for a small number of epochs. Only a fraction of the pre-training data is needed because the encoder already encodes rich linguistic representations.
- Text classification (BBC dataset)
  - Classifies news articles into topic categories using the BBC News dataset. Serves as a clean benchmark for comparing fine-tuned Transformer performance against classical baselines such as TF-IDF + logistic regression.

### Miniproyecto 4 — Advanced Generative
- Capstone project integrating multiple generative modelling techniques ([VAE](#vae-target), [GAN](#gans-target), or diffusion) to tackle a multimodal generation task. Emphasises understanding trade-offs between generation quality, diversity, and training stability.
- Multimodal generation
  - Combines inputs from more than one modality (e.g., text and image) to condition the generative process, exploring how cross-modal representations can guide synthesis and improve controllability.
- Integrated techniques
  - Applies lessons from earlier modules — architecture design, regularisation, transfer learning, and loss function selection — together in a single generative pipeline, requiring informed decisions about which components to combine.

### Laboratorios
- Lab RNN (m4) — time series
  - Acronym: [RNN](#rnns-target) = Recurrent Neural Network
    - Neural networks that process sequential inputs by maintaining a hidden state, applicable to any time-ordered data. Vanilla [RNNs](#rnns-target), [LSTMs](#lstm-target), and [GRUs](#gru-target) are the main variants covered in this lab.
- Lab Transformers (m5) — NLP
  - Acronym: [NLP](#nlp-target) = Natural Language Processing
    - Computational understanding and generation of human language. In this lab, Transformer-based models are fine-tuned for text classification tasks.
- Lab ViT Part 1 & 2 (m6) — vision
  - Acronym: [ViT](#vit-target) = Vision Transformer
    - Transformer attention applied to image patches instead of text tokens. This lab covers both the architecture and fine-tuning on downstream visual tasks.
- Lab VAE Part 1 & 2 (m7) — generative
  - Acronym: [VAE](#vae-target) = Variational Autoencoder
    - Latent-variable generative models that learn a structured probabilistic latent space. This lab covers encoding, decoding, and sampling from the latent space for image generation.
- Lab GPT (m8) — LLMs
  - Acronym: [GPT](#gpt-target) = Generative Pre-trained Transformer ; [LLMs](#llms-target) = Large Language Models
    - Decoder-only Transformers trained on next-token prediction, scaled to billions of parameters to become [LLMs](#llms-target). This lab explores causal language modelling and text generation with a [GPT](#gpt-target)-style architecture.
