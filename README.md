# NLP: Aspect Category Sentiment Analysis (ACSA)

## Project Description
This project aims to solve the Subtask 4 in SemEval 2014 Task 4 - Aspect Based Sentiment Analysis

Sentiment analysis is increasingly viewed as a vital task both from an academic and a commercial standpoint. The majority of existing evaluations in Sentiment Analysis (SA) are aimed at evaluating the overall polarity of a sentence, paragraph, or text span. In contrast, this task will provide evaluation for detecting aspects and the sentiment expressed towards each aspect.

The Subtask 4 is Aspect category polarity or Aspect category sentiment analysis (ACSA): 
Given a set of pre-identified aspect categories (e.g., {food, price}), determine the polarity (positive, negative, neutral or conflict) of each aspect category. For example:
- “The restaurant was too expensive” → {price: negative}
- “The restaurant was expensive, but the menu was great” → {price:negative, food: positive}

## Methodology 
For ACSA task, I used BART pre-training model. I took references from the great paper Solving Aspect Category Sentiment Analysis as a Text Generation Task (Liu, 2021).

The model can be described shortly as below: 

Step 1 –Template sentences + Tokenization

<img src="images/Step1.png" width = "1000">

Step 2 – Sentiment generation

2.1 Encoder: Input tokenized original sentences and output hidden states.

2.2 Decoder:
- Input hidden states + tokenized template sentences (without the polarity word)
- Calculate the templates’ score with the three polarity words
- Choose the polarity with the highest score.
- Output sentiment word.
<img src="images/Step2.png" width = "1000">

## Data
The dataset I used in this task is SemEval 2016.

## Model result
My BART seq2seq model achieved 87.4% accuracy on the validation test and 85.5% on the test set.

## Future works
- I detected some errors of the labels in the training dataset. I believe the model test accuracy can be improved with data of better annotation. 
- In addition, the training dataset is very imbalanced, with less data for neutral polarity. We can consider oversampling methods in the future training.  
- I notice the model tends to performe worst in predicting the opinion of a sentence with both positive and negative meanings. Therefore, if the model is trained with more of such sentences,  the model can be more generalized and achieve a better performance. 

# References
- SemEval 2014 Task 4 - Aspect Based Sentiment Analysis: https://www.aclweb.org/portal/content/semeval-2014-task-4-aspect-based-sentiment-analysis
- Jian Liu et.al, 2021, Solving Aspect Category Sentiment Analysis as a Text Generation Task: https://aclanthology.org/2021.emnlp-main.361/, including Github repository at https://github.com/lgw863/acsa-generation)
