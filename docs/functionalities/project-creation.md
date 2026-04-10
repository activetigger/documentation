# Project Creation page

Project creation is available on the main page and lets you create a new project. 

![Overview of the Project Creation page](../img/functionalities/overview.png)

## Primary parameters

These parameters define the general project, only a subset (⚙️) can be modified after this step.

- ⚙️ <span class="parameter">Project name</span>: Unique name to identify the project. Could be changed in [Settings page](./settings.md).
- <span class="parameter">Dataset</span>: Data to use. Can be loaded :
    - From user, format Parquet, CSV or XLSX file, limit defined by the administrator. 
    - From another project (with access right)
- <span class="parameter">Id column</span>: index to identify each element in the treatment ; either from an existing column or row number. If the chosen index is not unique, an internal index is created different from the external index.
- ⚙️ <span class="parameter">Text column(s)</span>: The column(s) to use as text input. If several columns are selected, content of the columns will be concatenated with two linebreaks. 
- ⚙️ <span class="parameter">Language of the corpus</span>: General parameter used to suggest which models to use in the treatment. 
- ⚙️[^modify-column-annotation] <span class="parameter">Column(s) for existing annotations</span>: Load existing annotations. Each column is converted to a new scheme. Elements (XXX does it change how we select elements?)
- ⚙️ <span class="parameter">Column(s) for contextual information</span>: Information available to display in the [annotation page](./annotate.md).
- ⚙️[^modify-n-rows-trainset] <span class="parameter">Number of elements in the train set</span>: Sample of the general dataset used as train set
- ⚙️[^modify-valid-set] <span class="parameter">Number of elements in the validation set (optional)</span>: Sample of the general dataset used as validation set. Used for evaluation. This sample is randomly selected from the initla dataset before the train set.
- ⚙️[^modify-test-set] <span class="parameter">Number of elements in the test set (optional)</span>:  Sample of the general dataset used as test set. Used for evaluation. This sample is randomly selected from the initla dataset before the train set.

[^modify-column-annotation]: This parameter cannot be updated per se, but you can import annotations in [the Import tab in the Settings page](./settings.md#import)

[^modify-n-rows-trainset]: You can add N rows to your dataset in [the Parameters tab in the Settings page](./settings.md#parameters) but the rows selected will not follow the stratification rules you set up. We recommend creating larger sets than you'd need rather than importing new rows afterwards.

[^modify-valid-set]: This parameter cannot be updated per se, but you can drop the validation set and import a new one in [the Import tab in the Settings page](./settings.md#import)

[^modify-test-set]: This parameter cannot be updated per se, but you can drop the test set and import a new one in [the Import tab in the Settings page](./settings.md#import)

After setting the compulsory parameters, clicking the "Create" button will redirect you to the [Codebook page](./codebook.md) (or the [Annotate page](./annotate.md) if you have selected column(s) for existing annotation).

## Secondary parameters

Available in the "Advanced options" panel to configure specific treatments.

- <span class="parameter secondary">Prioritize existing labels</span>: When loading existing annotations, maximize the already annotated elements in the trainset. If there are not enough elements annotated to create all three sets, random elements will be picked. 
- <span class="parameter secondary">Select elements at random</span>: If set to `True`, the train, validation and test sets will be created by picking elements at random. If `Prioritize existing labels` is set to `True`, this parameter is ignored.
- <span class="parameter secondary">Stratify train set</span>: Force the stratification for the trainset ([What is stratification?](../theoretical-concepts/glossary.md#dataset-stratification)). If `Prioritize existing labels` is set to `True`, this parameter is ignored.
- <span class="parameter secondary">Stratify test set</span>:  Force the stratification for the test set ([What is stratification?](../theoretical-concepts/glossary.md#dataset-stratification)). If `Prioritize existing labels` is set to `True`, this parameter is ignored.
- <span class="parameter secondary">Column(s) used for stratification</span>: If `Stratify train set` and/or `Stratify test set`, the stratification will use the selected columns ([What is stratification?](../theoretical-concepts/glossary.md#dataset-stratification)). If `Prioritize existing labels` is set to `True`, this parameter is ignored.
- <span class="parameter secondary">Drop annotations for testset</span>: If set to `True` and columns have been selected for existing annotations, the annotations of elements in the testset will be dropped. 
- <span class="parameter secondary">Compute embeddings</span>: If set to `True`, upon creating the project, embeddings for the text inputs in the train, validation and test sets will start using [Sentence BERT](https://sbert.net/)
- <span class="parameter secondary">Seed</span>: The seed used for all random operations in the project.