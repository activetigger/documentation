# Annotate page

The annotate panel is the main page of the app to annotate your text data. 

![](../img/functionalities/annotate.png)

## Selecting text inputs to annotate

There are several ways to select a subset of text inputs. XXX more?

- <a class="parameter">Dataset</a>: Select the dataset on which you are working (train, validation or test).
- <a class="parameter">Selection mode</a>: Change the order in which elements are showed (fixed, or random).
- <a class="parameter">Active Mode</a>: Allows to choose a model for [Active Learning](#active-learning). This unlocks new selection modes: 
    - active: orders the text inputs by decreasing entropy.
    - Max LABEL: orders the text inputs by decreasing probability to be of label LABEL.
- <a class="parameter">Filter by Tag/User</a>: Only displays elements already have label (by current user) or don't, are tagged with a specific LABEL, or by a certain user ("by USER"). 
- <a class="parameter">Filter by content</a>: Only displays elements containing a certain regex pattern.

After setting a new dataset/selection method/filter, <a class="action primary">![](../img/icons/refresh.svg)</a> will apply the changes and fetch a new element.

## Annotation panel

The center of the page displays the text box as well as several buttons: 

- <a class="action primary">LABEL</a>: To tag the text input with the given LABEL and move on to the next text input.
- <a class="action primary">![](../img/icons/no-tag.svg) No tag</a>: if a tag exists, remove it and move on to the next text input.
- <a class="action primary">Skip</a>: Move on to the next text input without altering the annotation.

The "Comment" section allows to save a comment with the annotation of the text input.

### Display parameters

<a class="action secondary">![](../img/icons/display.svg)</a> opens a modal to modify the annotation panel display.

- <a class="parameter">Annotation History</a>: to display previous annotations of the given text input.
- <a class="parameter">Existing annotation</a>: to display existing annotation on the current text input. XXX do you see other people's label ? can't remember
- <a class="parameter">Show prediction stats</a>: to display a button for the label predicted by the model, bound the the hotkey "P" (if Active Mode is on).
- <a class="parameter">Show prediction stats</a>: to display the model's probability as well as the predicted label (if Active Mode is on).
- <a class="parameter">Element history</a>: to display previous tags at the bottom of the text box.
- <a class="parameter">Tokens approximation</a>: Approximate extimation of text truncation. Given a window size, text inputs exceeding this limit will be written in another column to emphasise possible truncation. This parameter is only visual and has no other impact.
- <a class="parameter">Height</a>: to set the height of the text box.
- <a class="parameter">Width</a>: to set the width of the text box.
- <a class="parameter">Force one column layout</a>: to display the label buttons in a column.
- <a class="parameter">Highlight words in the text</a> Similar to <a class="parameter">Filter by content</a> but without removing items not containing the regex expression.

### Annotation history

The last 100 text inputs annotated are visible underdeath the annotation page. For Active Learning to work best, the application retains, at all time, the list of text inputs annotated. This way, unless you <a class="action secondary">Clear history</a>, these elements will not be shown again.

## Active learning

<!-- TODO: Explain how active mode works with BERT models -->

### Models with ignored labels

## Annotate (multi-label)

The general layout is unchanged, to annotate elements, select one or more label in the dropdown menu and <a class="action primary">![](../img/icons/validate.svg)</a> to save the annotation and move on to the next text input.

## Annotate (span)

To annotate the text, first select a <a class="action primary">LABEL</a>, then highlight the text in the text box. Click on the highlight to remove. <a class="action primary">![](../img/icons/validate.svg) Validate the annotation</a> to save the annotation and move on to the next text input.