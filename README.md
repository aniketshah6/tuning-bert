# tuning-bert
this repository contains files related to a text classification project

The competition can be found at https://www.kaggle.com/competitions/nlp-getting-started. 

# data:
The training data is a csv file with lines corresponding to each tweet, with the entries: 'id', 'keyword', 'location', 'text', and 'target'. The 'target' entry is 0 or 1 depending on whether the tweet referred to a real disaster or not. The test data was essentially the same but omitted the 'target' entry which was to be predicted.

# approach and results:
My approach was to tune a BERT model to do this. Huggingface has a wonderful tutorial available at https://huggingface.co/docs/transformers/tasks/sequence_classification, which I mostly followed. I merged everything into a string containing the location and keyword data before the text of the tweet, which was then tokenized, etc. To make the kaggle training data play well with the tensorflow dataset construction methods took some slight adjustments, but after this was done the model did reasonably well on the task with very little tuning (training for 3 epochs resulted in successful classification of 80.845% of the test set). 
