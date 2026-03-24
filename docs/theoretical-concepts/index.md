# General concepts in Active Tigger

## Train, Validation and Test sets

In supervised machine learning (aka predictive models), it is common practice to split your dataset into [three subsets](https://en.wikipedia.org/wiki/Training%2C_validation%2C_and_test_sets): the training, validation, and test sets. The reason for this is to control [overfitting](https://en.wikipedia.org/wiki/Overfitting), which happens when a predictive model performs well on its training set, but fails to generalize to new inputs.

Each set plays a different role: 

- <span class="highlight">train set</span>: this set that will be used to train models[^1].
- <span class="highlight">validation set</span>: this set used to compare model performances across hyperparameters. 
- <span class="highlight">test set</span>: this set is used to evaluate the generalization quality of your final model. Do not use this choose models, otherwise your evaluation scores will not be valid (see [Goodhart's law](https://en.wikipedia.org/wiki/Goodhart's_law)). 

[^1]: Note that this set is itself split into a main training (80%) and a train-eval subset (20%). The train-eval subset is used to evaluate the model's generalization capabilities during training. The combination of the train subset and the train-eval subset makes choosing hyperparameters easier. See [Reading the loss curve](#reading-the-loss-curve)

In Active Tigger, we enforce some "good practice" measures:

- Splitting is performed before annotating so that the choice of validation and test sets is not influenced by choices made during annotation of the training set.
- Model predictions and active learning features are not available when annotating the validation and test sets, to prevent the annotator from being influenced by model predictions.
- By default splitting is performed using uniform random sampling upon [project creation](../functionalities/project-creation.md). [Additional options exist](../functionalities/project-creation.md#secondary-parameters) to control the sampling process such as [Stratification](./glossary.md#dataset-stratification).

!!! Note
    
    The dataset is split upon [project creation](../functionalities/project-creation.md). Sets can be modified in the [Settings](../functionalities/settings.md). Validation and Test sets are optional, but they are strongly recommended if your goal is to train predictive models.

## Representing texts with Features

When using machine learning in text analysis settings, the first step is always to transform each text input into arrays, alias <span class="highlight">a set of Features</span>[^2].

[^2]: In Active Tigger, we chose to name an array of numbers *a set of features*, where each column is a *feature*.

A set of features can be used to compute visualizations, fit topic models or quick models. Note that they are not required for BERT models (or generative LLMs), as they automatically compute their own features internally.

<!-- **ATTENTION POUR L'INSTANT C'EST SEULEMENT EMBEDDINGS** What do you mean? XXX -->
In Active Tigger, there are five kinds of features, which can be created in the Settings tab:

- <span class="highlight">Sentence embeddings</span>: Computed with transformer models, this method is the most advanced method for representing each text input [^3] as an array. As for all transformer model, each model has a [maximum window size](./glossary.md#tokens-and-window-sizes).
- <span class="highlight">FastText</span>: Each text input is split into words (using the [SpaCy](https://spacy.io/) tokenizer), each word is represented with a pre-computed embedding; the text input is represented as the average of all word embeddings. This method does not care for the order of the words. See the [fastText](https://fasttext.cc) webpage for details.
- <span class="highlight">DFM</span> (document-feature matrix): Each text is split into words (using the [SpaCy](https://spacy.io/) tokenizer), a large matrix is calculated: for a given row (=document) and column (= word), the coefficient represents the number of time the word appeared in the document. These matrices are usually transformed using various methods, see [Settings page](../functionalities/settings.md#features). This method is used in many pipelines designed before the invention of sentence transformers.
- <span class="highlight">Regex</span> (regular expression):  For a given regex, the feature is a single binary variable, reporting if the regex was found in the text input.
- <span class="highlight">dataset</span>: Import a column of your dataset as a feature. This can be useful when training quick models, for instance if you have a variable that measures the number of characters, or the text's source.

[^3]: Not necessarily a sentence, a text input can be a whole paragraph.

## What is Active Learning ?

<span class="highlight">Active learning</span> is a method to increase annotations efficiency, it lowers the number of annotations necessary to train performant models. 

The key idea: Instead of picking text inputs at random, the algorithm provides text inputs that are ambiguous and therefore, will likely be the most helpful when training a [BERT model](#what-are-bert-models). This method challenges the definition of each label forcing annotators to refine the codebook. In practice, a [quickmodel](#training-quick-models) is fitted on existing annotations and then used to predict the annotations for future text inputs. With the annotation, the model provides its confidence, i.e. the entropy of the predicted probabilities (higher entropy means low confidence). In the [Annotation tab](../functionalities/annotate.md#annotate-page), the app will order text elements with decreasing entropy for annotation. Read more about how to use active learning in the [Annotation page](../functionalities/annotate.md#active-learning)  


## Training Quick models

Quick models are standard supervised machine learning models, trained on features in order to predict labels. 
Compared to BERT models, they are lightweight and quick to train, hence their name. 
They are typically used in the early stages of annotation, as described in the workflow above. 

## Training BERT models

### What are BERT models?

(BERT models)[https://en.wikipedia.org/wiki/BERT_(language_model)] are powerful predictive models that you can use in order to generalize your annotations to a larger corpus (either your project's dataset, or an external one, see [Export page](../functionalities/export.md)).
They are pre-trained encoder language models[^4], meaning that they have been trained on very large corpora in order to encapsulate semantic "understanding". These models must be fine-tuned to adapt to any task.

[^4]: As opposed to decoder models i.e. generative models, encoder models' only goal is to create an embedding space that encapsulates the semantic of words.

Fine-tuning a BERT model is the process of adjusting its internal weights using optimization algorithms[^5] to maximize [quality scores](./glossary.md#model-quality-scores). [Learn more about fine-tuning models](https://youtu.be/IHZwWFHWa-w?si=WOzTeU4U6b62uq_s). This is a delicate art requiring trials and errors to find the best hyperparameters. Learn more about this process through the [loss curves](#reading-the-loss-curve).

[^5]:  Like [gradient descent](https://en.wikipedia.org/wiki/Gradient_descent), although nowadays we tend to use AdamW, an algorithm derived from gradient descent.

### Which model to choose?

<!-- should it live in the FAQ? -->

There are many different pre-trained models to choose from, hosted on the (Huggingface)[https://huggingface.co/] website.
The main difference between them is the corpus they have been pre-trained on (most of them are specialized in a single language), and their inner architecture (which among others determines the [window size](glossary.md#tokens-and-window-sizes)).
There is no golden rule for which model to choose: try different ones, and see which one works best on your data.

### Reading the loss curve

The loss curve provides key insights on how efficient the training was. It represents the evaluation of the [loss function](https://en.wikipedia.org/wiki/Loss_function) on the train and the eval-train set across training steps/epochs.

Here are some general rules for obtaining a good model while avoiding [overfitting](https://en.wikipedia.org/wiki/Overfitting). Refer to [quality scores](./glossary.md#model-quality-scores) for more insightful metrics on the model's performance.


#### Just right

![](../img/theoretical-concepts/bertrain-good.png)

This is what you want to see:

- Both curves went down during training: the model has learned
- Both curves have the same loss values: no overfitting
- The curves are flat at the end: nothing more to be learned, apparently

Now you only have to look at the evaluation metrics to see if you are satisfied with the prediction quality.


#### Overfitting

![](../img/theoretical-concepts/bertrain-overfit.png)

The model has overfitted:

- Both curves went down during training: the model has learned
- But the training curve is much lower than the evaluation curve

What to do:

- choose a lower learning rate, for slower weight updates
- use larger batches[^6], in order to smooth training over more examples per training step
- choose higher weight decay: this will prevent the weights from getting to large
- annotate more data, you may not have enough examples for the model to learn from

[^6]: The effective batch size is the system batch size times the gradient accumulation.

#### Underfitting

![](../img/theoretical-concepts/bertrain-flat.png)

The model has underfitted:
- Both curves are flat, the model learned nothing

What to do:

- choose a higher learning rates, for faster weight updates
- use smaller batches, as this will result in more training steps
- choose lower weight decay: too high regularization can prevent proper learning
- annotate more data, you may not have enough examples for the model to learn from


#### Incomplete learning

![](../img/theoretical-concepts/bertrain-more.png)

The model could learn more:

- Both curves went down during training: the model has learned
- Both curves have the same loss values: no overfitting
- But there is no plateau at the end, the curves are still going down

What to do:

- use more epochs, to give the model time to learn more
- choose a higher learning rate, for faster weight updates
- use smaller batches, as this will result in more training steps
- choose lower weight decay: too high regularization can prevent proper learning


#### Chaotic learning

![](../img/theoretical-concepts/bertrain-chaos.png)

The model is trying to learn too fast:

- Curves should be going down, not up and down
- Some learning has occured, but you can probably do better

What to do:

- choose a lower learning rate, for slower weight updates
- use larger batches, in order to smooth training over more examples per training step
- choose higher weight decay: this will prevent the weights from getting to large
- annotate more data, you may not have enough examples for the model to learn from


### Which hyper-parameters to choose?

<!-- AM: it is unclear if it is pedagogical material (in which case, this table is coherent) or descriptive material, (in which case it should live in the functionalities section) -->

**Base parameters**

|Name|Type|Description|Typical value|
|---|---|---|---|
|Model base|General|Which pre-trained model will be fine-tuned.<br>Larger models need more training data.||
|Max context window|General|The number of *tokens* that will be used during training for each text. <br> Lower values make training faster and use less memory.||
|Epochs|General|The number of times your training data will be presented to the model|3|
|Learning rate|General / Regularization|How much the model's weights will be changed at each step|5e-6 to 5e-4|
|Weight decay|Regularization|Prevents model weights to become too high|0.01|

**Advanced parameters**

|Name|Type|Description|Typical value|
|---|---|---|---|
|Total batch size|General / Regularization|How many training examples are presented at each step.<br>Total batch size = Batch size x Gradient accumulation.|16 or 32 (16)|
|Batch size|General / Regularization|Number of examples that are loaded in memory at any one time.|1-32 (4)|
|Gradient accumulation|General / Regularization|Number of batches accumulated to perform a gradient descent step.<br>Use higher values for small GPUs.|1-32 (4)|
|Eval|General|Number of times the model will be evaluated on the evaluation set during training (aka checkpoints).|9|
|Train-eval split size|General|Portion of the data that will be used for evaluation during training.|0.2|
|Balance classes|General|Whether to use only the number of observations of the smallest class during training.|Deactivated|
|Loss|General|Which loss function is optimized: use Weighted cross entropy for unbalanced class|Cross entropy|
|Keep the best model|General|Whether to keep the best checkpoint according to evaluation loss,<br>instead of the final checkpoint.|Activated|
|Class threshold|Data|Minimum number of observations for a class to be used during training.<br>Use higher values to exclude small classes.|1|
|Labels to ignore|Data|Which classes to ignore during training|None|


## Projections

A projection is a 2D (dimensional reduction)[https://en.wikipedia.org/wiki/Dimensionality_reduction] of your training data, used for visualization (in the **Explore** panel).

It uses an unsupervised model in order to reduce high-dimensional [set of features](#representing-texts-with-features) to two dimensions: similar texts will be grouped together.

The resulting visualization will help detecting outliers, and will group texts according to general themes. <!-- yes, but also, no...-->

In classification workflows, it is recommended to use projections to get a first overview of your corpus, and to determine whether you need to perform some more cleaning and filtering before annotating texts and training models.

Note that the placement of texts in the visualization does not tell you everything you want to know about your corpus.

This reflects the difference between unsupervised and supervised learning: unsupervised learning is only based on features, while supervised learning is meant to find the relationship between features and labels.

In many cases, different annotations will appear close together in the projection: this means that your classification scheme goes beyond topic modeling.

**TODO: details and links (in Glossary?)**


## Topic models

A topic model (in the **Explore** panel) is an unsupervised model meant to capture the main themes that are present in a corpus, based on text *features*.

Active Tigger features BERTopic models, which work in two successive steps: first a dimensionality reduction step (as in *Projection*, see above), then a clustering step.

Topic modeling can either be an end in itself, or a useful step in a annotation/prediction workflow. 

If your goal is to find the main topics in your corpus, you can use topic modeling as a first approximation, and then **Convert to scheme** in order to refine this using additional annotations and modeling.

**TODO: details and links (in Glossary?)**


