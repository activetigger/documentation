# Settings page

The Settings page contains many tabs with **moderate** to **high impacts** on your project. 

## Parameters

This tab displays the parameters of the project and allows editing of some parameters or deletion of the project. 

![](../img/functionalities/parameters.png)

- <span class="action primary">Change parameters</span> to edit some parameters:
    - <span class="parameter">Project name</span>: [see Project Creation page](./project-creation.md#primary-parameters)
    - <span class="parameter">Text column(s)</span>: [see Project Creation page](./project-creation.md#primary-parameters)
    - <span class="parameter">Language of the corpus</span>: [see Project Creation page](./project-creation.md#primary-parameters)
    - <span class="parameter">Column(s) for contextual information</span>: [see Project Creation page](./project-creation.md#primary-parameters)
    - <span class="parameter">Add N elements in the train set</span>: Pick new elements from the dataset uploaded. *This action ignores stratification*.

!!! note
    
    It is not possible to directly add elements to the test and validation sets. However, you can drop them and import news ones in the Import tab (learn more [in the FAQ](../faq/faq.md#can-i-add-a-test-set-or-validation-set-after-creating-the-project-if-i-havent-already) and get instructions [below](./settings.md#import)). 

- <span class="action red-danger">Delete project</span> to delete the project, including annotations and models. 

!!! warning

    Deleting the project is **irreversible**. **It cannot be undone**. 

## Features

Displays the available features and their parameters. 

![](../img/functionalities/features.png)

- <span class="action primary">Add a new feature</span> to compute new features ([more details on the available features modes](../conceptualizing/general.md#representing-texts-with-features)).
    - if using **sentence or BERT embeddings**:
        - <span class="parameter">Feature name</span>
        - <span class="parameter secondary">Model to use</span>
        - <span class="parameter secondary">Pooling</span> for BERT models: average all token embeddings (mean) or use the CLS token's only. 
        - <span class="parameter secondary">Max length tokens</span>: the number of token per entry (context window size). After tokenization each input is truncated/padded to match this size.
        - <span class="parameter secondary">Batch size</span>: number of entries that the model keeps in memory at once.  
    - if using **fasttext** (See the [Features concept](../conceptualizing/general.md#representing-texts-with-features)):
        - <span class="parameter">Feature name</span>
        - <span class="parameter secondary">Model to use</span>
    - if using **dfm**: Using `CountVectorizer`
        - <span class="parameter">Feature name</span>
        - <span class="parameter secondary">TF-IDF</span>: if set to True, applies TF-IDF.
        - <span class="parameter secondary">N-grams</span>: the size of n-grams to account for.
        - <span class="parameter secondary">Min term freq</span>: the minimum frequency for an n-gram to be included in the vocabulary.
        - <span class="parameter secondary">Max term freq</span>: the maximum frequency for an n-gram to be included in the vocabulary.
        - <span class="parameter secondary">Norm</span>: if set to True, normalize the features at the end
        - <span class="parameter secondary">Log</span>: if set to True, apply logarithm function to the features.
    - if using **regex**: creates a boolean feature indicating whether the regex query is found in the text input
        - <span class="parameter">Feature name</span>
        - <span class="action input">Regex query</span>
    - if using **dataset**: imports from a column in the original dataset
        - <span class="parameter">Column to use</span>
        - <span class="parameter">Type of the feature</span>: either numerical or categorical.
    - if using **import**: import a pre-computed feature in CSV, XLSX or Parquet format. The file must contain one row per project element, matched on the project's ID. Only numeric columns can be imported.

Features can be downloaded from the [Export page](./export.md#features).

## Import 

The import tab allows you to import data for the current process outside of the [Project Creation page](./project-creation.md). 

![](../img/functionalities/import.png)

- **Import annotations**: import annotations for existing elements in the train dataset. The IDs must match with the IDs in your train set. If the labels differ, new labels will be created. **If annotations already exist, they will be overwritten.**
    - <span class="parameter">File to upload</span>: Parquet, CSV or XLSX file, limit defined by the administrator.
    - <span class="parameter">Column for ID</span>: column from the loaded dataset that must match the external IDs from the current text inputs.
    - <span class="parameter">Column for annotations</span>: column from the loaded dataset that contains the annotations to import.
    - <span class="action primary">Import annotations</span> to finalise the importation.
- **Validation set** and **Test set**: drop or import the validation or test set.
    - _if a validation/test set exists_, 
        - <span class="action red-danger">Drop Test/Validation set</span>: delete the set as well as the features. They will be re-computed.
    - _if the validation/test set does not exist_
        - <span class="parameter">File to upload</span>: Parquet, CSV or XLSX file, limit defined by the administrator.
        - <span class="parameter">ID column</span>: index to identify each element in the treatment ; either from an existing column or row number. If the chosen index is not unique, an internal index is created different from the external index.
        - <span class="parameter">Text column(s)</span>: The column(s) to use as text input. If several columns are selected, content of the columns will be concatenated with two linebreaks. 
        - <span class="parameter">Column(s) for existing annotations (optional)</span>: load existing annotations. The column(s) containing the labels must have the same name as the scheme(s) in which the labels and the set will be imported. If labels are not found in the scheme, they will be ignored.
        - <span class="parameter">Number of elements</span>: number of rows in the set. 

## Session history 

The Session history tab shows the last 100 actions you performed in the project. 