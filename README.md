# Generate text with OpenAI LLMs Action

This action sends a message to llm by your choice using the OpenAI API.

## Inputs

### `openai_api_key`

**Required** The OpenAI API key.

### `message`

**Required** The message to send to GPT.

### `temperature`

**Optional** The temperature for the GPT model. Default is `0.7`.

### `model`

**Optional** The GPT model to use. Default is `gpt-4o`.

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
    - name: Checkout Repository
      uses: actions/checkout@v2

    - name: Use chat-with-gpt-action
      id: chat
      uses: BorislavStefanov31/chatgpt-action@v1.0.0
      with:
        openai_api_key: ${{ secrets.OPENAI_API_KEY }}
        message: 'Say this is a test!'
        temperature: 0.7
        model: 'gpt-4o'

    - name: Output GPT Response
      run: echo "${{ steps.chat.outputs.response_message }}"
