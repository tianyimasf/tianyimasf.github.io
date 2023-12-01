---
name: "Full Stack Deep Shroom: 9 Species & 280 Species"
image: ../assets/images/280_mushroom_species_classifier.PNG
description: A North EU mushroom image classifier trained on a FGVCx dataset with fastai and ResNet34.
date: 2023-05-21
layout: post
---

# Project Deep Shroom: 9 Species & 280 Species

## 9 Species

Using fast.ai, trained a ResNet18 model on a Kaggle dataset consists of 9 different folders that contains from 300 to 1500 selected images of corresponding mushrooms genuses, labels indicated by folder names. Deployed and published using Gradio on Hugging Face: [here](https://huggingface.co/spaces/tymasf/fungi-classification)(restart the app if it's sleeping). Achieved accuracy of 0.8323 and near perfect top 3 accuracy of 0.9627.

![hugging face 9](../../assets/images/9_species_mushroom_classification.PNG)

## 280 Species

Using Python and fast.ai, pre-processed and trained a ResNet34 model on a FGVCx dataset with 280 different mushroom species and around 45,000 different mushroom images, labels indicated by folder names. Deployed and published using Gradio on Hugging Face: [here](https://huggingface.co/spaces/tymasf/fungi-classification-280-species)(restart the app if it's sleeping), specifically its "Block" concept that is more complicated but more flexible than "Interface". Achieved Accuracy: 0.5654 and Top 5 Accuracy: 0.8347.

![hugging face 280](../../assets/images/280_mushroom_species_classifier.PNG)

[Kaggle Notebook (train & save model) (9 Species)](https://www.kaggle.com/tianyimasf/deep-shroom-classification-using-fast-ai)

[Github (280 Species)](https://huggingface.co/spaces/tymasf/fungi-classification-280-species/tree/main)
