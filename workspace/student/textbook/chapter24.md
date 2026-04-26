# Chapter 24: Deep Learning for Natural Language Processing
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## From Shallow to Deep NLP

Classical NLP relied on hand-crafted features (bag-of-words, n-grams, parse features) combined with traditional classifiers (SVM, CRF, logistic regression).

**Deep learning transformed NLP** by learning representations automatically from raw text — eliminating feature engineering and achieving state-of-the-art on nearly every benchmark.

## Word Embeddings

### Word2Vec (Mikolov et al., 2013)
Two architectures:
- **CBOW (Continuous Bag of Words):** Predict target word from context words.
- **Skip-gram:** Predict context words from target word.

Training: gradient descent on large corpora; the *representation* (embedding) is the byproduct.

**Key properties:**
- Semantic similarity: similar words have similar vectors.
- Analogical reasoning: king − man + woman ≈ queen.
- Dimension: typically 100–300.

### GloVe (Global Vectors)
- Factorize the word co-occurrence matrix.
- Combines global statistics (matrix factorization) with local context (Word2Vec).

### Subword Embeddings (FastText)
- Represent words as sums of character n-gram vectors.
- Handles out-of-vocabulary words and morphological variants.

## Recurrent Models for NLP

### Sequence-to-Sequence (Seq2Seq)
- **Encoder:** Read input sequence, produce fixed-length context vector (final hidden state).
- **Decoder:** Generate output sequence conditioned on context vector.
- Applications: Machine translation, summarization, dialogue.

**Problem:** Fixed-length context vector is a bottleneck for long sequences.

### Attention (Bahdanau, 2014)
- Allow decoder to attend to all encoder hidden states at each decoding step.
- Attention weights: αᵢⱼ = softmax(score(sᵢ, hⱼ)) — how relevant is encoder position j at decoder step i?
- Context vector: cᵢ = Σⱼ αᵢⱼ hⱼ.
- **Visualizable:** Attention weights show alignment between source and target.

## The Transformer
(Vaswani et al., "Attention Is All You Need," 2017)

Replaces all recurrence with **self-attention** — revolutionized NLP and beyond.

### Architecture

**Encoder stack (BERT-style):**
- Each layer: Multi-Head Self-Attention + Feed-Forward Network.
- Residual connections and layer normalization around each sub-layer.

**Decoder stack (GPT-style):**
- Each layer: Masked Self-Attention + Cross-Attention (over encoder) + Feed-Forward.
- Masking ensures autoregressive generation (can only attend to previous tokens).

### Self-Attention
Each token creates Query (Q), Key (K), Value (V) vectors via linear projections.

Attention(Q, K, V) = softmax(QKᵀ / √d_k) V

- Q·Kᵀ: similarity between all pairs of tokens.
- Softmax: attention weights.
- ×V: weighted combination of value vectors.

**Multi-head attention:** Run h attention heads with different Q, K, V projections; concatenate and project.
- Different heads capture different types of relationships (syntax, coreference, semantics).

### Positional Encoding
Transformers have no inherent position awareness — add position information via:
- **Sinusoidal encoding (original Transformer):** Fixed trigonometric functions of position.
- **Learned positional embeddings (BERT, GPT):** Trainable position vectors.
- **Relative positional encodings (T5, RoPE):** Encode relative distance between tokens.

### Computational Complexity
- Self-attention: O(n²d) per layer — quadratic in sequence length.
- **Limitation for long sequences:** Efficient attention variants (Longformer, BigBird, FlashAttention) reduce this.

## Pre-trained Language Models

### BERT (Devlin et al., 2018)
- **Bidirectional Encoder Representations from Transformers.**
- Pre-training objectives:
  1. **Masked Language Modeling (MLM):** Predict randomly masked tokens.
  2. **Next Sentence Prediction (NSP):** Predict if sentence B follows sentence A.
- Architecture: 12 or 24 Transformer encoder layers.
- **Fine-tuning:** Add a task-specific head; fine-tune all parameters on labeled data.
- BERT dominated NLU benchmarks (GLUE, SQuAD) in 2018-2019.

### GPT Series (Radford et al., 2018–2023)
- **Unidirectional autoregressive decoder.**
- Pre-training: Predict next token; trained on massive web corpora.
- GPT-2 (117M → 1.5B params): Generated fluent text; released cautiously.
- GPT-3 (175B params): **In-context learning** — perform tasks from a few examples in the prompt (few-shot) without fine-tuning.
- GPT-4: Multimodal; near-human on many benchmarks.

### T5 (Raffel et al., 2019)
- **Text-to-Text Transfer Transformer.**
- Frames all NLP tasks as text-to-text: input = "translate English to French: {text}", output = translation.
- Enables unified training and fine-tuning for all tasks.

### RoBERTa, ALBERT, DeBERTa
- Variants of BERT with improved training procedures, efficiency, or architecture.

## Scaling Laws

**Kaplan et al. (2020) and Hoffmann et al. (2022, "Chinchilla"):**
- Model performance scales predictably with: model parameters N, training data tokens D, and compute C.
- **Optimal training:** For a compute budget C, train a model of N parameters on ~20×N tokens (Chinchilla law).
- Larger models need proportionally more data.
- Emergent capabilities appear at sufficient scale.

## Prompt Engineering and In-Context Learning

- **Zero-shot:** Describe the task in the prompt; model performs it without examples.
- **Few-shot:** Provide 1–100 input-output examples in the prompt.
- **Chain-of-Thought (CoT):** Prompt the model to reason step-by-step before answering.
- **Instruction tuning:** Fine-tune on a large set of (instruction, response) pairs — improves zero-shot generalization.
- **RLHF:** Fine-tune with human preference feedback to improve helpfulness and safety.

## Key Applications

- **Text summarization:** Extractive (select sentences) or abstractive (generate new text).
- **Dialogue systems:** Task-oriented (slot filling) and open-domain (chit-chat, ChatGPT).
- **Information retrieval:** Dense retrieval using BERT-like encoders; RAG.
- **Code generation:** Codex, GitHub Copilot, Claude Code — trained on code corpora.
- **Multimodal:** CLIP (image-text alignment), DALL-E, GPT-4V — language + vision.

## Key Terms

- **Transformer:** Attention-based architecture; replaces recurrence with self-attention.
- **Self-attention:** Each token computes attention over all other tokens using Q, K, V projections.
- **BERT:** Bidirectional encoder; pre-trained with MLM and NSP; fine-tuned for tasks.
- **GPT:** Autoregressive decoder; pre-trained on next-token prediction; few-shot via prompting.
- **Scaling laws:** Model performance predictably improves with size, data, and compute.
- **In-context learning:** Learning from examples provided in the prompt, no gradient updates.
- **Chain-of-Thought:** Prompting technique eliciting step-by-step reasoning.
- **RLHF:** Reinforcement Learning from Human Feedback — aligns LLMs with human preferences.
