# tuning-bert
this repository contains files related to a text classification project

The competition can be found at https://www.kaggle.com/competitions/nlp-getting-started. In short, the objective is use to the text, location, and keyword data of a tweet to determine whether it refers to a (real) disaster or not. 

My approach was to tune a BERT model to do this. Huggingface has a wonderful tutorial available at https://huggingface.co/docs/transformers/tasks/sequence_classification, which I mostly followed.

The input to the model was simply a string containing the location and keyword data before the text of the tweet, which was then tokenized, etc. To make the kaggle training data play well with the tensorflow dataset construction methods took some slight adjustments, but after this was done the model did reasonably well on the task with very little tuning (training for 3 epochs resulted in successful classification of 80.845% of the test set). 
