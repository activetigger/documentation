# Settings page

The settings page contains many tabs with **moderate** to **high impacts** on your project. We describe them on this page.

## Parameters

This page displays the parameters of the project and allows editing or deleting the project.

![](../img/functionalities/parameters.png)

- <span class="action primary">Change parameters</span> to edit some parameters:
    - <span class="parameter">Project name</span>: [see Project Creation page](./project-creation.md#primary-parameters)
    - <span class="parameter">Text column(s)</span>: [see Project Creation page](./project-creation.md#primary-parameters)
    - <span class="parameter">Language of the corpus</span>: [see Project Creation page](./project-creation.md#primary-parameters)
    - <span class="parameter">Column(s) for contextual information</span>: [see Project Creation page](./project-creation.md#primary-parameters)
    - <span class="parameter">Add N elements in the train set</span>: Pick new elements from the dataset uploaded. XXX ⚠️ **Ignores stratification** ⚠️
- <span class="action red-danger">Delete project</span> to delete the project, annotations and models. **There is no going back.**

!!! note
    
    It is not made possible to manage the size of the sets and move elements around. Read more [here](../faq/faq.md#why-cant-i-change-the-size-of-my-sets-on-the-go)

## Features

Displays the available features and their parameters. 

- <span class="action primary">Add a new feature</span> to compute new features ([more details on the available features modes](../theoretical-concepts/index.md#representing-texts-with-features)).
    - if using **embeddings**:
        - <span class="parameter">Feature name</span>
        - <span class="parameter">Model to use</span>
        - <span class="parameter">Context window size</span>: The number of token per entry. After tokenization each input is truncated/padded to match this size.
    - if using **fasttext**:
        - <span class="parameter">Feature name</span>
        - <span class="parameter">Model to use</span>
    - if using **dfm**: Using `CountVectorizer` XXX @Julien
        - <span class="parameter">Feature name</span>
        - <span class="parameter">TF-IDF</span>: if set to True, applies TF-IDF to the feature matrix (XXX).
        - <span class="parameter">n-grams</span>: the size of n-grams to account for.
        - <span class="parmater">min term freq</span>: the minimum frequence for a n-gram to be included in the vocabulary.
        - <span class="parmater">max term freq</span>: the maximum frequence for a n-gram to be included in the vocabulary.
        - <span class="parameter">Norm</span>: if set to True, normalize the featres XXX What normalisation? before or after log ?
        - <span class="parameter">Log</span>: if set to True, apply logarithm function to the feature the featres.
    - if using **regex**: creates a boolean feature whether the regex query if found in the text input
        - <span class="parameter">Feature name</span>
        - <span class="parameter">Regex query</span>
    - if using **dataset**: imports from a column in the original dataset
        - <span class="parameter">Column to use</span>
        - <span class="parameter">Type of the feature</span>: either numerical or categorical.

Features can be downloaded from the [Export page](./export.md#features).

## Import 

The import tab allows you to import data for the current process outside of the [Project Creation page](./project-creation.md). 

![](../img/functionalities/import.png)

- **Import annotations**: import the annotations for the text inputs in the train dataset. The IDs must match. if the labels differ, new labels will be created. XXX or ignored? no idea. If annotations already exists, they will be overwritten.
    - <span class="parameter">File to upload</span>: Parquet, CSV or XLSX file, limit defined by the administrator.
    - <span class="parameter">Column for ID</span>: column from the loaded dataset that must match the IDs from the current text inputs. XXX Internal or external? 
    - <span class="parameter">Column for annotations</span>: column from the loaded dataset that contains the annotations to import.
    - <span class="action primary">Import annotations</span> to finalise the importation.
- **Validation set** and **Test set**: drop or import the validation or test set.
    - _if a validation/test set exists_, 
        - <span class="action red-danger">Drop Test/Validation set</span>: delete the set as well as the features. They will be re-computed.
    - _if the validation/test set does not exist_
        - <span class="parameter">File to upload</span>: Parquet, CSV or XLSX file, limit defined by the administrator.
        - <span class="parameter">ID column</span>: index to identify each element in the treatment ; either from an existing column or row number. If the chosen index is not unique, an internal index is created different from the external index.
        - <span class="parameter">Text column(s)</span>: The column(s) to use as text input. If several columns are selected, content of the columns will be concatenated with two linebreaks. 
        - <span class="parameter">Column(s) for existing annotations</span>: Load existing annotations. If labels are not found in the current scheme, they will be ignored.
        - <span class="parameter">Number of elements</span>: Number of rows 