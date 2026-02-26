# Codebook Page

This section describes the Codebook page, the key elements and their interactions with the rest of the application.

![](../img/functionalities/codebook.png)

## Scheme management

At the top of the screen, you will find the scheme ([what is a scheme?](../theoretical-concepts/index.md#what-is-a-scheme)) management component. It consists of a dropdown menu and 4 actions buttons. 

- <a class="primary-action">Current scheme</a>: Scheme to use for the current session.
- <a class="icon">![](../img/icons/plus.svg)</a> Create a new scheme, with a unique name and a type ([see available types](../theoretical-concepts/index.md#available-scheme-types))
- <a class="icon">![](../img/icons/rename.svg)</a> Rename the current scheme.
- <a class="icon">![](../img/icons/duplicate.svg)</a> Duplicate the current scheme with all annotations. 
- <a class="icon">![](../img/icons/delete.svg)</a> Delete the current scheme and its annotations. **This action is definitive.**


## Guidelines

Codebook allows to keep information on how to use the current scheme ([How to write a codebook](XXX)). 

- <a class="icon">![](../img/icons/rename.svg)</a> Access edition mode.
- <a class="icon">![](../img/icons/book.svg)</a> Open the Codebook in a browser tab to access it during annotation.
- <a class="icon">![](../img/icons/download.svg)</a> Download the Codebook as a markdown file.

## Labels management


- <a class="parameter">New label name</a> <a class="icon">![](../img/icons/plus.svg)</a> Create a new label.
- <a class="icon">![](../img/icons/delete.svg)</a> delete the specific label
- <a class="icon">![](../img/icons/rename.svg)</a> rename the specific label (you can use to merge annotations with another label) 


The table summarize existing labels in the current scheme, the distribution of annotations for each dataset (train, valid and test). The rows can be re-ordered, the order of the rows will manage the order of the labels in the [Annotate Page](./annotate.md)