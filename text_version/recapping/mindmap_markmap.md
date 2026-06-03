---
markmap:
  colorFreezeLevel: 2
  maxWidth: 320
  initialExpandLevel: 2
---

# ML Techniques

## Foundations
### History & Biological Inspiration
- Wiesel & Hubel — simple vs. complex cells
- Neocognitron (Fukushima)
- Perceptron → Multi-layer networks
- ImageNet moment (2012)

### Neural Network Basics
#### Activation Functions
- ReLU
- Sigmoid
- Tanh
- Softmax
#### Learning Dynamics
- Forward pass
- Backpropagation
- Gradient descent
- Learning rate
#### Key Distinctions
- Parameters vs. Hyperparameters
- Underfitting vs. Overfitting

### Loss Functions
- Mean Squared Error (MSE)
- Cross-entropy
- Binary cross-entropy
- KL Divergence

## Convolutional Neural Networks (CNNs)
### Core Components
- Convolution filters (kernels)
- Stride & Padding
- Max Pooling / Avg Pooling
- Fully-connected layers
- ReLU activations

### Landmark Architectures
- AlexNet — 8 layers, ImageNet 2012
- VGG — uniform 3×3 filters
- ResNet — skip connections
- Inception — multi-scale filters

### Training for Vision
- Data augmentation
- Batch normalization
- Dropout
- Transfer learning & fine-tuning

### Applications
- Image classification
- Object detection
- Semantic segmentation
- Time series (1D conv)

## Recurrent Neural Networks (RNNs)
### Architectures
- Vanilla RNN
- LSTM — input / forget / output gates
- GRU — update / reset gates

### Challenges
#### Vanishing Gradient
- Gradients shrink through time
- Solutions: LSTM/GRU gating, layer norm
#### Exploding Gradient
- Gradients grow unbounded
- Solution: gradient clipping

### Applications
- Natural Language Processing
- Time series forecasting
- Speech recognition
- Anomaly detection

## Attention & Transformers
### Self-Attention Mechanism
- Query (Q) — what to look for
- Key (K) — what to match against
- Value (V) — what to aggregate
- Scaled dot-product: softmax(QKᵀ/√dₖ)·V
- Multi-head attention — parallel views

### Text Representations
- One-hot encoding
- Word2Vec embeddings
- Dense semantic vectors
- Sentence Transformers

### Positional Encoding
- Sinusoidal (sin/cos functions)
- Learnable positional embeddings
- Absolute vs. relative positions

### Language Transformers (NLP)
#### Architecture
- Encoder — bidirectional context
- Decoder — autoregressive generation
- Layer normalization
- Feed-forward sublayers
#### Pre-training & Fine-tuning
- Masked language modeling (BERT-style)
- Next-token prediction (GPT-style)
- Downstream task adaptation

### Vision Transformers (ViT)
- Image → patches → linear embeddings
- 2D positional encoding
- Same attention mechanism as NLP
- Pre-trained on ImageNet-21k
- Fine-tuned on downstream vision tasks
- Challenges: resolution sensitivity, scale

## Generative Models
### Discriminative vs. Generative
- Discriminative: P(Y|X) — decision boundaries
- Generative: P(X,Y) — data structure
- Trade-offs: labeled data, complexity, versatility

### Latent Space
- Abstract compressed representation
- Semantic clustering of similar concepts
- Interpolation between samples
- Controlled attribute manipulation

### Variational Autoencoders (VAE)
- Encoder: Q_φ(Z|X) — posterior approximation
- Decoder: P_θ(X|Z) — generation
- ELBO loss: reconstruction + KL term
- Smooth, structured latent space
- Applications: generation, anomaly detection

### Generative Adversarial Networks (GANs)
#### Architecture
- Generator — creates synthetic samples from noise
- Discriminator — real vs. fake classifier
- Minimax adversarial game
#### Loss Functions
- Jensen-Shannon Divergence (original)
- Wasserstein distance (WGAN — more stable)
- Hinge loss
#### Challenges
- Mode collapse
- Training instability
- Non-convergence
#### Applications
- Image synthesis
- Style transfer
- Super-resolution
- Video generation

### Diffusion Models (DDPM)
#### Forward Process
- Gradual noise addition over T timesteps
- Markovian: q(xₜ|xₜ₋₁)
- Destroys data structure progressively
#### Reverse Process
- Learns to denoise step-by-step
- p_θ(xₜ₋₁|xₜ) approximation
- Neural network predicts noise
#### Training
- L2 loss on predicted vs. true noise
- Stable compared to GANs
#### Applications
- DALL-E 2
- Stable Diffusion
- Midjourney
- Image editing / inpainting

## Large Language Models (LLMs)
### GPT Family (OpenAI)
- Decoder-only Transformer
- Next-token prediction pre-training
- GPT-1 → GPT-2 → GPT-3 → GPT-4
- GPT-4: multimodal (text + image)
- ChatGPT: RLHF fine-tuned

### LLaMA (Meta)
- Efficient decoder-only Transformer
- Smaller size, competitive performance
- Open weights for research

### Multimodal Models
- Text + image inputs
- AudioGEN — text-to-audio (Meta)
- Cross-modal embeddings

## Training Techniques
### Optimization
- SGD (Stochastic Gradient Descent)
- Adam / AdamW
- Learning rate scheduling
- Warm-up strategies

### Regularization
- Dropout
- Batch normalization
- Layer normalization
- Weight decay (L2)

### Transfer Learning Paradigm
- Pre-train on large dataset
- Fine-tune on target task
- Frozen vs. unfrozen layers
- Few-shot & zero-shot capabilities

### Frameworks
- PyTorch — dynamic graphs, research
- TensorFlow / Keras — production, deployment
- Hugging Face Transformers

## Projects & Labs
### Miniproyecto 1 — CNNs
- Architecture design
- Image classification pipeline

### Miniproyecto 2 — RNNs
- Sequential data modeling
- Movie/sentiment analysis

### Miniproyecto 3 — Transformers NLP
- Fine-tuning BERT-style model
- Text classification (BBC dataset)

### Miniproyecto 4 — Advanced Generative
- Multimodal generation
- Integrated techniques

### Laboratorios
- Lab RNN (m4) — time series
- Lab Transformers (m5) — NLP
- Lab ViT Part 1 & 2 (m6) — vision
- Lab VAE Part 1 & 2 (m7) — generative
- Lab GPT (m8) — LLMs
