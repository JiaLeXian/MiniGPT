# MiniGPT: Efficient Intelligence Through Compact Architecture and Curated Data

**Jiale Xian**
Independent Research Project
January 2023

---

# Abstract

MiniGPT is an early investigation into efficient language modeling developed in January 2023. The project explores whether language-model capability can emerge through better architecture, better data selection, and better parameter efficiency rather than scaling parameter count alone.

The project was motivated by a simple question:

> Can intelligence become more efficient before it becomes larger?

MiniGPT combines a compact transformer architecture, a curated language-learning corpus, and a low-compute training regime to investigate alternative paths to language-model development.

The resulting model contains approximately **0.456 million parameters**, uses an **8-layer, 8-head transformer architecture**, and was trained on **miniText**, a carefully curated **1.3GB corpus containing 98.5 million characters**.

The model achieved validation loss in the range of **1.48–1.55** while using approximately **23× fewer parameters** than a common nanoGPT character-level baseline.

The work was later presented at the **Institute for Pure and Applied Mathematics (IPAM), UCLA** during *Mathematical Challenges and Opportunities for Autonomous Vehicles (AVRC2)* under the title:

**Efficient Language Models for Better Research**

---

# Research Motivation

Most progress in modern language models has come from increasing:

* parameter count
* training data
* compute budgets

MiniGPT explores a different direction.

Instead of asking:

> How can we make models larger?

MiniGPT asks:

> How can we make learning more efficient?

The project investigates four connected ideas:

### 1. Architecture Efficiency

Can transformer depth partially substitute for width?

### 2. Attention Efficiency

Can narrow attention heads remain effective when paired with sufficient depth?

### 3. Data Efficiency

Can carefully selected language outperform indiscriminate language collection?

### 4. Learning Efficiency

Can a compact model trained on a high-quality corpus generalize without dropout regularization?

---

# Core Research Thesis

MiniGPT is built around a broader hypothesis:

> Intelligence depends not only on scale, but also on structure, information quality, and learning efficiency.

This idea appears repeatedly throughout the project:

* compact architecture instead of larger architecture
* curated language instead of larger language corpora
* efficient learning instead of brute-force scaling
* reasoning-oriented language instead of indiscriminate web text

---

# Main Contributions

## Compact Transformer Architecture

MiniGPT explores a deeper, narrower GPT-style architecture containing approximately:

```text
0.456 million parameters
```

while maintaining competitive language-modeling performance.

---

## Curated Language Corpus

MiniGPT introduces **miniText**, a curated language-learning dataset designed around language quality rather than corpus size.

---

## Low-Compute Language Modeling

The project investigates how much language-model capability can be achieved under limited compute resources.

---

# Architectural Design

A common nanoGPT-style character-level baseline uses:

```text
n_layer = 6
n_head  = 6
n_embd  = 384
```

MiniGPT instead uses:

```text
n_layer = 8
n_head  = 8
n_embd  = 64
```

Resulting head dimension:

```text
head_size = 64 / 8 = 8
```

This architecture intentionally trades model width for depth.

The guiding hypothesis:

> A compact transformer with greater depth can use parameters more efficiently than a wider shallow architecture.

---

# Model Configuration

| Parameter           | Value                    |
| ------------------- | ------------------------ |
| Parameters          | 0.456M                   |
| Layers              | 8                        |
| Attention Heads     | 8                        |
| Embedding Dimension | 64                       |
| Head Dimension      | 8                        |
| Context Length      | 32                       |
| Vocabulary Size     | 430                      |
| Tokenization        | Character-level          |
| Architecture        | Decoder-only Transformer |

Each transformer block uses pre-layer normalization:

```text
x = x + SelfAttention(LayerNorm(x))
x = x + FeedForward(LayerNorm(x))
```

The model includes:

* causal self-attention
* residual connections
* feed-forward networks
* layer normalization
* autoregressive generation

---

# miniText Dataset

MiniGPT was trained on **miniText**, a custom language corpus containing:

