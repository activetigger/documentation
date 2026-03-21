# Glossary


## Roles

**TODO**


## DFM options

**TODO**


## Projects

Active Tigger is organized around projects, which are essentially the combination of a dataset and a set of schemes. 

The dataset is a table that contains the texts that you want to work on, and optionally some other columns that will help you in the process. 
It can be very large, in which case you will work on smaller subsets (see the *Train, Validation and Test sets* section on the *Theoretical concepts* page).


## Schemes

In Active Tigger, each project is organized into one or several schemes. 
What do we call schemes? Simply what you are trying to analyze, annotate or predict. 
In practice, it is a set of **labels** as well as the annotations, a **codebook** and classifier models (Quick or BERT).
All users with access to a project can see all the schemes. 

For instance, if your project contains a corpus of speeches, there might be different things you are looking for: whether the speeches mention a given topic, whether they use a certain tone, whether they adopt a certain stance... 
Each of these things will be a different scheme. 

There are different types of schemes in Active Tigger: 
- multiclass: each text will be given a single label
- multilabel: each text can be given several labels simultaneously
- span: instead of tagging a complete text, you select one or several portions of the text to label

What you can and cannot do with each scheme type: 

||Multiclass|Multilabel|Span|
|---|---|---|---|
|Create labels and a codebook|🟢|🟢|🟢|
|Explore your corpus with a<br/> visualisation or topic models |🟢|🟢|🟢|
|Train a classifier (Quick or BERT)|🟢|🟠 (need to dichotomize labels)|🔴|
|Use generative models|🟢|🟢|🟢|
|Export annotations|🟢|🟢|🟢|
|Export models|🟢|🟠 (dichotomized models)|🔴|

Note that existing columns in your dataset can be imported as schemes, at project creation (multiclass only). 
This can be useful if you already have some annotations for a given scheme, or even if your whole corpus is already annotated and you want to use Active Tigger just for visualization or for training predictive models.


## Model quality scores

When training a predictive model, it is essential to know how good they are performing.
That is what the quality scores are for.

In Active Tigger, each predictive (multiclass) model has 3 different scores *for each class*, and one global score, all bounded between 0 and 1 (higher is better).

|Measure|Data|Formula|Interpretation|
|---|---|---|---|
|Precision|Per class|(number of correct positive predictions) / (number of positive predictions)|How confident you can be about the positive predictions of each class|
|Recall|Per class|(number of correct positive predictions) / (number of positive cases in the actual annotations)|Portion of the actual positive cases that are found by the model|
|F1|Per class|2 x (Precision x Recall) / (Precision + Recall)|Harmonic mean of Precision and Recall: overall quality of the model's predictions for each class|
|Macro F1|Overall|Average of the per-class F1 scores|Overall quality of the model on all classes|

For more details, see [Wikipedia page](https://en.wikipedia.org/wiki/F-score).

Note that each of these scores are separately computed for the training-evaluation set (in the Training tab), and the validation and test sets (in the Evaluation tab).
See the Theoretical concepts section for more information about these three datasets.


## Dataset stratification 

A corpus might come from different sources, or different time periods, that you might want to treat equally in an annotation workflow.
If not, you are running the risk of training models that are more adapted to majority than minority sources.
This is where stratification comes in: making sure that each source is equally represented in the training, validation and test sets.

Stratification is done at Project creation: choose the variables you want to stratify on, and the subsets will contain an equal number of cases for each source.


## Tokens and window sizes

Large language models (including sentence embedding models) do not use plain texts to process data, but first decompose them into tokens in order to make them easier to handle.
Tokens are either whole words or parts of words: very common words in a given language will typically have their own token, as well as common radicals and prefixes and suffixes.
For instance, in English, "iterat-", "-e", "re-", "-s", "-ing", or "-ion" are parts that have similar meanings across words, which is why it is more efficient to decompose "iterate", "iterates", "reiterate", "iterating", "iteration", etc. into tokens than to represent them as altogether separate terms.
Each individual symbol will also have its own token, so that any given word (including typos) can be read by the model.

Each language model uses its own tokenizer (the algorithm that transforms raw text into tokens), and this is done transparently: you don't have to choose it yourself, it is done automatically.

One important feature of each language model is that it has a maximum window size: the number of tokens it is able to process for any given text.
Therefore, it is important to check each language model you are using for its specific window size, as tokens beyond this limit will be ignored by the model.
In the annotation tab, tokens exceeding a given limit are displayed in italic font.
You can modify this displayed window size using the **config menu** button. 

In order to check the tokenizers of different models, you can use sites such as ()[https://llm-calculator.com/], ()[https://llmtokencounter.com/], ()[https://token-calculator.net/], etc. 
Most of them are made for generative LLMs, but can still give you a rough estimation of how your corpus will be treated.

**TODO link to relevant python module**

