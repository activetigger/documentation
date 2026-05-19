# Generative page

The panel allows to use external generative models to annotate or extract information with prompts.

!!! warning

    This is an experimental page, dedicated to exploring the use of external generative models. Some features can evolve rapidly.

The general idea is to run a prompt for a sample of the text and get the results. Each run is characterized by a `batch` id.

Each LLM model is running on external servers: it is up to the user to check its parameters and the level of security for the server involved.

## Add new model

<span class="action primary">Create new model</span> allows to create a new model for the project (shared by all users).

The main point to configure a model is to have access to an API. Usually, this involves knowing the endpoint and the credentials.

!!! info

    Several APIs are based on the [OpenAI API](https://developers.openai.com/api/reference/overview/): OpenAI, OpenRouter. [Ollama](https://ollama.com/) runs quantized models and can be installed locally.

    [Ilaas](https://www.ilaas.fr/) is a French federation providing models for inference.

    [HuggingFace](https://huggingface.co/) is a platform for open source models that can also host LLMs.

- <span class="parameter">API</span>: The type of API that serves the model. 
    - <span class="parameter">Endpoint</span>: Some APIs require specifying the endpoint.
- <span class="parameter">Model</span>: The model to call from the API.
    - *Available models are specific to each API.*
- <span class="parameter">API Credentials</span>: Authentication token (specific to the API).
- <span class="parameter">Name</span>: The name of the model.


## Configure and run a generation

Select a model

Define the sample of elements you want to send with the prompt

- <span class="parameter">Elements</span>: Number of elements to send
- <span class="parameter">From</span>: Dataset

Select or save a prompt

- <span class="parameter">Saved prompts</span>: Prompt the user saved
- <span class="parameter">ICON</span>: Save current prompt
- <span class="parameter">ICON</span>: Delete selected prompt

Enter a prompt : plain text for the prompt to send to the generative model. You can add elements from the dataset : `[[TEXT]]` for the text, and `[[CONTEXT-VARIABLE]]` for each contextual variable.

<span class="action primary">Generate</span> Launch the generation process

## Results

Once a generation process has finished, generated data is displayed in the table.


- <span class="action secondary">Download all</span> Download the generated data.
- <span class="action secondary">Clear all</span> Clear all generated data for the current project.

*Add treatment for the generated columns* allows you to select filters to clean the generated text before downloading it.




