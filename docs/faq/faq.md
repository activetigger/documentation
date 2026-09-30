# FAQ

In this section you will find frequently asked questions (FAQ) on ActiveTigger.   
For specific questions do not hesitate to reach out on [Discord](https://discord.gg/3uNnjw2k).

## Access and account management

### How can I recover my password?

If you are using the CREST instance (default online version), you can reset your password by clicking on the "Reset password" button on the log page. You will receive an email at the registered address with instructions to reset it. 
If you are deploying your own instance, it will depend if the mail option is activated. If not, the only solution is to contact the administrator to reinitialize it for you.

### If I destroyed my project, is it possible to recover the data?

No. There is no copy of the data outside the one which is used by the project. We recommend you export your annotations regularly. 

### I have bugs or repetitive problems.

You can have a look at the "Help" and "Bugs" sections of our [Discord community](https://discord.gg/3uNnjw2k) to see if someone else has had or is having the same issue. You can also directly expose your problem and ask your questions in these dedicated channels.     
If you are sure that there is a bug, we invite you to open an issue on [Github](https://github.com/activetigger/activetigger).

### Can I launch processes if the GPU is already under use?

Yes, but your process will be put in a queue and you will need to wait for enough GPU memory to be available for the process to start. You can see your position in the queue at the bottom left-hand corner of the screen.

## Train, validation and test sets

### What size should my train, validation and test sets be?

While there is no golden answer to this question, here are some guidelines:

- The training set will be the largest, and you will typically not annotate all of it, especially if using active learning. Because of this, you can make it as large as you want, in particular if some of your labels are infrequent. However, keep in mind that the train set will be loaded in memory and making it larger can add a computational cost. 
- The validation and test set size mainly depend on how precise you want your model evaluation to be, how much data you are willing to annotate, and the expected frequency of the labels you are annotating. One rule of thumb is to have at least 100 observations of each label _(for a label representing roughly 20% of all annotations, consider annotating 500 text inputs for the validation set, and 500 more for the test set)_. You can also make the sets a bit larger and not annotate them completely, if you annotate them in random order. 
- If you are unsure about validation and test sizes, refrain from allocating all of your data into training, validation and test sets so that you can add data to these sets if you need to.

If you are still undecided, start with a size of 10,000 data points for the train set, 1,000 for the validation set, and 1,000 for the test set. You may need to adjust these later as your knowledge of the data improves. 

### Can I increase the size of the train set after creating the project?
Yes. In your project, click on the Settings tab and select Change parameters. There you can add N elements to the train set (without stratification). Please note that if you increase the size of your project, you then need to create a new feature in the Features tab of the Settings.  

### Can I add a test set (or validation set) after creating the project if I haven't already? 
Yes. You can add your validation and/or test sets whenever you want. You need to prepare a valid set outside of ActiveTigger (be careful that no data point from your training set appears in your validation and test sets). Then go to Settings, click on the Import tab, and import your set.

### What should I do if I realise that the test set (or validation set) is the wrong size?
If you think that it is too big, you don’t have to do anything. Simply annotate the number of data points that you want *in random order*. Untagged values will be ignored.   

If you think that it is too small, you can drop your current test set and upload another one
- First, export your test set and all your annotations: click on Export, then on “Tags: test” and “All annotations / schemes”.
- Using external tools (e.g. R or Python editors), gather the elements that have not been allocated to any set: take your original dataset and remove the elements present in “All annotations / schemes" dataset. Randomly draw the N elements that you wish to add and combine them with the “Tags: test” set that you have exported. 
- Back in ActiveTigger, drop the current test set: go to Settings, click on Import, then on “Drop Test set”.
- In the same window, you can now import the new test set containing the additional N elements. 

## Data annotation

### Should I annotate my data at the sentence-level, paragraph-level or document-level? 
The choice of an annotation unit depends on your research question, your data and the technical means available to you. Here are five questions you should pay attention to to make up your mind:
- What are you _looking for_? This may be the most important question. For instance, if you are looking for the presence of a word or a sentence within a text, then the sentence-level is enough; if you are looking to extract a theme where the meaning of a sentence depends on neighbouring sentences, then you should work at least at the paragraph level. 
- Does your chosen unit have _thematic homogeneity_? If a unit addresses several themes at once, meaning will be diluted and the model’s performance will deteriorate. You should select a unit with more consistency. 
- What is the likely _distribution of your labels_ across units? Though low units are generally easier to deal with, choosing a low unit can sometimes make a rare label even rarer. If two annotation units make sense, choose the one for which labels will be most evenly distributed.
- Is there a model appropriate to your data whose _context window_ fits your chosen unit? For each model, the size that each entry can be (the context window) is capped. The base context window is 512 tokens (approx 300-400 English words), but some models can now go up to 8192 tokens. If no model appropriate to your data has a right context window, you should consider a lower annotation unit. Otherwise, ask yourself whether it is acceptable that data points exceeding the context window are truncated. 
- Do you have enough _computing power_ to deal with your chosen unit? The bigger the context window is, the more computing power is needed to fine-tune the model. Be aware that if you do not have your own GPU and plan on using the CREST instance, the maximum context window that you can reasonably compute is 1024 tokens. 

### What set should I annotate first? 

We recommend starting by annotating your training set first, in order to get a grasp on your corpus and to stabilize the codebook. Only start annotating the validation and test sets once you are sure of the precise definition of each of your labels.

### How many annotations do I need in the train set?

There is no golden rule: it depends on the difficulty of the classification task.

A few dozen annotations per label might be enough for a simple task on short texts, but you might need several hundreds if you are looking for subtle details in longer texts. In any case, it is good practice to annotate roughly the same amount of texts per label. 

In general, more is always better, but it also depends on how useful your annotations are (see *Active learning* section).

### I have difficulties annotating my texts with my current scheme

If as a human annotator you are not able to decide how to annotate a text with the current scheme, maybe you would need to redesign your scheme (increasing or decreasing the number of labels, or re-conceptualizing them)

## Model hyperparameters and performance

### What sets of features should I use?

Generally, the recommended features are Sentence embeddings for computing visualizations, topic models, and quick models. For quick models, they can be used along with regex features, if there are some keywords that are particularly informative (or that you want to disambiguate). In low-resource environments, fastText or DFM embeddings can be used instead of sentence embeddings. 

### I have both good and bad prediction scores for my labels, though I have annotated enough elements !

Having heterogeneous scores can be a sign of ill-defined labels. We advise testing each label in a binary scheme to evaluate its relevance, in order to refine your codebook based on those results.

### Can I export a model and then import it in a new project, on new data?
It is not currently possible to import models. However, you can compute predictions on an external dataset using a fine-tuned model from one of your projects.   
To do that, go in the Model tab, then in the Prediction tab. Select the model that you want to use, click on “Prediction on an external dataset” and choose your file. You can then download the predictions in the Export tab. 

