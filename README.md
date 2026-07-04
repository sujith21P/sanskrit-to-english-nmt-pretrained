# Sanskrit-to-English Neural Machine Translation Pipeline

This repository contains the implementation, evaluation pipeline, and inference configurations for a Sanskrit-to-English Neural Machine Translation (NMT) system, developed as part of the Natural Language Understanding (NLU) curriculum.

## 🛠️ Model Architecture & Specifications

The translation core leverages the highly scalable **615 Million parameter distilled variant of Meta's No Language Left Behind (NLLB-200)** architecture. By utilizing a full-scale 615M parameter model rather than a sub-scale ~11.4M model, the pipeline effectively maps the deep morphological complexities, nominal declensions, and intricate sandhi structures of classical Sanskrit into coherent English syntactical representations.

### Model Metrics & Parameter Breakdown

| Metric / Specification | Details |
| :--- | :--- |
| **Model Family** | Meta NLLB-200 (No Language Left Behind) |
| **Hugging Face Hub Checkpoint** | `facebook/nllb-200-distilled-600M` |
| **Total Parameter Count** | **~615 Million** (615,033,984 parameters) |
| **Architecture Layout** | Sequence-to-Sequence (Seq2Seq) Encoder-Decoder Transformer |
| **Tokenizer Subsystem** | SentencePiece Unified Vocabulary |
| **Target Task Target** | Cross-Lingual Machine Translation (Sanskrit $\rightarrow$ English) |

---

## ⚙️ Inference & Decoding Configuration

To optimize translation quality and prevent degenerate repetition common in cross-lingual generation, the inference routine is strictly bounded by an explicit **Beam Search** decoding tree:

* **Beam Width:** 5 (Tracks top-5 candidate sequences simultaneously)
* **Length Penalty:** 1.0 (Ensures proper balance between summary and sentence expansion)
* **Non-Repetition Constraint:** Strict 3-gram blocking rules applied over the autoregressive decoder steps to prevent structural looping patterns.
