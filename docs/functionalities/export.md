# Export page

On this page, you can export your existing data, annotations, and models.

## Annotations

This tab allows users to download annotated datasets (train, test, validation or all).

![](../img/functionalities/export-annotations.png)

- <span class="action primary">Tags: train</span>, <span class="action primary">Tags: test</span>, <span class="action primary">Tags: eval</span> to download the annotations for the train, test or validation dataset. Text inputs without an annotation are dropped. 
- <span class="action primary">All annotations/schemes</span> to download the full dataset (train, test and eval) with all columns from the original dataset and a column per scheme. Text inputs without annotations are included.
- <span class="action primary">Static link to the raw dataset (click right, save as...)</span> to download the full dataset (as a Parquet file) as uploaded when creating the project.

## Features

![](../img/functionalities/export-features.png)

- <span class="action primary">Export selected features</span> to download the features and the corresponding index.
- <span class="action primary">Export current projection</span> to download the projection's nodes' coordinates computed in the [Visualisation tab of the Explore page](./explore.md#visualization) and the corresponding index.

## Models

![](../img/functionalities/export-models.png)

- <span class="action primary">Prediction on external dataset</span> to upload a new dataset and infer labels for each row using the selected model.
- <span class="action primary">Prediction on complete dataset</span> to infer labels on the full dataset as imported upon project creation.
- <span class="action secondary">Export fine-tuned model (large file)</span> to download the weights of the fine-tuned model (good practice for reproducibility).
