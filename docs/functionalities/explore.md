# Explore Page

This section describes each of the three tabs found in the Explore Page.

## Tabular View

The tabular view displays your data in a tabular view. Filters are available to assist your exploration.

![](../img/functionalities/tabular-view.png)

- Filters available
    - Select the dataset to explore ("train", "valid" or "test").
    - Select elements with a tag.
    - Select elements given a regex query.
- The table: The table contains 6 columns including the id, the label, the user who produced the label, the text, any comment and the date the label was produced.
    - Click on the <a class="action primary">id</a> to go to the [Annotate page](./annotate.md) and annotate the text input.
    - Click on the <a class="action primary">label</a> to annotate in the tabular view. Click <a class="action primary">Validate changes</a> to save changes in the database.

## Visualization

The visualization tab displays a projection of the embedding space in two dimension ([what is a projection?](../theoretical-concepts/index.md#what-is-a-projection)). Projection computed with either [UMAP](../theoretical-concepts/index.md#what-is-umap) or [t-SNE](../theoretical-concepts/index.md#what-is-t-sne). 

!!! warning 
    There is only one projection per project. 
    Computing a new projection will overwrite the current projection.

![](../img/functionalities/visualisation.png)

- <a class="action primary">Compute new projection</a>
    - <a class="parameter">Select a feature</a>: choose the set of feature ([what are features?](../theoretical-concepts/index.md#what-are-features))to use for the projection. If choosing several sets of features, they will be concatenated before projection. <a class="action secondary">Add a new feature</a> to [Compute new features](../theoretical-concepts/index.md#compute-new-features).
    - When using **UMAP**:
        - <a class="parameter">n neighbors</a>:
        - <a class="parameter">min distance</a>:
    - When using **t-SNE**:
        - <a class="parameter">perplexity</a>: XXX
        - <a class="parameter">learning rate</a>: XXX
        - <a class="parameter">init</a>: XXX
    - <a class="parameter">Feature scaling</a>: this is a method normalizes the range of independant variables (i.e. each feature) ([should I scale my features?](../theoretical-concepts/index.md#should-i-scale-my-features)).
- <a class="action secondary">Parameters</a> to see the parameters of the current projection.
- The visualization panel displays each text input in a 2D space. The color of the node depends on the label, _or the absence thereof_. 
    - <a class="icon">![](../img/icons/visualisation-control/frame.svg)</a> to select a subset of text inputs.
    - <a class="icon">![](../img/icons/visualisation-control/frame-off.svg)</a> removes the frame.
    - _If a frame exists_, <a class="icon">![](../img/icons/visualisation-control/lock.svg)</a><a class="action secondary"> Lock the selection</a> to lock on the frame. Going to the [Annotate page](./annotate.md) will only display elements in the frame.
    - Clicking a node displays the text input as well asprevious annotations and the [Annotation Panel](./annotate.md#annotation-panel), much like in the [Annotation page](./annotate.md)

Projections can be downloaded from the [Export page](./export.md#features).

## Topic model

The topic model ([what is a topic model?](../theoretical-concepts/index.md#what-is-a-topic-model)) section displays existing topic models (for a given project and user ??? XXX) and allows to compute new ones [BERTopic](https://bertopic.com/)[^1]. 

[^1]: Find a full tutorial on BERTopic for the social science [here](https://www.css.cnrs.fr/the-general-inquirer-in-the-time-of-llms-a-bertopic-tutorial/).

![](../img/functionalities/bertopic.png)

- <a class="action primary">Compute new BERTopic</a> to create a new topic model.
    - <a class="parameter">Name</a>: must be unique (with regard to? unique at all or unique per project ? unique per project per user? XXX )
    - <a class="parameter">Embedding model</a>: choose from the [available embedding models](../faq/faq.md#choose-models-made-available) to compute the embeddings that will be used for fitting the model. These embeddings will be computed if they do not exist already for a given dataset.
    - <a class="parameter">Number of neighbours</a>: [UMAP parameter](../theoretical-concepts/index.md#what-is-umap) — a dimension reduction algorithm; low values will generate a topic model focusing on local structures (i.e. very specific topics) whereas higher values will generate a topic model focusing on the global structure (i.e. global topics) (more [here](https://css-polytechnique.github.io/css-ipp-materials/pages/techy-notes.html#tbl-umap-parameters)).
    - <a class="parameter">Min topic size</a>: [HDBSCAN parameter](../theoretical-concepts/index.md#what-is-hdbscan) — a clustering algorithm —, this parameters correspond to the minimum number of elements in a group to be considered a cluster, otherwise the group is considered as noise. Increasing this value will generate few large groups; decreasing this value will generate many small groups.
    - <a class="parameter secondary">Outlier reduction</a>: If set to True, all text inputs considered as noise will be added to the closest topic ([more info](https://css-polytechnique.github.io/css-ipp-materials/pages/techy-notes.html#reduce-outliers-strategies)).
    - <a class="parameter secondary">Force compute embeddings</a>: If set to True, the app will first generate the embeddings overwriting any existing embeddings. 
    - <a class="parameter secondary">Input dataset</a>: What dataset should be used to fit the model (train, train + test + valid or the complete dataset uploaded to the project).
    - <a class="parameter secondary">Filter out texts of length lower than</a>: Before fitting the model, exclude text inputs of length inferior to this value. 
    - <a class="parameter secondary">Number of components</a>: [UMAP parameter](../theoretical-concepts/index.md#what-is-umap) — a dimension reduction algorithm; it defines the number of dimension the algorithm reduces the embeddings to. Low values will flatten the representation of the input texts, whereas higher values maintain a richer representation (more [here](https://css-polytechnique.github.io/css-ipp-materials/pages/techy-notes.html#tbl-umap-parameters)).
- The visual representation of the topics displays each text input as a node with a color corresponding to the topic generated by the topic model.
- <a class="action secondary">Parameters</a> to see the parameters of the current topic model.
- <a class="action primary">Convert to scheme</a> to create a [scheme](../theoretical-concepts/index.md#what-is-a-scheme) and assign labels using the topics generated. XXX Add NOTE REGARDING THE DANGERS OF DOING THAT
- <a class="action primary">Export topics</a> to download (csv file) the topic table displayed underneath.
- <a class="action primary">Export topic per text</a> to download a mapping of each element id[^2] to a the topic index.
- <a class="action primary">Topic model report</a> to download an HTML report with key insights (topics description, 2D map, hierarchical representation, representative documents and the parameters of the model).
- The table (downloadable with Export topics) summarises the topic model. 
    - Topic: the topic id.
    - Count: the number of elements in the topic.
    - Name: A standard name for the topic.
    - Representation: A list of keywords that represent the topic.
    - Representative docs: A list of documents that are at the core of the topic generated.

[^2]: As set up when [creating a project](./project-creation.md).