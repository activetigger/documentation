# Generative page

!!! warning

    This is an experimental page, dedicated to explore the use of external generative models. Some features can evolve rapidely.

The panel allows to use external generative models to annotate or extract information with prompts. The general idea is to run a prompt for a sample of the text and get the results. Each run is caracterized by a `batch ` id.

Each LLM model is running on external servers : it is up to the user to check its parameters and the level of security for the server involved.

## Add new model

<span class="action primary">Create new model</span> allows to create a new model for the project (shared by all users).

The main point to configure a model is to have access to an API. Usually, this involve to know the endpoint and

!!! info

    Several of them are based on [OpenAI API](https://developers.openai.com/api/reference/overview/) : OpenAI, OpenRouter. [Ollama](https://ollama.com/) runs quantized models and can be installed locally.

    [Ilaas](https://www.ilaas.fr/) is a french federation providing models for inference

    HuggingFace is a french plateform for open source models that can also host LLM

- <span class="parameter">API</span>: The type of API that serves the model. 
    - <span class="parameter">Endpoint</span>: Some API needs to specify the endpoint
- <span class="parameter">Model</span>: The model  to call from the API
    - *Available models are specific for each API
- <span class="parameter">API Credentials</span>: Authentification token (specific for the API)
- <span class="parameter">Name</span>: The name of the model


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

Once a generation processed finished, generated data is display in the table.


- <span class="action secondary">Download all</span> Launch the generation process
- <span class="action secondary">Clear all</span> Launch the generation process

*Add treatment for the generated columns* allows to select filters to clean the generated texte before downloading it.




