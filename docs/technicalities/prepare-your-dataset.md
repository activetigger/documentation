
## Note on preparing your input dataset 

The input dataset should be a CSV, Parquet, or XLSX file. The text columns must be well prepared and curated before upload as <span class="highlight">ActiveTigger does not propose any text treatment option</span>. The only text manipulations implemented is the concatenation of text columns. Cleaning you dataset can include, but is not limited to the following: 

- Removing semanticless characters (html tags, encoding artefacts, emojis[^note-emoji], ...).
- Removing any duplicates.
- Splitting texts at the sentence/paragraph level.
- Ensuring all inputs are written in a single language (depending on the task).

!!! Note "Size of the texts"
    If you use models, please mind that they have a limited context windows. It means that if text exceed this windows (depending of the model, from an hundred to thousand words), it will be truncated.

[^note-emoji]: Depending on your task you may want to keep them because they carry significant information, or remove them because they will act as noise. Also, models may not have been trained on emojis, meaning that they will be replaced by `[unk]` tokens, adding noise to your text inputs.

We also encourage users to <span class="highlight">carefully set up their ID column</span> as they will ease the process of aggregating the annotations with external metadata for downsteam analysis.

!!! Note "Troubleshoot using Parquet files"
    If you upload a parquet file, you can encounter issues related to the format of your parquet file. Easy fix includes: 

    - Make sure that data contained is formatted as a string.
    - Make sure to not have nested columns (columns and sub-columns).