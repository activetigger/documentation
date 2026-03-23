# FAQ

## How can I recover my password ?

For the moment, the only solution is to contact the administrator of your service to reinitialize it for you.

## Can I launch processes if the GPU is already full ?

You need to wait for enough GPU memory to be able to launch your process. There is no queue system for the moment. You can try to decrease the batch size to lower the required memory.

## If I destroyed my project, is it possible to recover the data ?

No.

## I have bugs or repetitive problems

Please open a issue on the Github.

## I have just created a project but want to modify certain parameters (e.g., increase the trainset size).

Go to the project tab, navigate to Settings, and select Update Project. Please note that if you increase the size of your project, you then need to create a new feature in the Prepare tab. 

## Trouble shoot with parquet files

If you upload a parquet file, you can encounter issues related to the format of your parquet file. Easy fix includes: 

- Make sure that data contained is formatted as a string.
- Make sure to not have nested columns (columns and sub-columns).

## Choose models made available? 

## Why can't I change the size of my sets on the go? 

## How to create consisitent ID for my project? 

## Should I scale my features?

## What metrics should I use?

## How large should my different sets be?

While there is no golden answer to this question, here are some guidelines:

- The training set will be the largest, and you will typically not annotate all of it, especially if using active learning. Because of this, you can make it as large as you want, especially if some of the classes you are looking for are infrequent.
- The validation and test set size mainly depend on how precise you want your model evaluation to be, how much data you are willing to annotate, and the expected frequency of the classes you are annotating. One rule of thumb is to have at least 100 observations of each label: if your smallest class is expected to appear in 20\% of texts, use 500 validation and test cases. You can also make the sets a bit larger and not annotate them completely, if you annotate them in random order.

## What set should I annotate first? 

We recommend starting by annotating your training set first, in order to get a grasp on your corpus and to stabilize the codebook. Only start annotating the validation and test sets once you are sure of the precise definition of each of your labels.

## What sets of features should I use?

Generally, the recommended features are Sentence embeddings for computing visualizations, topic models, and quick models. For quick models, they can be used along with regex features, if there are some keywords that are particularly informative (or that you want to disambiguate). In low-resource environments, fastText or DFM embeddings can be used instead of sentence embeddings. 

### How many annotations do I need?

There is no golden rule: it depends on the difficulty of the classification task.

A few dozen annotations per class might be enough for a simple task on short texts, but you might need several hundreds if you are looking for subtle details in longer texts.

In general, more is always better, but it also depends on how useful your annotations are (see *Active learning* section).