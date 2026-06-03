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
  - Maths: f(x) = max(0, x) — zero for negatives, identity for positives
- Sigmoid
  - Maths: σ(x) = 1 / (1 + e⁻ˣ) — squashes input to (0, 1), used in gates and binary output
- Tanh
  - Maths: tanh(x) = (eˣ − e⁻ˣ) / (eˣ + e⁻ˣ) — zero-centred, squashes to (−1, 1)
- Softmax
  - Maths: softmax(zᵢ) = eᶻⁱ / Σⱼ eᶻʲ — converts score vector to probability distribution
#### Learning Dynamics
- Forward pass
- Backpropagation
  - Maths: ∂L/∂w = (∂L/∂a) · (∂a/∂z) · (∂z/∂w) — chain rule decomposes gradient layer by layer
- Gradient descent
  - Maths: θ ← θ − η · ∇_θ L — shifts each parameter opposite to its gradient by step size η
- Learning rate
#### Key Distinctions
- Parameters vs. Hyperparameters
- Underfitting vs. Overfitting

### Loss Functions
- Mean Squared Error (MSE)
  - Maths: L = (1/n) Σᵢ (ŷᵢ − yᵢ)² — averages squared errors, penalises large deviations more
- Cross-entropy
  - Maths: L = −Σᵢ yᵢ log(ŷᵢ) — penalises low confidence on the correct class
- Binary cross-entropy
  - Maths: L = −[y log(ŷ) + (1−y) log(1−ŷ)] — divergence between predicted probability and binary label
- KL Divergence
  - Maths: D_KL(P ‖ Q) = Σₓ P(x) log(P(x)/Q(x)) — how much P diverges from reference Q

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
  - Maths: A(Q,K,V) = softmax(QKᵀ / √dₖ) · V — relevance scores scaled to prevent vanishing gradients
- Multi-head attention — parallel views
  - Maths: MultiHead(Q,K,V) = Concat(head₁,…,headₕ) Wᴼ where headᵢ = Attention(Q Wᵢᴼ, K Wᵢᴷ, V Wᵢᵛ)

### Text Representations
- One-hot encoding
- Word2Vec embeddings
- Dense semantic vectors
- Sentence Transformers

### Positional Encoding
- Sinusoidal (sin/cos functions)
  - Maths: PE(pos, 2i) = sin(pos / 10000^(2i/d)) ; PE(pos, 2i+1) = cos(pos / 10000^(2i/d))
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
  - Maths: L = E_q[log p_θ(x|z)] − D_KL(q_φ(z|x) ‖ p(z)) — maximise reconstruction while keeping latent close to Gaussian prior
- Smooth, structured latent space
- Applications: generation, anomaly detection

### Generative Adversarial Networks (GANs)
#### Architecture
- Generator — creates synthetic samples from noise
- Discriminator — real vs. fake classifier
- Minimax adversarial game
#### Loss Functions
- Jensen-Shannon Divergence (original)
  - Maths: JSD(P‖Q) = ½ D_KL(P‖M) + ½ D_KL(Q‖M), M=½(P+Q) — symmetric similarity between real and generated distributions
- Wasserstein distance (WGAN — more stable)
  - Maths: W(P,Q) = inf_{γ∈Π(P,Q)} 𝔼[‖x−y‖] — earth-mover distance, stable gradients even with disjoint support
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
  - Maths: q(xₜ|xₜ₋₁) = N(xₜ ; √(1−βₜ) xₜ₋₁ , βₜ I) — adds scheduled Gaussian noise; after T steps xₜ ≈ N(0,I)
- Destroys data structure progressively
#### Reverse Process
- Learns to denoise step-by-step
- p_θ(xₜ₋₁|xₜ) approximation
  - Maths: p_θ(xₜ₋₁|xₜ) = N(xₜ₋₁ ; μ_θ(xₜ,t) , Σ̃(t)) — neural network predicts mean of clean distribution
- Neural network predicts noise
#### Training
- L2 loss on predicted vs. true noise
  - Maths: L = ‖ μ_θ(xₜ, t) − μ̃(xₜ, x₀) ‖² — minimised across all timesteps
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
  - Maths: θ ← θ − η · ∇_θ L — parameter update opposite to gradient direction
- Adam / AdamW
  - Maths: mₜ=β₁mₜ₋₁+(1−β₁)gₜ ; vₜ=β₂vₜ₋₁+(1−β₂)gₜ² ; θₜ←θₜ₋₁−η·m̂ₜ/(√v̂ₜ+ε) — adapts lr per parameter using bias-corrected moments
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

## Maths
### Activation Functions
#### ReLU
- f(x) = max(0, x)
- Zero for negatives, identity for positives — removes negative activations and adds non-linearity

