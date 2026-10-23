# Codebook Page

This section describes the Codebook page, the key elements and their interactions with the rest of the application.

![](../img/functionalities/codebook.png)

## Scheme management

At the top of the screen, you will find the [scheme](../conceptualizing/glossary.md#schemes) management component. It consists of a dropdown menu and 4 action buttons. 

- <span class="action primary">Current scheme</span> : Scheme to use for the current session.
- <span class="icon">![](../img/icons/plus.svg)</span> to create a new scheme, with a unique name and a type ([see available types](../conceptualizing/glossary.md#schemes))
- <span class="icon">![](../img/icons/rename.svg)</span> to rename the current scheme.
- <span class="icon">![](../img/icons/duplicate.svg)</span> to duplicate the current scheme with all annotations. 
- <span class="icon">![](../img/icons/delete.svg)</span> to delete the current scheme and its annotations. *This action cannot be undone*.


## Guidelines

The Codebook allows you to keep information on how to use the current scheme. 

- <span class="icon">![](../img/icons/rename.svg)</span> to enter editing mode (formatted in markdown).
- <span class="icon">![](../img/icons/book.svg)</span> to open the Codebook in a browser tab to access it during annotation.
- <span class="icon">![](../img/icons/download.svg)</span> to download the Codebook as a markdown file.

## Labels management

The table summarizes existing labels in the current scheme and the distribution of annotations for each dataset (train, validation and test). 

- <span class="parameter">New label name</span> <span class="action primary">Add</span> to create a new label.
- <span class="icon">![](../img/icons/delete.svg)</span> to delete the specific label.
- <span class="icon">![](../img/icons/rename.svg)</span> to rename the specific label (renaming a label to the name of an existing label will result in merging existing annotations).

The rows can be re-ordered through drag and drop. Reordering rows will change the order of the labels in the [Annotate Page](./annotate.md). 
