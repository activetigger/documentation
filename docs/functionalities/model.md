# Model Page

This section describes the Model page, containing the Training tab and the Evaluation tab, both displaying available models and their performance.

## Training

This section first describes the layout and the information found on the page, then the models available and their parameters.

![](../img/functionalities/bertopic.png) <!-- TODO : Change the file -->

The first section contains the trained models, either [Quick Model](#quickmodel) or [Bert Model](#bertmodel) and buttons to train new models. Each model can be deleted using the <a class="icon">![](../img/icons/delete.svg)</a> button.

### Quick Models

The Quick Models are classification models from [scikit-learn](http://scikit-learn.org/stable/supervised_learning.html) trained on pre-computed features ([what are features?](../theoretical-concepts/index.md#what-are-features)). They are quick to train and do not require GPUs. These models can be used for Active Learning ([what is Active Learning?](../theoretical-concepts/index.md#what-is-active-learning)) in the [Annotate page](./annotate.md).

When launching a model training, the model will be trained on the subset of the train set where labels exist. There must be at least 10 (?? XXX) annotated text inputs per label. Once trained, the model will predict the labels for the rest of the train set in order to be used in Active Learning (see [Annotation page](./annotate.md#active-mode))

Models available include: 

- [Logistic model](http://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) with L2 penalty: XXX. The parameters are: 
    - <a class="parameter">Cost</a>: XXX
- [Logistic model](http://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) with L1 penalty: XXX. The parameters are: 
    - <a class="parameter">Cost</a>: XXX
- [k-Nearest-Neighbors (KNN)](http://scikit-learn.org/stable/modules/generated/sklearn.neighbors.KNeighborsClassifier.html): XXX. The parameters are: 
    - <a class="parameter">Number of neighbors</a>: XXX
- [Random Forest](http://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html): XXX. The parameters are:
    - <a class="parameter">Number of estimators</a>:
    - <a class="parameter">Max features</a>:
- [Multinomial Naive Bayes classifier](http://scikit-learn.org/stable/modules/generated/sklearn.naive_bayes.MultinomialNB.html): XXX. The parameters are:
    - <a class="parameter">Alpha</a>
    - <a class="parameter">Fit prior</a>

!!! warning "All features are scaled before fitting the Quick Model"

On top of model-specific parameters, additional parameters can be set: 

- <a class="parameter">Name for the model</a>: The name used as a reference in the interface.
- <a class="parameter">Automatically balance classes</a>: If set to True, the model will be trained on a subset of the train set constructed by picking an equal number of text inputs accross labels. 
- <a class="parameter">10-fold cross validation</a>: Computes performance test using the [10-fold cross validation technique](http://scikit-learn.org/stable/modules/cross_validation.html).
- <a class="parameter">Labels to ignore</a>: Labels selected will be ignored. You need at least two labels to start training a model. Models with ignored labels are available for active tigger (see [Annotation page](./annotate.md#models-with-ignored-labels)). 

<!-- TODO: ADD the retraining process-->

### BERTmodel

The BERT Models are embedding models with a classification layer [trained with the huggingface framework](https://huggingface.co/docs/transformers/tasks/sequence_classification). They can take dozens of minutes to train and require GPUs[^1]. These models can be used for Active Learning ([what is Active Learning?](../theoretical-concepts/index.md#what-is-active-learning)) in the [Annotate page](./annotate.md).

[^1]: You can train on the CPU but that would be sub-optimal.

When launching a model training, the model will be trained on the subset of the train set where labels exist. There must be at least 10 (?? XXX) annotated text inputs per label. After training, the best model (accross epochs / checkpoints) will be used to predict the labels on the whole trainset to be used in Active Learning (see [Annotation page](./annotate.md#active-mode)).

The parameters for the model are: 

- <a class="parameter">Name for the model</a> The name used as a reference in the interface.
- <a class="parameter">Model base</a>: The pretrained model used for generating the embeddings. Models are loaded through the HuggingFace interface ([which models can I train?](../faq/faq.md#choose-models-made-available)). 
- <a class="parameter">Context window size</a>: The number of token per entry. After tokenization each input is truncated/padded to match this size. If selecting <a class="parameter">Auto adjust Max context window size</a> the window size will be calculated as the minimum between the maximum window size of the model and the length of the longest entry of the dataset.
- <a class="parameter">Epochs</a>: The number of times the model will be train on the train dataset[^2] ([more on choosing the hyperparameters](../theoretical-concepts/index.md#choose-hyper-parameters)). 
- <a class="parameter">Learning Rate</a>: The initial learning rate value used during training ([more on choosing the hyperparameters](../theoretical-concepts/index.md#choose-hyper-parameters)). 
- <a class="parameter">Weight Decay</a>: The probability for a weight to not be updated during the backward propagation ([more on choosing the hyperparameters](../theoretical-concepts/index.md#choose-hyper-parameters)).
- <a class="parameter secondary">Use GPU</a>: If set to True, the model will be trained on GPU.
- <a class="parameter secondary">Batch size</a>: The number of inputs provided to the model at once. Large batch size makes training faster but requires higher tier hardware.
- <a class="parameter secondary">Gradient Accumulation</a>: The number of batches used to update the weights during the backward propagation. @JULIEN
- <a class="parameter secondary">Eval</a>: This is the number of evaluation — scoring performance on the train-eval dataset — performed during the run.
- <a class="parameter secondary">Train-eval split size</a>: The ratio of elements in the train dataset[^2] that will be used to assess the model performance during training.
- <a class="parameter secondary">Class threshold</a>: The minimum number of annotation per label required. XXX sort out class or theshold
- <a class="parameter secondary">Balance classes</a>: If set to True, the train dataset[^2] will be constructed using the same number of text inputs per label.
- <a class="parameter secondary">Loss</a>: The loss function used optimise the model weights for training.
- <a class="parameter secondary">Keep the best model</a>: If set to True, the model .
- <a class="parameter secondary">Labels to ignore</a>: Text inputs with these labels will be dropped out of the train dataset[^2].

[^2]: Reminder: the train dataset is the subset of the train set where labels exist.


## Evaluation
