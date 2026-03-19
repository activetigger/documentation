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

**1. Create a project → 2. Define your annotation scheme → 3. Annotate → 4. (Optional) Train a model → 5. Export your results**

**What you'll need before starting:**

- An access to Active Tigger account
- A web browser through which you can access ActiveTigger either on a server or by running it locally on your computer
- A tabular dataset (CSV, XLSX, or Parquet) where each row is a text unit to annotate. 

**That's it!**

## 1. Create a project

Go to the **New Project** screen and fill in:

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
    For our example with political/non-political headlines, let's import 8000 text elements in our training dataset (that does not mean we are going to annotate all of them - see here for how to determine how many elements to import).

## 2. Define your annotation scheme

Under the **Codebook** tab, we can go to the next step: defining our labels.

A coding scheme is the set of labels you'll use to annotate. One scheme is created by default.

Click **New label**, type your label name, and press **+**. Repeat for each label.

In our example, let's create two labels: "political" and "non-political".

> Consider writing a short codebook (Project → Codebook tab) explaining how to distinguish labels, especially if you work with collaborators.

## 3. Annotate

Next, let's start annotating!

Go to the **Tag** tab. The interface shows you one text at a time. Read it, click the appropriate label, and move on. ActiveTigger picks the next element automatically.

**Selection modes:**

- **Random** (recommended to start): picks elements at random.
- **Fixed:** follows the original order of your dataset.
- **Keyboard shortcuts:** press the number key corresponding to a label to annotate without clicking.

**You can also:**

- Add a comment to any annotation (useful for edge cases)
- Go back to re-annotate the previous element
- Skip an element to return to it later

!!! info "Active Learning"

    For our example, maybe we find that most headlines are not classifiable as "political". Going through the dataset in a random order, it takes us a lot of time to find examples of this category. This is where active learning can come in handy.
    
    In "active" mode, a model guesses what label you will apply to a given text, offering you the opportunity to correct it. This can help to speed up the annotation process if you are aiming to train a model that can automatically annotate your entire dataset.
    
    To enable Active Mode, you need to first train a Quick Model. Go to **Model → Create new quick model**.
    
    In the **Tag** tab, click on the little tiger face under **Active Mode**.
    
    In this mode, you can switch between the following text selection methods:
    
    - **Active:** prioritises texts the model is most uncertain about.
    - **Maxprob:** prioritises texts the model is most confident about.
    
    Try alternating between them and correct the model's preliminary guesses!


## 4. Train a model (optional)

If your goal is to extend your annotations to the full corpus automatically, you can train a BERT-based model directly in the interface.

A BERT-based classifier model uses your annotations to "learn" what kinds of texts should go in each category. Once trained, it can be applied on your data to apply your coding scheme automatically.

You should aim to have around a few hundred annotations with examples in each category (for our project, in both our "political" and "non-political" news headlines)

Go to **Model → Create new quick model**.

In the **Model** tab, you can also evaluate your model.

## 5. Export

Here, you can export your annotations, models, and the predictions made by the model on your data.

Once you are happy with your model, you can use it to predict labels on your entire dataset under **Export → Models → Prediction complete dataset**.

You can then export your predictions. Congratulations, you have a fully annotated dataset!


!!! info "Best practices"

    In practice, going through each of these steps requires iteration and careful thinking about your annotation strategy. In this documentation, you'll find more detailed information about each key feature of ActiveTigger as well as advice on best practices.


**You may also be curious about:**

- how to manage collaboration through adding multiple users to your project
- how to use topic models to get an overview of what your dataset is about
- how to use generative AI tools in ActiveTigger

## Get in touch

If you encounter a bug or have a suggestion, feel free to raise an issue on Github.

We also have an active Discord community used to signal troubleshooting, exchange ideas, and ask questions about ActiveTigger. Please reach out at css@ensae.fr.
