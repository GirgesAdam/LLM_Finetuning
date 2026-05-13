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

## Model Details

- **Base model:** `Qwen/Qwen2.5-1.5B-Instruct`
- **Fine-tuning method:** LoRA / PEFT
- **Training framework:** LLaMA-Factory
- **Task type:** Supervised fine-tuning
- **Primary language:** Arabic
- **Output style:** Structured JSON-like responses
- **Evaluation loss:** `0.3492`

## Intended Use

This model is intended for experiments and educational projects involving Arabic news understanding.

Example use cases:

- Extracting structured metadata from Arabic news articles
- Identifying people, organizations, countries, topics, and events in news text
- Producing structured outputs from Arabic article content
- Translating or reformulating Arabic news content into structured multilingual outputs
- Demonstrating LoRA fine-tuning with LLaMA-Factory and Qwen2.5

## Not Intended For

This model should not be used as-is for high-stakes applications such as:

- Legal or political decision-making
- Financial decision-making
- Medical or safety-critical use
- Fully automated journalism or fact-checking
- Production systems without human review

The model may generate incorrect, incomplete, or hallucinated information.

## Training and Evaluation Data

The model was fine-tuned on an internal Arabic news instruction dataset named `news_finetune_train`.

The dataset follows an instruction-tuning format with fields similar to:

```json
{
  "instruction": "Extract structured information from the Arabic news article.",
  "input": "Arabic news article text...",
  "output": "{...structured response...}"
}
