# tuning-bert
This repository contains files to produce an entry to the introductory NLP kaggle competition. The details of the competition, including data, can be found at https://www.kaggle.com/competitions/nlp-getting-started, but to briefly summarize, the goal of the competition is to determine whether a given tweet in some collection is about a (real) disaster, or not. 

# data:
The training data is a csv file with lines corresponding to each tweet, with the entries: `id`, `keyword`, `location`, `text`, and `target`. The `target` entry is 0 or 1 depending on whether the tweet referred to a real disaster or not. The test data was essentially the same but omitted the `target` entry which was to be predicted.

Some examples of tweets (with empty `keyword` and `location` entries) with `target` = 1 are 

* "Forest fire near La Ronge Sask. Canada",
* "Our Deeds are the Reason of this #earthquake May ALLAH Forgive us all",
* "#RockyFire Update => California Hwy. 20 closed in both directions due to Lake County fire - #CAfire #wildfires",

and some with `target` = 0 are

* "this is ridiculous....",
* "Was in NYC last week!",
* "Crying out for more! Set me ablaze".

# approach and results:
My approach was to tune a BERT model to do the classification. Huggingface has a wonderful tutorial available at https://huggingface.co/docs/transformers/tasks/sequence_classification, which I adapted to this context.

I chose to use the 'bert-base-cased' model because it seemed possible that capital letters might make a difference in some contexts (e.g. 'that was FIRE' vs 'that was fire'). Since location and keyword data also seemed significant based on some exploratory analysis, I merged everything into a string containing the location and keyword data before the text of the tweet, which was then tokenized, etc. 

To make the kaggle training data play well with the tensorflow dataset construction methods took some slight adjustments, but after this was done the model did reasonably well on the task with very little tuning. Training for 3 epochs resulted in successful classification of 80.845% of the test set. The file that generated the model and the results is the `text_classification_kaggle.ipynb` file in this repository.

The resulting classification along with the rest of the test tweet data is in the `output_full.csv` file in this repository.

It would be worthwhile to experiment with using different models and leaving out keyword data since, in some cases keywords were deceptive. 