```text
1.3 GB
98,553,672 characters
```

miniText was not designed as a maximum-scale dataset.

Instead, it was built around a language-learning principle:

> Not all books teach language equally well.

Some texts provide:

* richer vocabulary
* stronger grammar
* clearer structure
* higher-quality reasoning
* more transferable language patterns

Others contribute little to language acquisition despite increasing dataset size.

miniText was therefore curated to reduce:

* offensive language
* noisy web text
* crawl artifacts
* repetitive low-information content
* language with limited educational value

while preserving texts that contribute more effectively to language learning.

The dataset explores the hypothesis that:

> A smaller but better-selected corpus can teach language models more efficiently than a much larger unfiltered corpus.

Data-to-parameter ratio:

```text
98.5M characters / 0.456M parameters
≈ 216 characters per parameter
```

---

# Regularization Experiment

MiniGPT uses:

```text
dropout = 0.0
```

The model was intentionally trained without dropout regularization.

This configuration investigates whether:

> A compact model trained on a sufficiently large and carefully curated corpus can generalize without explicit dropout.

The resulting training regime can be summarized as:

```text
small model
+
curated corpus
+
zero dropout
```

---

# Training Setup

| Parameter              | Value           |
| ---------------------- | --------------- |
| Hardware               | NVIDIA Tesla T4 |
| Optimizer              | AdamW           |
| Learning Rate          | 1e-3            |
| Batch Size             | 16              |
| Context Length         | 32              |
| Training Iterations    | 70,000          |
| Dropout                | 0.0             |
| Estimated Compute Cost | ~$6,500 USD     |

---

# Results

Validation loss:

```text
1.48 – 1.55
```

## Parameter Comparison

| Model                      | Parameters |
| -------------------------- | ---------- |
| MiniGPT                    | 0.456M     |
| nanoGPT Character Baseline | ~10.65M    |

MiniGPT uses:

```text
4.3% of the parameters
```

or approximately:

```text
23× fewer parameters
```

than a common nanoGPT-style character-level baseline.

---

# Comparison with nanoGPT Character Models

| Metric              | nanoGPT Baseline       | MiniGPT                |
| ------------------- | ---------------------- | ---------------------- |
| Parameters          | ~10.65M                | 0.456M                 |
| Relative Size       | 100%                   | ~4.3%                  |
| Layers              | 6                      | 8                      |
| Heads               | 6                      | 8                      |
| Embedding Dimension | 384                    | 64                     |
| Dataset             | Tiny Shakespeare-scale | miniText (98.5M chars) |
| Dropout             | Standard               | 0.0                    |
| Validation Loss     | ~1.4–1.6               | 1.48–1.55              |

Although the datasets differ, MiniGPT demonstrates that competitive character-level language-modeling performance can be achieved using substantially fewer parameters when architecture and data quality become primary design variables.

---

# IPAM Presentation

Presented at:

**Institute for Pure and Applied Mathematics (IPAM), UCLA**

Program:

**Mathematical Challenges and Opportunities for Autonomous Vehicles (AVRC2)**

Date:

**June 12–16, 2023**

Presentation:

**Efficient Language Models for Better Research**

The presentation explored how efficient language models can support research workflows under limited compute resources.

---

# Research Themes

MiniGPT explores themes that remain active areas of AI research:

* Small Language Models (SLMs)
* Parameter-efficient transformers
* Efficient intelligence
* Data quality and curation
* Low-compute AI systems
* Architecture-driven scaling alternatives

---

# Conclusion

MiniGPT explores an alternative path for language-model development.

Rather than treating parameter count as the primary source of capability, the project investigates how:

* architecture
* data selection
* parameter efficiency
* and compute efficiency

interact to produce useful language-model behavior.

The broader question remains relevant today:

> How much intelligence can be achieved through better design before requiring larger scale?

---

## Author

**Jiale Xian**

Independent research project developed in January 2023 and presented at IPAM/UCLA in June 2023.