#### Sigmoid
- σ(x) = 1 / (1 + e⁻ˣ)
- Squashes any real value into (0, 1) — used for binary outputs and LSTM/GRU gates

#### Tanh
- tanh(x) = (eˣ − e⁻ˣ) / (eˣ + e⁻ˣ)
- Squashes values to (−1, 1) — zero-centred, preferred over sigmoid in hidden layers

#### Softmax
- softmax(zᵢ) = eᶻⁱ / Σⱼ eᶻʲ
- Converts a score vector into a probability distribution that sums to 1 — used at classification output

### Loss Functions
#### Mean Squared Error (MSE)
- L = (1/n) Σᵢ (ŷᵢ − yᵢ)²
- Averages squared prediction errors — penalises large deviations more heavily, used in regression

#### Binary Cross-Entropy
- L = −[y log(ŷ) + (1−y) log(1−ŷ)]
- Measures divergence between predicted probability and binary label — used in binary classifiers and GAN discriminator

#### Categorical Cross-Entropy
- L = −Σᵢ yᵢ log(ŷᵢ)
- Penalises low confidence on the correct class — standard for multi-class softmax output

#### KL Divergence
- D_KL(P ‖ Q) = Σₓ P(x) log(P(x) / Q(x))
- How much distribution P diverges from reference Q — used in VAE and Diffusion model objectives

### Backpropagation & Optimisation
#### Chain Rule (Backprop)
- ∂L/∂w = (∂L/∂a) · (∂a/∂z) · (∂z/∂w)
- Recursively decomposes the loss gradient layer by layer from output back to weights

#### Gradient Descent Update
- θ ← θ − η · ∇_θ L
- Shifts each parameter opposite to its gradient by step size η — the core weight update rule

#### Adam Optimizer
- mₜ = β₁ mₜ₋₁ + (1−β₁) gₜ  ← 1st moment (mean)
- vₜ = β₂ vₜ₋₁ + (1−β₂) gₜ²  ← 2nd moment (variance)
- θₜ ← θₜ₋₁ − η · m̂ₜ / (√v̂ₜ + ε)
- Adapts learning rate per parameter using bias-corrected gradient mean and variance estimates

### Attention Mechanism
#### Scaled Dot-Product Attention
- A(Q, K, V) = softmax(QKᵀ / √dₖ) · V
- Dot products between Q and K give relevance scores; scaling by √dₖ prevents vanishing gradients; V is aggregated by those weights

#### Multi-Head Attention
- headᵢ = Attention(Q Wᵢᴼ, K Wᵢᴷ, V Wᵢᵛ)
- MultiHead(Q,K,V) = Concat(head₁, …, headₕ) Wᴼ
- Runs h independent attention operations in parallel — each head learns different relational patterns

### Positional Encoding
#### Even dimensions — Sine
- PE(pos, 2i) = sin(pos / 10000^(2i/d))
- Encodes absolute position using a sine wave whose frequency decreases with dimension index i

#### Odd dimensions — Cosine
- PE(pos, 2i+1) = cos(pos / 10000^(2i/d))
- Paired with sine to give each position a unique, continuous signature across all dimensions

### Generative Model Equations
#### VAE — ELBO Loss
- L = E_q[log p_θ(x|z)] − D_KL(q_φ(z|x) ‖ p(z))
- Maximises reconstruction quality (1st term) while keeping latent distribution close to a unit Gaussian prior (2nd term)

#### Forward Diffusion — DDPM
- q(xₜ | xₜ₋₁) = N(xₜ ; √(1−βₜ) xₜ₋₁ , βₜ I)
- Adds scheduled Gaussian noise at each timestep t; βₜ controls noise magnitude — after T steps xₜ ≈ N(0,I)

#### Reverse Diffusion — DDPM
- p_θ(xₜ₋₁ | xₜ) = N(xₜ₋₁ ; μ_θ(xₜ, t) , Σ̃(t))
- Learned denoising step; neural network predicts the mean of the clean distribution conditioned on noisy input and timestep

#### Diffusion Training Objective (Simplified)
- L = ‖ μ_θ(xₜ, t) − μ̃(xₜ, x₀) ‖²
- L2 distance between predicted and true reverse-process mean — minimised across all timesteps

#### GAN — Jensen-Shannon Divergence
- JSD(P ‖ Q) = ½ D_KL(P ‖ M) + ½ D_KL(Q ‖ M), where M = ½(P+Q)
- Symmetric measure of similarity between real and generated distributions — minimised by the generator in original GAN

#### GAN — Wasserstein Distance (WGAN)
- W(P, Q) = inf_{γ ∈ Π(P,Q)} 𝔼_(x,y)~γ [‖x − y‖]
- Earth-mover distance between distributions — provides stable gradients even when P and Q have disjoint support, reducing mode collapse

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
