# Codebook Page

This section describes the Codebook page, the key elements and their interactions with the rest of the application.

![](../img/functionalities/codebook.png)

## Scheme management

At the top of the screen, you will find the scheme ([what is a scheme?](../theoretical-concepts/index.md#what-is-a-scheme)) management component. It consists of a dropdown menu and 4 actions buttons. 

- **Dropdown menu**: Select the scheme to use. The name of the scheme in use can be found in the left panel, underneath the project name.
- **Action buttons**:
    - ![](../img/icons/plus.svg) Create a new scheme: Opens a modal to create a new scheme. To create a new scheme, you will need to choose: 
        - A scheme name
        - A type ([see available types](../theoretical-concepts/index.md#available-scheme-types))
    - ![](../img/icons/rename.svg) Rename the current scheme: Opens a modal to rename the current scheme. A new name will be required. XXX Do we say what it does in the background??
    - ![](../img/icons/duplicate.svg) Duplicate the current scheme: Creates a new scheme (`SCHEME-NAME_copy`) with the same labels names. Also copies the annotations. 
    - ![](../img/icons/delete.svg) Delete the current scheme: Delete the scheme, as well as the annotations. **This action is definitive.**


## The codebook 

Underneath the Scheme management component, you will find a the Codebook ([How to write a codebook](XXX)). 

- ![](../img/icons/rename.svg) Edit Codebook: Opens a modal with an edit panel and a preview panel. Clicking on "Save" or outside the modal will close the modal and save the edits.
- ![](../img/icons/book.svg) Open the Codebook in a new tab.
- ![](../img/icons/download.svg) Download the Codebook as a markdown file.

## Labels management

At the bottom of the page, you will find the label management component. It consists of a text input and a table. 

- The text input, with the ![](../img/icons/plus.svg), allows you to create a new label.
- The table: 
    - In the table, you will find all existing labels, as well as the number of elements, per label and set (train, valid and test). The rows can be re-ordered, the order of the rows will manage the order of the labels in the [Annotate Page](./annotate.md)
    - At the end of each row, you will find a ![](../img/icons/delete.svg) icon and a ![](../img/icons/rename.svg) icon to delete and rename the labels. If renaming a label to another, the annotations will be merged. 