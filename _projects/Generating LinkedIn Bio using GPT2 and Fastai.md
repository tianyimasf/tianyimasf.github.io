---
name: "Generating LinkedIn Bio using GPT2 and Fast.ai"
image: ../assets/images/tokenizer.PNG
description: Fine-tuning LLM to generate stylized texts.
date: 2024-01-31
layout: post
index: 8
---

# Background

Fast.ai is a high-level deep learning framework built on PyTorch that is highly flexible and easy to use.
It's developed by Jeremy Howard, which also used this framework with some torch usage to teach an extensive
deep learning course that litearlly impacted people's deep learning career trajectories. It's so foundamental,
detailed, yet easy to understand and intuitive. And I'll use fast.ai to apply NLP techniques illustrated in
his book to fine-tune gpt2 to make it write LinkedIn profile for me!

# Basic fine-tuning of GPT2 using fast.ai

## Data preparation

LinkDB provides LinkedIn profile sample datasets for various countries. To view the datasets, here is the url:
https://nubela.co/blog/sample-data-for-linkdb/. I downloaded the US, Danish, Singapore, and Canadian datasets
so that I have 40,000 base profiles to filter from. I also tried to download some data through their APIs, which
proved to be too expensive. I did add the ones I got to the dataset.

I can access their profile bio by selecting the "summary" attribute in their profile objects. The data is initially
very messy as expected, so I wrote codes to clean the data. First, I filtered out null values, string consists of only
empty spaces, emails, urls, or punctuations and digits. I used regex to achieve this. Then I removed all formatting
of texts, since some of the texts used special fonts and made it impossible to detect language. Here, I'm removing
non-English summaries, since I don't want imbalanced classes -- the model would have to adapt to the other languages
too if I keep them, while not having enough data on those languages at the same time, making it hard to generate bios
in those languages.

Finally, I saved only the bios to a csv.

## Basic Fine-tuning using fast.ai and gpt2

Fast.ai makes it very easy to fine-tune a language model. Here I only did the very basic fine-tuning steps. It worked
well for sentences with 30 - 50 words. However, you can definitely see patterns in the generated sentences, and it's
bad for generating longer sentences. Later, I'll update with more complex tuning techniques and explanations.

Here, I followed the official guide from fast.ai: https://docs.fast.ai/tutorial.transformers.html

First, we import the pre-trained model:

```python
from transformers import GPT2LMHeadModel, GPT2TokenizerFast

pretrained_weights = 'gpt2'
tokenizer = GPT2TokenizerFast.from_pretrained(pretrained_weights)
model = GPT2LMHeadModel.from_pretrained(pretrained_weights)
```

Then we use fast.ai's `text` library to create a `DataLoader` object that has a number of attributes to be used when training the model.

## Preparing data using fast.ai

First we need to wrap torch's tokenizer into fast.ai's `Transform` object:

```python
from fastai.text.all import *

class TransformersTokenizer(Transform):
    def __init__(self, tokenizer): self.tokenizer = tokenizer
    def encodes(self, x):
        device = 'cuda' if torch.cuda.is_available() else 'cpu'
        toks = self.tokenizer.tokenize(x)
        return tensor(self.tokenizer.convert_tokens_to_ids(toks)).to(device).long()
    def decodes(self, x): return TitledStr(self.tokenizer.decode(x.cpu().numpy()))
```

We build the `DataLoader` step by step, first build a `TsfmList` which stands for "TransformedList":

```python
# split function that will be applied to split the dataset into train/val
splits = [range_of(train_len), list(range(train_len, l))]
tls = TfmdLists(bios, TransformersTokenizer(tokenizer), splits=splits, dl_type=LMDataLoader)
```

You can access the sequence ids like this:

![see data](../../assets/images/see_data.PNG)

And use `show_at()` to see the text version:

![show at](../../assets/images/show_at.PNG)

To finally build the `DataLoader`, we just need to specify the batch size and sequence length:

```python
bs,sl = 4,256
dls = tls.dataloaders(bs=bs, seq_len=sl)
```

## Fine-tuning the model

TBD
