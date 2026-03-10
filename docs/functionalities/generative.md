# Generative page

!!! warning

    This is an experimental page, dedicated to explore the use of external generative models. Some features can evolve rapidely.

The panel allows to use external generative models to annotate or extract information with prompts. The general idea is to run a prompt for a sample of the text and get the results. Each run is caracterized by a `batch ` id.

Each LLM model is running on external servers : it is up to the user to check its parameters and the level of security for the server involved.

## Add new model

<a class="action primary">Create new model</a> allows to create a new model for the project (shared by all users).

The main point is to identify where the model is available : which API is used ?

!!! info

    Several of them are based on [OpenAI API](https://developers.openai.com/api/reference/overview/) : OpenAI, OpenRouter. [Ollama](https://ollama.com/) runs quantized models and can be installed locally.

    [Ilaas](https://www.ilaas.fr/) is a french federation providing models for inference

    HuggingFace is a french plateform for open source models that can also host LLM

- <a class="parameter">API</a>: The type of API that serves the model. 
    - <a class="parameter">Endpoint</a>: Some API needs to specify the endpoint
- <a class="parameter">Model</a>: The model  to call from the API
    - *Available models are specific for each API
- <a class="parameter">API Credentials</a>: Authentification token (specific for the API)
- <a class="parameter">Name</a>: The name of the model


## Configure and run a generation

Select a model

Define the sample of elements you want to send with the prompt

- <a class="parameter">Elements</a>: Number of elements to send
- <a class="parameter">From</a>: Dataset

Select or save a prompt

- <a class="parameter">Saved prompts</a>: Prompt the user saved
- <a class="parameter">ICON</a>: Save current prompt
- <a class="parameter">ICON</a>: Delete selected prompt

Enter a prompt : plain text for the prompt to send to the generative model. You can add elements from the dataset : `[[TEXT]]` for the text, and `[[CONTEXT-VARIABLE]]` for each contextual variable.

<a class="action primary">Generate</a> Launch the generation process

## Results

Once a generation processed finished, generated data is display in the table.


- <a class="action secondary">Download all</a> Launch the generation process
- <a class="action secondary">Clear all</a> Launch the generation process

*Add treatment for the generated columns* allows to select filters to clean the generated texte before downloading it.




