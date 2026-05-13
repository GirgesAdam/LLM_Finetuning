---
library_name: peft
license: other
base_model: Qwen/Qwen2.5-1.5B-Instruct
tags:
- llama-factory
- peft
- lora
- qwen
- qwen2.5
- arabic
- news
- information-extraction
- structured-generation
- text-generation
model-index:
- name: arabic-news-qwen2.5-lora
  results:
  - task:
      type: text-generation
      name: Structured Arabic News Generation
    dataset:
      name: news_finetune_train
      type: private
    metrics:
    - type: loss
      value: 0.3492
      name: Validation Loss
---

# Arabic News Qwen2.5 LoRA Fine-Tune

This repository contains a LoRA adapter fine-tuned from [`Qwen/Qwen2.5-1.5B-Instruct`](https://huggingface.co/Qwen/Qwen2.5-1.5B-Instruct) for structured Arabic news processing.

The model was fine-tuned to follow instructions related to Arabic news articles, including structured information extraction and multilingual news translation tasks.

This is a **PEFT/LoRA adapter**, not a full standalone model. To use it, load the base model first, then apply this adapter.

---

## Model Details

- **Base model:** `Qwen/Qwen2.5-1.5B-Instruct`
- **Fine-tuning method:** LoRA / PEFT
- **Training framework:** LLaMA-Factory
- **Task type:** Supervised fine-tuning
- **Primary language:** Arabic
- **Output style:** Structured JSON-like responses
- **Evaluation loss:** `0.3492`

---

## Intended Use

This model is intended for experiments and educational projects involving Arabic news understanding.

Example use cases:

- Extracting structured metadata from Arabic news articles
- Identifying people, organizations, countries, topics, and events in news text
- Producing structured outputs from Arabic article content
- Translating or reformulating Arabic news content into structured multilingual outputs
- Demonstrating LoRA fine-tuning with LLaMA-Factory and Qwen2.5

---

## Not Intended For

This model should not be used as-is for high-stakes applications such as:

- Legal or political decision-making
- Financial decision-making
- Medical or safety-critical use
- Fully automated journalism or fact-checking
- Production systems without human review

The model may generate incorrect, incomplete, or hallucinated information.

---

## Training and Evaluation Data

The model was fine-tuned on an internal Arabic news instruction dataset named `news_finetune_train`.

The dataset follows an instruction-tuning format with fields similar to:

```json
{
  "instruction": "Extract structured information from the Arabic news article.",
  "input": "Arabic news article text...",
  "output": "{...structured response...}"
}
```

The full training dataset is not included in this repository because of size and licensing considerations.

A small sample dataset may be provided in:

```text
data/sample/
```

---

## Training Procedure

The model was trained using LLaMA-Factory with PEFT LoRA fine-tuning.

### Training Hyperparameters

| Hyperparameter | Value |
|---|---:|
| Learning rate | `0.0001` |
| Train batch size | `1` |
| Eval batch size | `1` |
| Gradient accumulation steps | `4` |
| Total train batch size | `4` |
| Optimizer | `AdamW` |
| Adam beta1 | `0.9` |
| Adam beta2 | `0.999` |
| Adam epsilon | `1e-08` |
| LR scheduler | `cosine` |
| Warmup ratio | `0.1` |
| Epochs | `3.0` |
| Seed | `42` |

---

## Training Results

The model achieved the following final evaluation result:

```text
Validation Loss: 0.3492
```

Best logged validation loss:

```text
0.3214 at step 1300
```

### Training Log

| Training Loss | Epoch  | Step | Validation Loss |
|:-------------:|:------:|:----:|:---------------:|
| 0.4779 | 0.1481 | 100  | 0.4030 |
| 0.3938 | 0.2963 | 200  | 0.3865 |
| 0.5203 | 0.4444 | 300  | 0.3678 |
| 0.4821 | 0.5926 | 400  | 0.3523 |
| 0.3828 | 0.7407 | 500  | 0.3403 |
| 0.4154 | 0.8889 | 600  | 0.3397 |
| 0.2703 | 1.0370 | 700  | 0.3361 |
| 0.2253 | 1.1852 | 800  | 0.3383 |
| 0.2677 | 1.3333 | 900  | 0.3323 |
| 0.2723 | 1.4815 | 1000 | 0.3259 |
| 0.3145 | 1.6296 | 1100 | 0.3277 |
| 0.2413 | 1.7778 | 1200 | 0.3238 |
| 0.2920 | 1.9259 | 1300 | 0.3214 |
| 0.1336 | 2.0741 | 1400 | 0.3490 |
| 0.1882 | 2.2222 | 1500 | 0.3506 |
| 0.1967 | 2.3704 | 1600 | 0.3506 |
| 0.2248 | 2.5185 | 1700 | 0.3511 |
| 0.1419 | 2.6667 | 1800 | 0.3490 |
| 0.1606 | 2.8148 | 1900 | 0.3498 |
| 0.1919 | 2.9630 | 2000 | 0.3491 |

---

## Inference Example

### Input

```text
أعلنت وزارة الصحة عن إطلاق حملة وطنية جديدة للتطعيم في مختلف المحافظات، بهدف زيادة معدلات الوقاية وتحسين الخدمات الصحية للمواطنين.
```

### Expected Output

```json
{
  "title": "إطلاق حملة وطنية جديدة للتطعيم",
  "summary": "أعلنت وزارة الصحة عن حملة وطنية للتطعيم تهدف إلى زيادة معدلات الوقاية وتحسين الخدمات الصحية.",
  "category": "health",
  "language": "ar",
  "organizations": [
    "وزارة الصحة"
  ],
  "locations": [],
  "people": [],
  "topics": [
    "الصحة",
    "التطعيم",
    "الخدمات الصحية"
  ],
  "sentiment": "neutral"
}
```

---

## Output Files

After training, the project produces files such as:

```text
adapter_model.safetensors      # LoRA adapter weights
adapter_config.json            # LoRA adapter configuration
train_results.json             # Training metrics
eval_results.json              # Evaluation metrics
trainer_state.json             # Trainer state and logs
trainer_log.jsonl              # Detailed trainer logs
training_loss.png              # Training loss chart
training_eval_loss.png         # Evaluation loss chart
```

---

## Framework Versions

- PEFT `0.12.0`
- Transformers `4.48.2`
- PyTorch `2.5.1+cu124`
- Datasets `3.2.0`
- Tokenizers `0.21.0`

---

## Acknowledgements

This project uses:

- [`Qwen/Qwen2.5-1.5B-Instruct`](https://huggingface.co/Qwen/Qwen2.5-1.5B-Instruct)
- PEFT / LoRA
- LLaMA-Factory
- Hugging Face Transformers
