# Project Creation page

This section describes the process of creating a new project.

![Overview of the Project Creation page](../img/functionalities/overview.png)

## Basic parameters

In this section we describe the parameters to

| Parameter                                |  Compulsory | Default Value       |
| :--------------------------------------- | :---------: | :------------------ |
| <a class="parameter">Project name</a>                             |     ✅      | "Project-TIME-DATE" |
| <a class="parameter">Dataset</a>                                  |     ✅      |                     |
| <a class="parameter">Id Column</a>                                |     ✅      | "Row number"        |
| <a class="parameter">Text column(s)</a>                           |     ✅      |                     |
| <a class="parameter">Language of the corpus</a>                   |     ✅      | "English"           |
| <a class="parameter">Column(s) for existing annotations</a>       |     ❌      |                     |
| <a class="parameter">Column(s) for contextual information</a>     |     ❌      |                     |
| <a class="parameter">Number of elements in the train set</a>      |     ✅      | 100                 |
| <a class="parameter">Number of elements in the validation set</a> |     ❌      | 0                   |
| <a class="parameter">Number of elements in the test set</a>       |     ❌      | 0                   |

- <a class="parameter">Project name</a>: This name is used to reference all annotations, models and more. You will be able to change this name in the [Settings page](./settings.md).
- <a class="parameter">Dataset</a>: The dataset you will use for annotation annotating and training models. You can used datasets from different origins:
    - <a class="parameter">Load from disk</a>: You can load a dataset from your device. The file must be a Parquet ([troubleshoot for Parquet files](../faq/faq.md#trouble-shoot-with-parquet-files)), CSV or XLSX file **under 400MB**. 
    - <a class="parameter">Load from another project</a>: You can load a dataset from any other project that you have access to (XXX which access??).
- <a class="parameter">Id Column</a>: The column to use as an index. You can choose a column from your dataset, or choose to use the row number from the original dataset you've loaded. If you provide a column, the column must contain unique elements, if some elements are redundant, the row number will be used instead. (XXX Mention id_internal / id_external)
- <a class="parameter">Text column(s)</a>: The column(s) to use as text input. If several columns are selected, content of the columns will be concatenated with two linebreaks. 
- <a class="parameter">Language of the corpus</a>: This information will be used to provide you with relevant models. You will still be able to use multilingual models or models in another language. 
- <a class="parameter">Column(s) for existing annotations</a>: If you already have annotations in your dataset and wish to use them, every column selected will generate a new scheme with the detected labels. Elements (XXX does it change how we select elements?)
- <a class="parameter">Column(s) for contextual information</a>: The content of these columns will be displayed in the [annotation page](./annotate.md). *For instance, if you annotate journal articles, you may want to know the date or the name of the journal.* 
- <a class="parameter">Number of elements in the train set</a>: The number of elements to include in the trainset. If you are not planning on training models you can put all your texts inputs in the train set and ignore the validation and test sets.
- <a class="parameter">Number of elements in the validation set</a>: The number of elements to include in the validation set.
- <a class="parameter">Number of elements in the test set</a>: The number of elements to include in the test set. 

After setting the compulsory parameters, clicking the "Create" button will redirect you to the [Codebook page](./codebook.md) (or the [Annotate page](./annotate.md) if you have selected column(s) for existing annotation).

## Advanced parameters

Some parameters are hidden under the banner "Advanced options". We describe them here

| Parameter                         |  Compulsory | Default Value   |
| :-------------------------------- | :---------: | :-------------- |
| <a class="parameter">Prioritize existing labels</a>        |     ❌      | `False`         |
| <a class="parameter">Select elements at random</a>         |     ❌      | `True`          |
| <a class="parameter">Stratify train set</a>                |     ❌      | `False`         |
| <a class="parameter">Stratify test set</a>                 |     ❌      | `False`         |
| <a class="parameter">Column(s) used for stratification</a>  |     ❌      |                 |
| <a class="parameter">Drop annotations for testset</a>      |     ❌      | `False`         |
| <a class="parameter">Compute embeddings</a>                |     ❌      | `True`          |
| <a class="parameter">Seed</a>                              |     ❌      | a random number |

- <a class="parameter">Prioritize existing labels</a>: If you have selected columns for existing annotations, setting this parameter to `True`, the train, validation and test sets will be created from elements already annotated. If there are not enough elements annotated to create all three sets, random elements will be picked. 
- <a class="parameter">Select elements at random</a>: If set to `True`, the train, validation and test sets will be created by picking elements at random. If `Prioritize existing labels` is set to `True`, this parameter is ignored.
- <a class="parameter">Stratify train set</a>: Whether or not, you wish to stratify the train set ([What is stratification?](../theoretical-concepts/index.md#what-is-the-stratification-of-a-dataset)). If `Prioritize existing labels` is set to `True`, this parameter is ignored.
- <a class="parameter">Stratify test set</a>: Whether or not, you wish to stratify the test set ([What is stratification?](../theoretical-concepts/index.md#what-is-the-stratification-of-a-dataset)). If `Prioritize existing labels` is set to `True`, this parameter is ignored.
- <a class="parameter">Column(s) used for stratification</a>: If `Stratify train set` and/or `Stratify test set`, the stratification will use the selected columns ([What is stratification?](../theoretical-concepts/index.md#what-is-the-stratification-of-a-dataset)). If `Prioritize existing labels` is set to `True`, this parameter is ignored.
- <a class="parameter">Drop annotations for testset</a>: If set to `True` and columns have been selected for existing annotations, the annotations of elements in the testset will be dropped. You will have to annotate these elements again. 
- <a class="parameter">Compute embeddings</a>: If set to `True`, upon creating the project, embeddings for the text inputs in the train, validation and test sets will start using [Sentence BERT](https://sbert.net/)
- <a class="parameter">Seed</a>: The seed used for all random operations in the project.