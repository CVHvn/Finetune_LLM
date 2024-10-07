# Vietnamese student feedback sentiment analytics
Finetune opensource llm like Qwen-2.5, Gemma-2, Phi-3, Llama-3, ... on Synthetic-vietnamese-students-feedback-corpus Dataset

# Introduction
This repos finetuned multiple LLM models with the ynthetic-vietnamese-students-feedback-corpus Dataset. I tried finetune full models (only small models like qwen 2 0.5B and 1.5B), lora and qlora.

# Dataset

## Synthetic-vietnamese-students-feedback-corpus Dataset

Synthetic-vietnamese-students-feedback-corpus Dataset is downloaded from [kaggle](https://www.kaggle.com/datasets/toreleon/synthetic-vietnamese-students-feedback-corpus/data)

This Dataset included student feedback with sentiment and topic of this feedback. The dataset is balanced with 8k training samples and 2k testing samples. 

Almost all feedback is short (longer feedback has 48 words).

# Motivation

I try fine-tuning LLM models to learn about LLM models and compare them with older structures like [e5 base](https://github.com/CVHvn/Vietnamese-text-classification) (1 kind of Roberta). Almost LLM have the same way of fine-tuning, then we can reuse my code for other models or other datasets.

# How to use it

Just run all my notebook.

# Result and experience

Most models have accuracy in the range (85%, 87%), lower than e5 base. The model after fine tuning can almost only understand the content related to this dataset. When I try the sentence "the food is delicious", many models automatically associate and interpret it according to the school topic (because the dataset is about school reviews). Although the model is less overfit than the base e5 (the llms after fine tuning can point out some incorrectly labeled sentences), it is still not good enough because of the dataset quality.

Finetune with lora gives as good quality as full model with qwen 2 0.5b and 1.5b (only in my test). Lora also helps save memory and storage without slowing down finetune speed (or not significantly).

Qlora significantly reduces memory by using 4 bits, but it slows down training speed a lot --> if you have enough gpu memory, I recommend only using lora for training.
