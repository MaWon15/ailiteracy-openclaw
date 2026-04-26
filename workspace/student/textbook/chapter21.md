# Chapter 21: Deep Learning
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## Neural Networks Foundations

**Artificial neural network (ANN):** A network of interconnected units (neurons) loosely inspired by the brain.

### Perceptron (single layer)
- Inputs: x₁, ..., xₙ.
- Weights: w₁, ..., wₙ and bias w₀.
- Output: h_w(x) = g(w₀ + Σᵢ wᵢxᵢ) where g is an **activation function**.
- **Perceptron learning rule:** Adjust weights based on error.
- **Limitation (Minsky & Papert, 1969):** Cannot learn XOR — only linearly separable functions.

### Multilayer Perceptron (MLP / Feedforward Network)
- Input layer → hidden layer(s) → output layer.
- Hidden layers enable learning nonlinear functions.
- **Universal approximation theorem:** A single hidden layer with enough units can approximate any continuous function to arbitrary precision.

## Activation Functions

| Function | Formula | Properties |
|---|---|---|
| Sigmoid | 1/(1+e^(-z)) | Output ∈ (0,1); vanishing gradient at extremes |
| Tanh | (e^z − e^(-z))/(e^z + e^(-z)) | Output ∈ (−1,1); zero-centered |
| ReLU | max(0, z) | Simple; avoids vanishing gradient; default for hidden layers |
| Leaky ReLU | max(0.01z, z) | Avoids "dead ReLU" problem |
| Softmax | e^(zᵢ)/Σⱼ e^(zⱼ) | Output layer for multiclass; produces probabilities |

## Training Neural Networks

### Loss Functions
- **Cross-entropy:** For classification: L = −Σᵢ yᵢ log ŷᵢ.
- **MSE:** For regression: L = (1/n) Σᵢ (yᵢ − ŷᵢ)².

### Backpropagation
Efficient computation of gradients via the **chain rule**:
1. **Forward pass:** Compute activations and loss.
2. **Backward pass:** Propagate error gradients from output to input using chain rule.
3. Update weights: wᵢ ← wᵢ − α × ∂L/∂wᵢ.

Time complexity: O(W) per example where W = number of weights.

### Optimization Algorithms
- **Stochastic Gradient Descent (SGD):** Update on individual examples or mini-batches.
- **Momentum:** Accumulate gradient direction to speed up convergence.
- **Adam:** Adaptive learning rates per parameter; momentum + RMSProp. Default optimizer for deep learning.
- **Learning rate scheduling:** Warm-up then decay; cosine annealing.

### Regularization
- **L2 (weight decay):** Penalize large weights; shrinks toward zero.
- **L1:** Encourages sparsity.
- **Dropout:** Randomly zero out units during training; forces redundant representations.
- **Batch Normalization:** Normalize activations within a mini-batch; stabilizes training.
- **Early stopping:** Stop when validation loss stops improving.
- **Data augmentation:** Artificially increase training set (flips, crops, noise).

## Convolutional Neural Networks (CNNs)

Designed for structured grid data (images, audio, video).

### Key Operations
- **Convolution layer:** Applies a learned filter (kernel) at each position.
  - Learns local features; weights shared across spatial positions.
  - Parameters: filter size, number of filters, stride, padding.
- **Pooling layer:** Downsample feature maps (max pooling, average pooling).
  - Reduces spatial size; provides translation invariance.
- **Fully connected layer:** Standard MLP at the end for classification.

### Properties
- **Weight sharing:** Same filter applied everywhere → fewer parameters.
- **Translation equivariance:** Features detected regardless of position.

### Notable Architectures
- **LeNet (1998):** First successful CNN for digit recognition.
- **AlexNet (2012):** Won ImageNet; sparked deep learning revolution.
- **VGGNet:** Very deep networks with small (3×3) filters.
- **ResNet (2015):** Residual connections — skip connections allow very deep networks (100+ layers).
- **EfficientNet:** Systematically scaled depth, width, and resolution.

## Recurrent Neural Networks (RNNs)

Designed for sequential data — the hidden state carries information across timesteps.

**Basic RNN:**
- hₜ = g(Wₕ hₜ₋₁ + Wₓ xₜ + b) — hidden state updated at each step.
- Output: yₜ = Wᵧ hₜ.

**Problem: Vanishing/exploding gradients** — gradients shrink or explode exponentially over long sequences.

### LSTM (Long Short-Term Memory)
- **Cell state:** Long-term memory.
- **Three gates:**
  - **Forget gate:** Decide what to erase from cell state.
  - **Input gate:** Decide what to write to cell state.
  - **Output gate:** Decide what to output.
- Effectively maintains gradients over hundreds of timesteps.
- Standard RNN for most sequential tasks before Transformers.

### GRU (Gated Recurrent Unit)
- Simplified LSTM: Combines forget and input gates into one **update gate**.
- Fewer parameters; often comparable performance.

## Attention Mechanisms and Transformers

### Attention
Allows the model to focus on relevant parts of the input when producing each output.

**Scaled dot-product attention:**  
Attention(Q, K, V) = softmax(QKᵀ/√d_k) V

- Q = queries, K = keys, V = values — all linear projections of the input.
- Computes a weighted sum of values, weighted by query-key similarity.

### Transformer Architecture (Vaswani et al., 2017)
- Replaces recurrence with **self-attention** — every token attends to all others.
- **Multi-head attention:** Multiple attention heads capture different relationships.
- **Positional encoding:** Injects position information (not inherent in attention).
- **Layer normalization + residual connections.**
- **Feed-forward sub-layer** applied position-wise.

**Advantages over RNNs:**
- Parallelizable (no sequential dependency).
- Long-range dependencies handled directly.
- Scales to very large models.

### Foundation Models and Large Language Models (LLMs)
- **BERT (2018):** Bidirectional encoder; pre-trained on masked language modeling.
- **GPT series:** Unidirectional decoder; autoregressive language model.
- **T5:** Encoder-decoder; treats all tasks as text-to-text.
- **Pre-training + fine-tuning:** Pre-train on large corpus, fine-tune on downstream task.
- **Emergent capabilities:** Arise at scale — in-context learning, chain-of-thought reasoning.

## Generative Models

### Variational Autoencoders (VAEs)
- Encoder maps x to a latent distribution q(z|x).
- Decoder samples z and reconstructs x.
- Trained by ELBO: reconstruction loss + KL divergence (regularization).

### Generative Adversarial Networks (GANs)
- **Generator G:** Maps noise z to fake samples.
- **Discriminator D:** Distinguishes real from fake.
- **Min-max game:** G minimizes, D maximizes log likelihood of correct classification.
- Training challenges: mode collapse, instability.
- Applications: Image synthesis (DALL-E ancestors), data augmentation.

### Diffusion Models
- Gradually add noise to data; train to reverse the noising process.
- State-of-the-art image and audio generation (DALL-E 2, Stable Diffusion, Midjourney).

## Key Terms

- **Backpropagation:** Efficient gradient computation via the chain rule.
- **CNN:** Uses convolution and pooling for spatial data; weight sharing.
- **LSTM:** RNN variant with gates to manage long-term dependencies.
- **Transformer:** Attention-based architecture; parallelizable; dominates NLP and vision.
- **ResNet:** Residual connections allow training of very deep networks.
- **Dropout / Batch Normalization:** Regularization and training stability techniques.
- **Foundation model / LLM:** Large pre-trained model adapted to many downstream tasks.
- **GAN / Diffusion model:** Generative models for synthesis tasks.
