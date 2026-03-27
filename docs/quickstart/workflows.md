# Workflows

This page presents possible ways of using Tigger for your research and how to do it.

## Annotate a corpus collaboratively

Active Tigger's makes collaborative annotation seamless through the following features:

- Creation of a scheme ([what is a scheme?](../theoretical-concepts/glossary.md#schemes)) and a codebook for the project.
- Annotation of the text inputs by each user.
- Comparison of annotations and measure agreement
- Export the annotated corpus for analysis

Why choose Active Tigger for this task: 

- User friendly interface, on any device.
- Seamless integration of collaborative work.
- Safe storage of data.

Here is an overview of the steps necessary to set up and undertake an annotation project with manual annotation:

- <span class="step">Step 0 — Prepare your corpus:</span> Prepare your corpus as a CSV, XLSX or parquet file. [More information here](../functionalities/project-creation.md#note-on-preparing-your-input-dataset)
- <span class="step">Step 1 — Create your project:</span> On the [Project Creation page](../functionalities/project-creation.md), give the project a name, upload the data file and enter the columns you require for the annotation (ID, text, contextual). Set the number of rows in the train set to the size of your dataset. You may consider setting [secondary parameters](../functionalities/project-creation.md#secondary-parameters).
- <span class="step">Step 2 — Give your collaborators access to your project:</span> Go to the [Users page](../functionalities/monitoring-account-and-users.md) and authorize your collaborators to access and annotate text inputs from your project.
- <span class="step">Step 3 — Create your scheme and write down your codebook:</span> On the [Codebook page](../functionalities/codebook.md), create a scheme that fits your study (multiclass, multilabel or span — [more info on the available schemes](../theoretical-concepts/glossary.md#schemes)) and start writing the instructions for labelling the corpus. All users can see the schemes, labels and codebook of your project, but only managers and contributors can edit them.
- <span class="step">Step 4 — Start annotating your corpus:</span> Go to the [Annotate page](../functionalities/annotate.md) and start the annotation process. You can:
    - Add a label (<span class="action primary">LABEL</span>), remove a label (<span class="action primary">No tag</span>), or move forward (<span class="action primary">Skip</span>).
    - Add a comment to your annotation.
    - Choose which text inputs to annotate or the order in which you wish to see them ([more info](../functionalities/annotate.md#selecting-text-inputs-to-annotate)).
- <span class="step">Step 5 — Curate the annotation (Only available to projects with more than one user):</span> On the [Annotate page](../functionalities/annotate.md), choose ["Curate"](../functionalities/annotate.md#curate). You will be able to see annotations differences between schemes or between users and choose which annotation to keep (as well as agreement metrics).
- <span class="step">Step 6 — Export your annotated corpus:</span> On the [Export page](../functionalities/export.md), choose ["Annotations"](../functionalities/export.md#annotations) and <span class="action primary">All annotations/schemes</span> to download your corpus as a CSV file, or XLSX or parquet.

In practice, the annotation process is not so linear. It is normal to move back and forth between <span class="step">step 3</span>, <span class="step">step 4</span> and <span class="step">step 5</span> to refine your codebook and change your annotation strategy. You may also want to use exploration tools ([see below](#explore-your-data)), or use machine learning to find the most challenging text inputs and test your codebook on rare or ambiguous cases.

## Accelerate annotation with Active learning

Active Tigger makes machine learning methods easily available to social scientists, in particular by implementing the full pipeline for finetuning *classifier models* ([what are BERT models?](../theoretical-concepts/index.md#what-are-bert-models); [How to finetune BERT models?](../theoretical-concepts/index.md#training-bert-models) ). These models can automatically extend your human-developed annotation scheme on a larger dataset. This workflow consists of: 

- Creation of a scheme ([what is a scheme?](../theoretical-concepts/glossary.md#schemes)) and a codebook for the project.
- Annotation of the text inputs.
- Training classifier models.
- Infer labels on non-annotated data.
- Export human and infered annotations corpus for analysis

Why choose Active Tigger for this task: 

- User friendly interface and model training without any coding skills required.
- Safer and reproducible use of machine learning tool for annotating a corpus.
- An easy introduction to good practices in machine learning.

Here is an overview of the steps to complete this workflow:

- <span class="step">Step 0 — Prepare your corpus:</span> Prepare your corpus as a CSV, XLSX or parquet file. [More information here](../functionalities/project-creation.md#note-on-preparing-your-input-dataset)
- <span class="step">Step 1 — Create your project:</span> On the [Project Creation page](../functionalities/project-creation.md), give the project a name, upload the data file and enter the columns you require for the annotation (ID, text, contextual). Set the number of rows in the train set to about 70% of your dataset, 15% to the test set and 15% to the validation set ([more info](../faq/faq.md#how-large-should-my-different-sets-be)). You may consider setting [secondary parameters](../functionalities/project-creation.md#secondary-parameters).
- <span class="step">Step 2 — Create your scheme and write down your codebook:</span> On the [Codebook page](../functionalities/codebook.md), create a scheme that fits your study (for now, only multiclass schemes can be used for training classifier models — [more info on the available schemes](../theoretical-concepts/glossary.md#schemes)) and start writing the instructions for labelling the corpus.
- <span class="step">Step 3 — Start annotating your corpus:</span> Go to the [Annotate page](../functionalities/annotate.md) and start the annotation process. You can:
    - Annotate text inputs (add, remove or skip) and leave comments
    - Choose which text inputs to annotate or the order in which you wish to see them ([more info](../functionalities/annotate.md#selecting-text-inputs-to-annotate)).
    - Use <span class="highlight">Active Learning</span> to primarly annotate text inputs that will lead to better classifiers, more quickly ([more info](../theoretical-concepts/index.md#what-is-active-learning)).
- <span class="step">Step 4 — Train a BERT model</span> On the [Model page](../functionalities/model.md) and in the [Training tab](../functionalities/model.md#training), <span class="action primary">Create new BERT model</span> and [set hyperparameters](../functionalities/model.md#bertmodel) ([more info on setting hyperparameters](../theoretical-concepts/index.md#training-bert-models))
- <span class="step">Step 5 — Evaluate the model on validation set:</span> On the [Model page](../functionalities/model.md) and in the [Evaluation tab](../functionalities/model.md#evaluation), select your model and <span class="action primary">Compute predictions</span> to classify text inputs from the validation and test set to compute metrics on these sets.
    - Once you have annotated your training set, you will probably have a better understanding of your data, and stabilized the definitions of your labels.
    - You can now annotate your validation set, and check whether your model performs as well as on the training set.
    - Again, iterate between annotation and validation quality, until you are satisfied with the quality scores.
    - If you have trained several models, choose the model maximizing the [quality scores](../theoretical-concepts/glossary.md#model-quality-scores) on the validation set.
- <span class="step">Step 6 — Annotate the test set </span> this is the final step, which should only be used to evaluate the quality of your final model ⚠️ Optimising the quality scores on the test set will lead to biased performance estimators!

- <span class="step">Step 7 — Export your annotated corpus and model:</span> On the [Export page](../functionalities/export.md) and ["Models tab"](../functionalities/export.md#models), select the bert model:
    - <span class="action primary">Prediction on complete dataset</span> infer labels on the full dataset as imported upon project creation.
    - <span class="action primary">Prediction on external dataset</span> to import a dataset and infer the labels.
    - <span class="action secondary">Export fine-tuned model (large file)</span> download the weights of the fine-tuned model (good practice for reproducibility).

Once again, this workflow tends to be much less linear in practice. You will likely move back and forth between <span class="step">step 3</span> and <span class="step">step 4</span> to accumulate enough annotations to develop a model that works as well as you want it to, as well as between <span class="step">step 4</span> and <span class="step">step 5</span> to [refine your hyperparameters](../theoretical-concepts/index.md#training-bert-models). This workflow is compatible with the collaborative annotation workflow as well as the exploration workflow.


## Explore your data

Sometimes, with a large textual dataset, it is difficult to get an overview of what your dataset contains. Active Tigger provides tools to explore your corpus (either as an independent step or as part of an annotation process), helping you understand its structure, identify clusters of similar content, and make more informed annotation decisions. You can use of the tabular oversight functionality of the interface, or make use of  [topic models](../theoretical-concepts/index.md#topic-models).

This workflow consists of:

- Browsing and filtering your data in a tabular view.
- Computing a topic model to map thematic structures in your corpus.
- Using topics to guide annotation or as a starting point for a scheme.
- Exporting topic outputs for further analysis.

Why choose Active Tigger for this task:

- No-code access to state-of-the-art topic modelling (BERTopic).
- Visual, interactive exploration of your corpus.
- A seamless bridge between exploration and annotation.

Here is an overview of the steps to explore your data with BERTopic:

- <span class="step">Step 0 — Prepare your corpus:</span> Prepare your corpus as a CSV, XLSX or parquet file. [More information here](../functionalities/project-creation.md#note-on-preparing-your-input-dataset)
- <span class="step">Step 1 — Create your project:</span> On the [Project Creation page](../functionalities/project-creation.md), give the project a name, upload your data file and enter the columns you require (ID, text, contextual). You may consider setting [secondary parameters](../functionalities/project-creation.md#secondary-parameters).
- <span class="step">Step 2 — Browse your data (optional):</span> On the [Explore page](../functionalities/explore.md), open the [Tabular View tab](../functionalities/explore.md#tabular-view) to filter and browse your corpus. You can filter by dataset (train, valid, test), by label, or by regex query. Click on any ID to go directly to the [Annotate page](../functionalities/annotate.md) for that text input.
- <span class="step">Step 3 — Compute a BERTopic model:</span> On the [Explore page](../functionalities/explore.md), go to the [Topic model tab](../functionalities/explore.md#topic-model) and click <span class="action primary">Compute new BERTopic</span>.
- <span class="step">Step 4 — Explore the topic model results:</span> Once computed, the [Topic model tab](../functionalities/explore.md#topic-model) displays:
    - A **visual map** of your corpus with each text input coloured by topic.
    - A **topic table** summarising each topic's ID, size, name, representative keywords, and representative documents.
    - export the results in different ways. See [here](../functionalities/explore.md#topic-model)

Using topic models for exploring your dataset can also be integrated into the above workflow pipelines. We recommend complementing a topic model approach with familiarizing yourself with your corpus by simply reading it, or through an annotation process. Confiding too much in an automated synthesis of your text data could risk missing important aspects of your corpus.



### Finding all the positive cases

If your dataset is relatively small (a few thousand texts), and your goal is to annotate all the positive cases of the classes you are interested in, you might not need to follow the complete workflow described below. 

However, active learning could still be very helpful: just follow step 1 of the following section, and iterate until you are confident you have found all the positive cases in your dataset.

The only difference: use the complete dataset as your training set.

