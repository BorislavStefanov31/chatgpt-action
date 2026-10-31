# Generate text with OpenAI LLMs Action

This action sends a message to the OpenAI model of your choice using the [Responses API](https://developers.openai.com/api/reference/resources/responses/methods/create).

## Inputs

### `openai_api_key`

**Required** The OpenAI API key.

### `message`

**Required** The message to send to the model.

### `instructions`

**Optional** System/developer instructions that guide the model's behaviour.

### `model`

**Optional** The model to use. Default is `gpt-6.1-sol`.

| Model | Best for |
| --- | --- |
| `gpt-6-astra` | Most capable; complex reasoning and coding |
| `gpt-6.1-sol` | Balance of intelligence and cost (default) |
| `gpt-6.1-terra` | Fast and efficient; visual reasoning and computer use |
| `gpt-6-luna` | Cheapest; focused, high-volume tasks |

See the [OpenAI models page](https://developers.openai.com/api/docs/models) for the full list.

### `reasoning_effort`

**Optional** How much the model reasons before answering: `none`, `low`, `medium`, `high`, `xhigh` or `max`. Supported values vary by model (for example `gpt-6-astra` and `gpt-6.1-sol` do not support `none`). Empty uses the model default.

### `temperature`

**Optional** Sampling temperature. Omitted by default, because many reasoning models reject it.

### `max_output_tokens`

**Optional** Upper bound on generated tokens, including reasoning tokens.

## Outputs

### `response_message`

The text returned by the model.

### `response_id`

The ID of the OpenAI response.

## Example usage

```yaml
name: Chat with Chat-GPT

on:
  push:
    branches:
      - main

jobs:
  chat:
    runs-on: ubuntu-latest

    steps:
    - name: Use chat-with-gpt-action
      id: chat
      uses: BorislavStefanov31/chatgpt-action@v2
      with:
        openai_api_key: ${{ secrets.OPENAI_API_KEY }}
        message: 'Say this is a test!'
        instructions: 'Answer in one short sentence.'
        model: 'gpt-6.1-sol'
        reasoning_effort: 'low'

    - name: Output GPT Response
      env:
        RESPONSE: ${{ steps.chat.outputs.response_message }}
      run: echo "$RESPONSE"
```
