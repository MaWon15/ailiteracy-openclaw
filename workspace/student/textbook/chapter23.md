# Chapter 23: Natural Language Processing
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## Why NLP Is Hard

Natural language understanding is difficult because language is:
- **Ambiguous:** "I saw the man with the telescope" — who has the telescope?
- **Context-dependent:** "It's cold in here" may be a request to close a window.
- **Underspecified:** "The chicken is ready to eat."
- **Ever-evolving:** New words, slang, idioms.
- **Requires world knowledge:** "John picked up the ball. He threw it." — who threw what?

## Language Models

A **language model** assigns probabilities to sequences of words.

### N-gram Language Models
- **Markov assumption:** P(wₙ | w₁, ..., wₙ₋₁) ≈ P(wₙ | wₙ₋₁) (bigram) or P(wₙ | wₙ₋₂wₙ₋₁) (trigram).
- **Training:** Estimate probabilities from corpus word counts.
- **Smoothing:** Required to handle unseen n-grams (Laplace, Kneser-Ney).
- **Perplexity:** Evaluation metric — 2^H where H is cross-entropy; lower is better.

**Limitations:** Cannot model long-range dependencies; data sparsity for large n.

### Neural Language Models
- **Word embeddings (Word2Vec, GloVe):** Represent words as dense vectors in a semantic space.
  - Words with similar meanings have similar vectors.
  - Arithmetic: king − man + woman ≈ queen.
- **RNN language models:** Maintain a hidden state across all previous tokens.
- **Transformer language models:** Self-attention captures arbitrary-distance dependencies.

## Text Classification

Assign a category to a text document.

- **Bag of words (BoW):** Represent document as word frequency vector; ignore order.
- **TF-IDF:** Weight terms by frequency in document × inverse document frequency.
- Classifiers: Naive Bayes, logistic regression, SVM, CNN, BERT fine-tuning.
- Applications: Spam detection, sentiment analysis, topic classification.

## Parsing and Syntactic Analysis

### Context-Free Grammars (CFGs)
- Rules: S → NP VP, NP → Det N, VP → V NP, etc.
- **Parse tree:** Hierarchical structure of a sentence.
- **Ambiguity:** Most sentences have multiple parse trees; need to choose most likely.

### Probabilistic CFG (PCFG)
- Each grammar rule has a probability; probability of a parse = product of rule probabilities.
- **CYK algorithm:** Dynamic programming parser for CFGs in O(n³|G|) time.
- **Earley algorithm:** Handles all CFGs including ambiguous ones.

### Dependency Parsing
- Models grammatical dependencies between words (subject, object, modifier relations) as a directed graph.
- **Arc-eager / transition-based parsing:** Shift-reduce parser; neural models.
- **Graph-based parsing:** Find maximum spanning tree of dependency graph.

## Semantic Analysis

Understanding the *meaning* of text.

### Word Sense Disambiguation (WSD)
- Words have multiple meanings ("bank" as financial or river bank).
- Lesk algorithm: overlap between dictionary definitions and context.
- Neural models use contextual embeddings (BERT encodes meaning in context).

### Semantic Role Labeling (SRL)
- Identify who does what to whom: Agent, Patient, Instrument, Location, Time.
- E.g., "John ate the pizza" → Agent=John, Theme=pizza, Predicate=ate.

### Named Entity Recognition (NER)
- Identify and classify named entities: PERSON, ORGANIZATION, LOCATION, DATE, etc.
- Sequence labeling problem; solved with CRFs, BiLSTMs, Transformers.

### Coreference Resolution
- Identify which phrases refer to the same entity.
- "John threw the ball. He caught it." → He=John, it=ball.

## Information Extraction

Extract structured information from unstructured text.

- **Relation extraction:** Identify relations between entities (Obama born_in Hawaii).
- **Open Information Extraction (OpenIE):** Extract (subject, relation, object) triples at scale.
- **Event extraction:** Identify events and their participants.

## Question Answering

- **Extractive QA:** Find a span in a passage that answers the question.
  - SQuAD dataset; BERT-style models achieve human-level performance.
- **Open-domain QA:** Retrieve relevant documents; extract or generate answer.
  - Retrieval-Augmented Generation (RAG): retrieve context, then generate answer.
- **Reading comprehension:** Requires multi-step reasoning across multiple sentences.

## Machine Translation

Map text from source language to target language.

### Statistical Machine Translation (SMT)
- **Noisy channel model:** P(target | source) ∝ P(source | target) × P(target).
- Phrase-based models; word alignment models (IBM models).

### Neural Machine Translation (NMT)
- **Encoder-decoder architecture:** Encoder reads source; decoder generates target.
- **Attention mechanism (Bahdanau, 2014):** Decoder attends to different parts of the source for each output word. Major improvement over fixed context vector.
- **Transformer-based NMT:** State-of-the-art; Google Translate, DeepL.

## Sentiment Analysis

Classify the sentiment expressed in text (positive/negative/neutral).

- **Lexicon-based:** Count positive/negative words.
- **ML-based:** Train classifiers on labeled reviews.
- **Aspect-based:** Identify sentiment toward specific aspects ("The food was great but service was slow").

## Key Terms

- **N-gram model:** Markov chain approximation to language; probability of each word given n−1 prior words.
- **Word embedding:** Dense vector representation of words capturing semantic similarity.
- **PCFG:** Probabilistic Context-Free Grammar for syntactic parsing.
- **Named Entity Recognition (NER):** Identify and classify named entities in text.
- **Coreference resolution:** Determine which mentions refer to the same entity.
- **Machine translation:** Sequence-to-sequence mapping with attention/Transformer.
- **Retrieval-Augmented Generation (RAG):** QA approach combining document retrieval with generative models.
