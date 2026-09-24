# FAQ

In this section you will find frequently asked questions (FAQ) on ActiveTigger.   
For specific questions do not hesitate to reach out on [Discord](https://discord.gg/3uNnjw2k).

## Access and account management

### How can I recover my password?

For the moment, the only solution is to contact the administrator of your service to reinitialize it for you.

### If I destroyed my project, is it possible to recover the data?

No. 

### I have bugs or repetitive problems

Please open an issue on Github.

### Can I launch processes if the GPU is already full?

Yes, but your process will be put in a queue and you will need to wait for enough GPU memory to be available for the process to start. You can see your position in the queue at the bottom left-hand corner of the screen. You can try to decrease the batch size to lower the required memory.

## Training, validation and test sets

### How large should my different sets be?

While there is no golden answer to this question, here are some guidelines:

- The training set will be the largest, and you will typically not annotate all of it, especially if using active learning. Because of this, you can make it as large as you want, especially if some of the labels you are looking for are infrequent. 
- The validation and test set size mainly depend on how precise you want your model evaluation to be, how much data you are willing to annotate, and the expected frequency of the labels you are annotating. One rule of thumb is to have at least 100 observations of each label _(for a label representing roughly 20% of all annotations, consider annotating 500 text inputs for the validation set, and 500 more for the test set)_. You can also make the sets a bit larger and not annotate them completely, if you annotate them in random order. 
- If you are unsure about validation and test sizes, refrain from allocating all of your data into training, validation and test sets so that you can add data to these sets if you need to.

If you are still undecided, start by allocating 70% of your dataset to the train set, 5-10% to the validation set and 5-10% to the test set, but keep in mind that you may need to adjust these later. 

### Can I increase the size of the train set after creating the project?

Yes. In your project, click on the Settings tab and select Change parameters. There you can add N elements to the train set (without stratification). Please note that if you increase the size of your project, you then need to create a new feature in the Features tab of the Settings.  

## Data annotation

### What set should I annotate first? 

We recommend starting by annotating your training set first, in order to get a grasp on your corpus and to stabilize the codebook. Only start annotating the validation and test sets once you are sure of the precise definition of each of your labels.

### How many annotations do I need?

There is no golden rule: it depends on the difficulty of the classification task.

A few dozen annotations per label might be enough for a simple task on short texts, but you might need several hundreds if you are looking for subtle details in longer texts.

In general, more is always better, but it also depends on how useful your annotations are (see *Active learning* section).

### I have difficulties annotating my texts with my current scheme

If as a human annotator you are not able to decide how to annotate a text with the current scheme, maybe you would need to redesign your scheme (increasing or decreasing the number of labels, or re-conceptualizing them)

## Model hyperparameters and performance

### What sets of features should I use?

Generally, the recommended features are Sentence embeddings for computing visualizations, topic models, and quick models. For quick models, they can be used along with regex features, if there are some keywords that are particularly informative (or that you want to disambiguate). In low-resource environments, fastText or DFM embeddings can be used instead of sentence embeddings. 

### I have both good and bad prediction scores for my labels (I have annotated enough elements !)

Having heterogeneous scores can be a sign of ill-defined labels. We advise testing each label in a binary scheme to evaluate its relevance, in order to refine your codebook based on those results.

