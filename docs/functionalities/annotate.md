# Annotate page

The Annotate panel is the main page of the app to annotate your data. 

![](../img/functionalities/annotate.png)

## Selecting text inputs to annotate

There are several ways to select a subset of text inputs.

- <span class="parameter">Dataset</span>: select the dataset on which you are working (train, validation or test).
- <span class="parameter">Selection method</span>: change the order in which elements are shown. 
   - fixed (in the order of the original dataset)
   - random
- <span class="parameter">Active Mode</span>: toggling this mode allows you to choose a model for Active Learning (more about the [concept](../conceptualizing/general.md#what-is-active-learning), more about its [implementation](#active-learning-in-practice)). This unlocks new selection methods: 
    - max LABEL: orders the text inputs by decreasing probability to be of a given LABEL.
    - active: orders the text inputs by decreasing entropy (prioritizing uncertain predictions).
    - active LABEL: orders the text inputs by decreasing entropy with regard to this specific LABEL.
- <span class="parameter">Prompts</span>: only displays elements matching a specific prompt. 
    - Enter a prompt, then <span class="action primary">Create prompt</span>, and exit the window.
    - This unlocks a new selection method, <span class="parameter">prompt (embedding)</span> which allows you to select the prompt you've typed.
- <span class="parameter">Filter by Tag/Users</span>: only displays elements with specific characteristics
    - being labeled with LABEL
    - being labeled by a specific user
    - with comments: elements which have a comment
    - wrong prediction: elements for those there is a disagreement between annotation and prediction
    - predicted as LABEL by current active model
- <span class="parameter">Filter by content</span>: only displays elements matching a search / RegEx expression (more about [RegEx](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions/Cheatsheet)).
    - To search in the context variables, use `CONTEXT=[your regex]` before the search
    - It is possible to use a query for more complex selection with under the hood [Pandas query](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.query.html) ; use `QUERY=[your query]`.
- <span class="parameter">Filter by projection</span>: when inputs are selected via a frame in the [Visualization tab of the Explore page](../functionalities/explore.md#visualization), you can <span class="parameter">Lock on projection</span> to only display the inputs contained in the frame. 


## Annotation panel

The center of the page displays the text box as well as several buttons. 

- <span class="action primary">LABEL</span> : tag the text input with the given LABEL and move on to the next text input.
- <span class="action primary">![](../img/icons/no-tag.svg) No tag</span> : if a tag exists, remove it and move on to the next text input.
- <span class="action primary">Skip</span> : move on to the next text input without altering the annotation.
- Add a comment to your annotation in the comment text box.
- If you want to access the Codebook during annotation, click on <span class="action secondary">![](../img/icons/book.svg)</span>. 

Most actions can be triggered with hotkeys (1,2,3 .. → or DEL).

### Display parameters

<span class="action secondary">![](../img/icons/display.svg)</span> opens a modal to modify the annotation panel display.

- <span class="parameter">Annotation History</span>: if ticked, displays previous annotations of the session.
- <span class="parameter">Existing annotation</span>: if ticked, displays existing annotation of the current text input.
- <span class="parameter">Show prediction</span>: if ticked, displays a button for the label predicted by the model (bound to the hotkey "P") when Active Mode is on.
- <span class="parameter">Show prediction stats</span>: if ticked, displays the model's probability as well as the predicted label (if Active Mode is on).
- <span class="parameter">Element history</span>: if ticked, displays previous tags of the current text input at the bottom of the text box.
- <span class="parameter">Mean annotation time</span>: if ticked, displays at the bottom of the screen the mean annotation time for the future annotations performed during the session. If the history is cleared, the annotation time is reset. 
- <span class="parameter">Tokens</span>: approximate an estimation of text truncation. Given a window size, text inputs exceeding this limit will be written in another color to emphasise possible truncation. This parameter is only visual and has no other impact.
- <span class="parameter">Height</span>: set the height of the text box.
- <span class="parameter">Width</span>: set the width of the text box.
- <span class="parameter">Force bottom labels</span>: if ticked, displays the label buttons horizontally under the text box.
- <span class="parameter">Force complete labels</span>: if ticked, adapts the label buttons' font size so that the whole label is legible.
- <span class="parameter">Highlight first</span> 
- <span class="parameter">Highlight words in the text</span> Similar to <span class="parameter">Filter by content</span> but without removing items not containing the regex expression.

### Annotation history

The last hundred inputs annotated are visible underneath the annotation panel. For Active Learning to work best, the application retains, at all times, the list of text inputs annotated. This way, unless you <span class="action secondary">Clear history</span>, these elements will not be shown again.

- You can choose to view your annotation history as cards (default) or as a table (by clicking on <span class="action secondary">![](../img/icons/display-as-table.svg)</span>). 
- You can also hide the history without clearing it by clicking on <span class="action secondary">![](../img/icons/hide-history.svg)</span>.

!!! warning 
    Changing scheme will automatically clear the history.

### Active Learning in practice

*Read about the concept of [Active learning](../conceptualizing/general.md#what-is-active-learning)*.

In the Annotate page, you can select a model (quick or BERT) to use its predictions for <span class="icon">![](../img/icons/active-tiger.svg)</span> Active Learning. <br/> This will allow you to see the chosen model's predictions ("guesses") for which category a given element belongs to, allowing you to correct it or confirm this prediction by manual annotation.

To use BERT models in active learning, you must first compute the predictions on the dataset, in the [Evaluate tab](./model.md#evaluation) <span class="action primary">Compute statistics on current annotations</span>.

When active learning is on, clicking on <span class="icon">![](../img/icons/active-tiger.svg) Model name</span> can allow you to: 
- Retrain quick model, either manually (<span class="action secondary">![](../img/icons/refresh.svg) Retrain now</span>) or every x annotations.
- Change model used for active learning.
- Deactivate active learning (<span class="action secondary">![](../img/icons/no-tag.svg) Deactivate</span>). <br/>

 Models trained on a reduced number of labels can be used, they will simply ignore unseen labels.

!!! tip
    The selection mode Max LABEL is especially useful in the early stages when the model "fails with confidence". This mode selects the elements on which the selected model makes confident predictions, but these may very well be incorrect. You can correct these predictions by correctly labelling elements in this mode, steering the model toward a correct definition of each label. Conversely, the selection mode Active LABEL picks elements on which the model is least confident in its prediction, allowing you to correct it in the same way. Switching between these modes in the annotations phase is often a helpful way to produce a functioning model faster.

## Curate

This section allows you to see agreements and disagreements in existing annotations, both between several users working on the same scheme and between different coding schemes.

In the "Current scheme" tab, disagreements between different users are displayed, meaning cases when several users annotating data in a given project have annotated the same element differently. You can resolve these disagreements by choosing a final label.

In the "Between scheme" tab, you can compare different annotations of the same element between different coding schemes.

## Annotate (multi-label)

When applying multiple labels to the same element, the general layout is unchanged. To annotate elements, select one or more labels in the dropdown menu and <span class="action primary">![](../img/icons/validate.svg) Validate</span> to save the annotation and move on to the next element.

## Annotate (span)

To annotate the text, first select a <span class="action primary">LABEL</span>, then highlight the text in the text box. 
Click on the highlight to remove it.    
<span class="action primary">![](../img/icons/validate.svg) Validate</span> the annotation to save the annotation and move on to the next text input.
