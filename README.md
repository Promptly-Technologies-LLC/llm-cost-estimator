# llm-cost-estimation

`llm-cost-estimation` is a Python library developed to aid in estimating the costs associated with Large Language Model (LLM) API calls.

## Key Features

- `models`: Contains essential details about various LLMs. This includes:
    - Cost per prompt token
    - Cost per completion token
    - Model description
    - Maximum tokens
- `count_token`: A utility function to count the tokens present in a specific prompt or chat history using a given model's encoding system.
- `estimate_costs`: A utility function to provide cost estimates for API calls to specified LLMs, based on:
    - Length of a text prompt
    - Average length of messages in a chat history

This open-source library aims to help developers predict and manage costs when integrating and working with LLMs.

## Using the `models` Object

The `models` object in the `llm-cost-estimation` library provides a list of dictionaries, each representing a different OpenAI model with key details such as costs per token, model description, maximum tokens, and more.

To use this `models` object, you should follow these steps:

1. Import the `models` object from the `llm-cost-estimation` library.

```python
from llm_cost_estimation import models
```

2. You can then access the models object which will display the details about the various models.

```python
for model in models:
    print(f'Model Name: {model["name"]}')
    print(f'Completion Cost Per Token: {model["completion_cost_per_token"]}')
    print(f'Prompt Cost Per Token: {model["prompt_cost_per_token"]}')
    print(f'Maximum Tokens: {model["max_tokens"]}')
    print(f'Description: {model["description"]}\n')
```

These steps will print the name, completion cost per token, prompt cost per token, maximum tokens, and a description for each model in the models object.

If you would like to view this data in a table format, you can use pandas. Here is an example:

```python
import pandas as pd

# Convert the list of dictionaries to a DataFrame
models_df = pd.DataFrame(models)

# Display the DataFrame
print(models_df)
```

This will display the information in a tabular format, with each row representing a different model and each column representing a different attribute of the model (name, completion cost per token, etc.).

## Using the `count_tokens` Function

The `count_tokens` function in the `llm-cost-estimation` library enables users to count the number of tokens in a string or list of chat messages using the encoding for a specified Large Language Model (LLM). It also provides an estimation for the number of tokens a completion might use, under the assumption that the completion will be of similar length to the input prompt or the average length of input messages.

Please note, this function utilizes the [tiktoken](https://github.com/openai/tiktoken) library, a Python library from OpenAI for counting the number of tokens in a text string without making an API call. For more information on how to count tokens in chat messages, you can refer to this [OpenAI Cookbook example](https://github.com/openai/openai-cookbook/blob/main/examples/How_to_count_tokens_with_tiktoken.ipynb).

Here's an example of how to use the `count_tokens` function:

```python
from llm_cost_estimation import count_tokens

text = "Hello, how are you?"
model = "gpt-4"

# Count tokens in the text
prompt_tokens, estimated_completion_tokens = count_tokens(text, model)

print(f"Number of tokens in the prompt: {prompt_tokens}")
print(f"Estimated number of tokens in the completion: {estimated_completion_tokens}")
```

In this code snippet:

- We import the `count_tokens` function from the `llm-cost-estimation` library.
- We define a text string and the model name.
- We call the `count_tokens` function with the text and the model name.
- Finally, we print the number of tokens in the prompt and the estimated number of tokens in the completion.

In the event you are working with a list of chat messages, the input should be formatted as follows:

``` python
chat_history = [{"role": "system", "content": "You are a helpful assistant."},
                {"role": "user", "content": "Who won the world series in 2020?"}]
                
prompt_tokens, estimated_completion_tokens = count_tokens(chat_history, model)
```

In this case, the function will calculate the number of tokens based on the structure of chat messages.

Remember to replace the sample code with your actual text or chat history and model where necessary.

## Using the `estimate_cost` Function

The `estimate_cost` function in the `llm-cost-estimation` library is a utility that can be used to calculate the cost of requesting a completion from a Large Language Model (LLM) given a specific input text or chat history. The function makes use of the token counting feature offered by the `count_tokens` function and computes the overall cost based on the number of tokens and the cost per token for the specified LLM.

Here's an example of how to use the `estimate_cost` function:

```python
from llm_cost_estimation import estimate_cost

prompt = "Hello, how are you?"
model = "gpt-4"

# Estimate the cost for the completion
estimated_cost = estimate_cost(prompt, model)

print(f"Estimated cost of this completion: {estimated_cost}")
```

In this code snippet:

- We import the `estimate_cost` function from the `llm_cost_estimation` library.
- We define a prompt string and the model name.
- We call the `estimate_cost` function with the prompt and the model name.
- Finally, we print the estimated cost of the completion.

In the case of a chat completion prompt, the input should be formatted as follows:

```python
chat_history = [{"role": "system", "content": "You are a helpful assistant."},
                {"role": "user", "content": "Who won the world series in 2020?"}]

# Estimate the cost for the completion
estimated_cost = estimate_cost(chat_history, model)
```

In this case, the function will calculate the cost based on the structure of chat messages. It's important to remember to replace the sample code with your actual prompt/chat history and model as necessary.