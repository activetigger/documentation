# Quickstart for ActiveTigger

*ActiveTigger* is an open-source software designed to support collaborative text annotation for computational social sciences.

It offers access to no-code computational methods suitable for a variety of research projects as long as they involve text data in some form.

**ActiveTigger could help you if you…**

- want to classify large amounts of text data (social media posts, news articles...)
- are working collaboratively with other human annotators
- want to get an overview of key topics in your text data
- are curious about computational methods and want an easy introduction

This Quickstart guide offers an overview of what you need to get started with ActiveTigger. 

Many **use cases** are possible, as ActiveTigger offers several methodological options. To provide an example, we structure this guide around a common problem in social science research: *having more textual data than you could manually analyze*.

!!! tip "Example"
    Let's say you have a dataset of 10 000 newspaper headlines. You want to classify them into "political" and "non-political" categories. It would take you a very long time to classify this manually. By following the below five steps in ActiveTigger, you can 1) make the manual annotation process easier and 2) train a classifier model that can extend your coding scheme automatically on the entire dataset.

## Workflow at a glance

<div class="img"><img src="../../img/quickstart/steps.svg"/></div>

**What you'll need before starting:**

- A web browser through which you can access ActiveTigger either on a server or by running it locally on your computer (see [installation](../software/installation.md)).
- An Active Tigger account.
- A tabular dataset (CSV, XLSX, or Parquet) where each row is a text unit to annotate. 

**That's it!**

## 1. Create a project

Go to the [**New Project**](../functionalities/project-creation.md) screen and fill in:

- **Project name** — A unique name for your project
- **Load dataset from disk** — Upload your CSV, XLSX, or Parquet file, with each text element in a separate row
- **Id column** — Specify the unique identifier for each row. If there is no such column in your dataset, pick "Row number"
- **Text columns** — Specify the column that contains the text you wish to annotate
- **Language of the corpus** — Specify the language of your text data (used to select relevant models, but you can also work in languages not listed here)
- **Number of elements in the train set** — Specify how many elements you wish to import in the training dataset

**Optional:**

- **Context columns:** columns to display alongside the text while annotating (e.g. author, date, source). May be useful to understand what you are annotating, but this data is not used by the model.
- **Existing annotations:** if your file already has a label column (for example, if you have already completed some manual annotation), you can import it.
- **Test set:** a held-out sample used later to evaluate your model. Not required to get started.

!!! tip "Example"
    For our example with political/non-political headlines, let's import 8000 text elements in our training dataset (that does not mean we are going to annotate all of them - [FAQ - how many rows to import?](../faq/faq.md#how-large-should-my-different-sets-be)).

## 2. Define your annotation scheme

Under the [**Codebook** tab](../functionalities/codebook.md), we can go to the next step: defining our labels.

A coding scheme is the set of labels you'll use to annotate. One scheme is created by default.

Click **New label**, type your label name, and click <span class="icon">![](../img/icons/plus.svg)</span>. Repeat for each label.

In our example, we create two labels: "political" and "non-political".

Consider writing a short [codebook](../functionalities/codebook.md#guidelines) explaining how to distinguish labels, especially if you work with collaborators.

## 3. Annotate

Next, let's start annotating!

Go to the [**Tag** tab](../functionalities/annotate.md). The interface shows you one text at a time. Read it, click the appropriate label, and move on. ActiveTigger picks the next element automatically.

**Selection modes:**

- **Random** (recommended to start): picks elements at random.
- **Fixed:** follows the original order of your dataset.

**You can also:**

- Add a comment to any annotation (useful for edge cases)
- Go back to re-annotate previous elements
- Skip an element to return to it later

!!! info "Active Learning"

    For our example, maybe we find that most headlines are not classifiable as "political". Going through the dataset in a random order, it takes us a lot of time to find examples of this category. This is where active learning can come in handy.
    
    In "active" mode, a model guesses what label you will apply to a given text, offering you the opportunity to correct it. This can help to speed up the annotation process if you are aiming to train a model that can automatically annotate your entire dataset.
    
    To enable Active Mode, you need to first train a Quick Model. Go to [**Model → Create new quick model**](../functionalities/model.md#quick-models).
    
    In the **Tag** tab, click on the little tiger face under [**Active Mode**](../functionalities/annotate.md#active-learning-in-practice).
    
    When active learning is on, it unlocks new strategies to pick the next element. [Read more](../functionalities/annotate.md#selecting-text-inputs-to-annotate).

    Read more about [Active Learning](../theoretical-concepts/index.md#what-is-active-learning).


## 4. Train a model

If your goal is to extend your annotations to the full corpus automatically, you can train a BERT-based model directly in the interface.

A BERT-based classifier model uses your annotations to "learn" what kinds of texts should go in each category. Once trained, the model can be used to infere the labels of unannotated text inputs. 

Go to **Model → Create new quick model**.

In the **Model** tab, you can also evaluate your model.

See [Model page](../functionalities/model.md#bertmodel) for more information on the parameters, the [Theoretical concepts page](../theoretical-concepts/index.md#training-bert-models) for guidelines on how to correctly train and model and the [FAQ page](../faq/faq.md#how-many-annotations-do-i-need) for additionnal pieces of advice.

## 5. Export

Lastly, export your annotations, models and predicitons to carry on the analysis. See [Export page](../functionalities/export.md) for more information.

!!! info "Best practices"

    In practice, going through each of these steps requires iteration and careful thinking about your annotation strategy. In this documentation, you'll find more detailed information about each key feature of ActiveTigger as well as advice on best practices.


**You may also be curious about:**

- how to manage collaboration through [adding multiple users](../functionalities/monitoring-account-and-users.md) to your project and [compare your annotations](../functionalities/annotate.md#curate)
- how to use [topic models](../functionalities/explore.md#topic-model) to get an overview of what your dataset is about
- how to use [generative AI tools in ActiveTigger](../functionalities/generative.md)

## Get in touch

If you encounter a bug or have a suggestion, feel free to raise an [issue on Github](https://github.com/activetigger/activetigger/issues).

We also have an active [Discord community](https://discord.gg/3uNnjw2k) used to signal troubleshooting, exchange ideas, and ask questions about ActiveTigger. 

For any other inquiry, please reach out at css@ensae.fr.
