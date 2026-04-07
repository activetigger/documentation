# Glossary

<!-- 
AM: same
## Roles

**TODO** -->

<!-- 
AM: belongs to the functionalities 
## DFM options

**TODO**
 -->

## Projects

Active Tigger is organized around projects. Each project consists of a dataset, a set of schemes, and additional assets such as features or topic models. A project can be shared across users for collaborating.

The dataset is a table that contains the texts that you want to work on, and optionally some other columns that will help you in the process. It can be very large, in which case you will work on smaller subsets (see the [Train, Validation and Test sets](./index.md#train-validation-and-test-sets)).

See [Project Creation page](../functionalities/project-creation.md)

## Schemes

In Active Tigger, each project is organized into one or several schemes. In short, it gathers the data you want to analyze, the corresponding annotations, and models for to assist your exploration and annotation. In practice, it is a set of **labels** as well as the annotations, a **codebook** and classifier models (Quick or BERT).

Users with access to a project can see all the schemes. 

!!! Example

    A project contains corpus of speeches, and seeks to identify what topics are mentioned as well as the tone used. Users can create different schemes to separately work on identifying speeches mentionning the environment, another for social inequalities and finally one more to identify agressive tones.

There are different types of schemes in Active Tigger: 

- <span class="highlight">Multiclass</span>: each text will be given a single label.
- <span class="highlight">Multilabel</span>: each text can be given several labels simultaneously.
- <span class="highlight">Span</span>: give a label to one or more portions of the text (spans).

What you can and cannot do with each scheme type: 

||Multiclass|Multilabel|Span|
|---|---|---|---|
|Create labels and a codebook|🟢|🟢|🟢|
|Explore your corpus with a<br/> visualisation or topic models |🟢|🟢|🟢|
|Train a classifier (Quick or BERT)|🟢|🟢|🔴|
|Use generative models|🟢|🟢|🟢|
|Export annotations|🟢|🟢|🟢|
|Export models|🟢|🟢|🔴|

!!! tip

    Multiclass schemes can be imported from your dataset upon project creation.


## Model quality scores

Quality scores provide valuable insights on predictive models performance.

### Evaluating Multiclass models

Active Tigger displays 3 scores per class as well as score weighted across all classes. Each score is bounded between 0 and 1 (the higher the better).

|Measure|Data|Interpretation|
|---|---|---|
|[Precision](https://en.wikipedia.org/wiki/Precision_and_recall)|Per class|How confident you can be about the positive predictions of each class|
|[Recall](https://en.wikipedia.org/wiki/Precision_and_recall)|Per class|Portion of the actual positive cases that are found by the model|
|[F1](https://en.wikipedia.org/wiki/Precision_and_recall#F-measure)|Per class|Overall quality of the model's predictions for each class|
|[Macro F1](https://en.wikipedia.org/wiki/F-score#Macro_F1)|Overall|Overall quality of the model on all classes|

!!! Note
    Each score is computed separately for the train set, the validation and test sets.


## Dataset stratification 

A corpus might come from different sources, or different time periods, that you might want to treat equally in an annotation workflow.
Stratifying the dataset prevents from working on unbalanced datasets. This is a common challenge in machine learning: training on non-representative samples leads to models failing on minority subsets. 

!!! Example
    If working on newspaper articles with 80% of all articles coming from LeMonde and only 20% coming from LePoint, training a model will most likely adapt to LeMonde's writing but not LePoint's. The source becomes a descriptor for your annotation whereas it shouldn't.

Stratification is performed upon [project creation](../functionalities/project-creation.md).


## Tokens and window sizes

Large language models (including sentence embedding models) do not use plain texts to process data, but first decompose them into tokens in order to make them easier to handle. Tokens are either whole words or parts of words: very common words in a given language will typically have their own token, as well as common radicals and prefixes and suffixes. *For instance, in English, "iterat-", "-e", "re-", "-s", "-ing", or "-ion" are parts that have similar meanings across words, which is why it is more efficient to decompose "iterate", "iterates", "reiterate", "iterating", "iteration", etc. into tokens than to represent them as altogether separate terms.*
Each unique symbol has its own token, so that any given word (including typos) can be read by the model.

Each language model uses its own tokenizer (the algorithm that transforms raw text into tokens).

One important feature of each language model is that it has a <span class="highlight">maximum window size</span>: the number of tokens it is able to process for any given text.
Therefore, it is important to be aware of the language model's specific window size, as tokens beyond this limit will be ignored.[^1]

[^1]: To assist you in the annotation process, the [Annotation tab](../functionalities/annotate.md#annotate-page) approximates the number of tokens per text input and displays excess tokens in italic. You can modify the limit in the **config menu** button. 

In order to check the tokenizers of different models, you can use sites such as [LLM Calculator](https://llm-calculator.com/), [LLM Token Counter](https://llmtokencounter.com/), [Token Calculator](https://token-calculator.net/), etc. Most of them are made for generative LLMs, but can still give you a rough estimation of how your corpus will be treated.

**TODO link to relevant python module**

