# Codebook Page

This section describes the Codebook page, the key elements and their interactions with the rest of the application.

![](../img/functionalities/codebook.png)

## Scheme management

At the top of the screen, you will find the scheme ([what is a scheme?](../theoretical-concepts/glossary.md#schemes)) management component. It consists of a dropdown menu and 4 actions buttons. 

- <span class="action primary">Current scheme</span>: Scheme to use for the current session.
- <span class="icon">![](../img/icons/plus.svg)</span> to create a new scheme, with a unique name and a type ([see available types](../theoretical-concepts/glossary.md#schemes))
- <span class="icon">![](../img/icons/rename.svg)</span> to rename the current scheme.
- <span class="icon">![](../img/icons/duplicate.svg)</span> to duplicate the current scheme with all annotations. 
- <span class="icon">![](../img/icons/delete.svg)</span> to delete the current scheme and its annotations. **This action is definitive.**


## Guidelines

Codebook allows to keep information on how to use the current scheme ([How to write a codebook](XXX)). 

- <span class="icon">![](../img/icons/rename.svg)</span> to access edition mode.
- <span class="icon">![](../img/icons/book.svg)</span> to open the Codebook in a browser tab to access it during annotation.
- <span class="icon">![](../img/icons/download.svg)</span> to download the Codebook as a markdown file.

## Labels management


- <span class="parameter">New label name</span> <span class="icon">![](../img/icons/plus.svg)</span> to create a new label.
- <span class="icon">![](../img/icons/delete.svg)</span> to delete the specific label
- <span class="icon">![](../img/icons/rename.svg)</span> to rename the specific label (you can use to merge annotations with another label) 


The table summarizes existing labels in the current scheme, the distribution of annotations for each dataset (train, valid and test). The rows can be re-ordered, the order of the rows will manage the order of the labels in the [Annotate Page](./annotate.md)