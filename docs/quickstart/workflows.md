# Workflows

This page presents possible ways of using Tigger for your research and how to do it.

## Annotate a corpus collaboratively

Active Tigger's first purpose is to make collaborative annotation seamless. This means: 

- Creation of a scheme ([what is a scheme?](XXX)) and a codebook for the project.
- Annotation of the text inputs by each user.
- Comparison of the annotations and measure agreement
- Export the annotated corpus for analysis

Here is an overlook of the steps necessary to complete this path.

- <span class="step">Step 0: Prepare your corpus:</span> Prepare your corpus as a CSV, XLSX or parquet file. [More information here](XXX)
- <span class="step">Step 1: Create your project:</span> On the [Project Creation page](../functionalities/project-creation.md), give the project a name, upload the data file and enter the columns you require for the annotation (ID, text, contextual). Set the number of elements in the train set to the size of your dataset. You may consider setting [secondary parameters](../functionalities/project-creation.md#secondary-parameters).
- <span class="step">Step 2: Give your collaborators access to your project:</span> Go to the [Users page](../functionalities/monitoring-account-and-users.md) and give your collaborators the right to access and annotate text inputs from your project.
- <span class="step">Step 3: Create your scheme and write down your codebook:</span> On the [Codebook page](../functionalities/codebook.md), create a scheme that fits your study (multiclass, multilabel or span — [more info on the available schemes](XXX)) and start writing the instructions for labelling the corpus. All users can see the schemes, labels and codebook; however, only managers and contributors can edit them.
- <span class="step">Step 4: Start annotating your corpus:</span> Go to the [Annotate page](../functionalities/annotate.md) and start the annoation process. You can:
  - Add a label to a text input (<span class="action primary">LABEL</span>), remove a label (<span class="action primary">No tag</span>), or move forward (<span class="action primary">Skip</span>).
  - Add a comment to your annotation.
  - Choose which text inputs to annotate or the order in which you wish to see them ([more info](../functionalities/annotate.md#selecting-text-inputs-to-annotate)).
- <span class="step">Step 5: Curate the annotation (Only available to projects with more than one user):</span> On the [Annotate page](../functionalities/annotate.md), choose ["Curate"](../functionalities/annotate.md#curate). You will be able to see annotations differences between schemes or between users and choose which annotation to keep as well as agreement metrics.
- <span class="step">Step 5: Export your annotated corpus:</span> On the [Export page](../functionalities/export.md), choose ["Annotations"](../functionalities/export.md#annotations) and click <span class="action primary">All annotations/schemes</span> to download your corpus as a CSV file, or XLSX or parquet.

Of course the reality is much less linear, you may want to move back and forth between step 3, step 4 and step 5 to refine your codebook and annotate accordingly. Also you may want to use exploration tools (see below for more insights), or use machine learning to find the most challenging text inputs and test your codebook on edge cases.

## Accelerate annotation with Active learning

## Explore your data
