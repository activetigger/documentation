# Glossary

## What is a scheme ?

What? In the context of the app, what difference does it make? 


"Scheme" refers to one of the many faces of your project. Each scheme, references a set of **labels** as well as the annotations, a **codebook** and classifier models (Quick and BERT). All users with access to a project can see all the schemes. 

|Unique to a scheme|Common across schemes|
|---|---|
|- Labels and annotations<br/>- Codebook<br/>- Quick and BERT models|- Topic models<br/>- Features<br/>- Settings and dataset splits<br/>- Generative models' configuration<br/>- Visualization|

!!! example

    On a project studying interactions between users on Twitter, one scheme can investigate misinformation spread (with labels: "Conspiracy theory", "Fake News", "Factual News" and "Neither") whereas another scheme can investigate the nature of the interaction (with labels: "Respectful Debate", "Casual chatting" and "Offense").

### Available scheme types

Each scheme has a "type" corresponding to the kind of annotation performed: 

- "Multiclass": Users can choose **one** label to give to each text input.
- "Multilabel": Users can choose **several** labell to give to each text input.
- "Span": Users can highlight in the text one or more extracts, each highlight is given **one** label.

What you can and cannot do with each scheme type: 

||Multiclass|Multilabel|Span|
|---|---|---|---|
|Create labels and a codebook|🟢|🟢|🟢|
|Explore your corpus with a<br/> visualisation or topic models |🟢|🟢|🟢|
|Train a classifier (Quick or BERT)|🟢|🟠 (need to dichotomize labels)|🔴|
|Use generative models|🟢|🟢|🟢|
|Export annotations|🟢|🟢|🟢|
|Export models|🟢|🟠 (dichotomized models)|🔴|

## Train, Validation and Test sets

When creating a project, you can choose the size of thre datasets: 

- train : This split includes rows that will be seen by the model during training. This split can represent 70% of the whole dataset.
- validation : This split includes rows that will not be seen by the model during training, but is used to evaluate the model and choose the right hyperparameters. This split can represent 15% of the whole dataset.
- test : This split includes rows that will not be seen by the model during training nor during hyperparameter tuning. In practice we communicate on the model's performance on this test set to prevent from cherry picking hyperparameters. This split can represent 15% of the whole dataset.

!!! note
    If do not plan on training a model for inference, you can ignore them and place all your text inputs in the train set. 

## What is a projection?

A projection is a 2D visualisation of text inputs obtained by applying a dimension reduction algorithm on one or more set of features. Doing so can help visualising clusters in your corpus.

## What are features 

A set of features is a mathematical representation of a text input. One feature is one dimension of the set of features. Set of features can be calculated with different techniques: 

- sentence-embeddings: This set of features consists of embeddings generated with pretrained models as can be found on HuggingFace. One set of features can include up to 1500 features that have no direct interpretation. Taken as a whole, the set creates an embedding space where two semantically similar texts will live close to one another. 
- fasttext: similar to the sentence-embeddings, this set of features consists of embeddings pretrained on text corpora, however these sets of features do not adapt to the context of the text input as sentence-embeddings would. One set of features can include up to 500 features that have no direct interpretation. Taken as a whole, the set creates an embedding space where two semantically similar texts will live close to one another. 
- dfm (Discrete XXX Matrix): This set of features counts the number of occurences of words in a text input and applies transformations (TF-IDF, normalisation and or logarithm). A set of feature can include up to 50k features, where each feature represents a word in the vocabulary of all words in the corpus.
- Regex: This is a set of features consisting of only one column: whether or not the text input contains the regular expression (`1` if it does, `0` otherwise)
- dataset: If you have metadata in your dataset, they can be included as a set of features using this method. 

## What is Active Learning? 

XXX