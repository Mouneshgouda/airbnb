# Working with GenAI APIs

Interacting with Generative AI models often involves using their APIs (Application Programming Interfaces). These APIs allow developers to send prompts or data to the AI model and receive generated content (text, images, code, etc.) programmatically.

---

## Key Aspects of Working with GenAI APIs

### 1. Choosing an API Provider

- **OpenAI**: Known for powerful models like GPT (text generation), DALL·E (image generation), and Whisper (speech-to-text).
- **Hugging Face**: Offers a vast ecosystem of open-source models and a platform (Hugging Face Hub and Inference API) for deploying and using many different models.

---

### 2. Authentication

To ensure secure and authorized access, you'll need an **API key**. This key identifies you and links your requests to your account for billing and usage tracking.

---

### 3. Pricing

GenAI APIs are typically not free for extensive use. Pricing models vary but often depend on factors like:

- **Tokens**: For text models, this refers to the number of words or sub-word units processed (both input prompt and generated output).
- **Image resolution/quality**: For image generation.
- **Model size/complexity**: More powerful models usually cost more.
- **API calls**: Sometimes a per-request fee.

---

### 4. JSON Input/Output

Most web APIs, including GenAI APIs, use **JSON (JavaScript Object Notation)** for sending requests and receiving responses. It's a lightweight, human-readable data interchange format.

---

## 1. OpenAI API

OpenAI provides a robust API for accessing their state-of-the-art models.

---

### Authentication

#### Sign Up & Get API Key:

1. Go to the [OpenAI website](https://platform.openai.com).
2. Create an account.
3. Navigate to your **API keys** section (usually under "API Keys" in your profile settings).
4. Generate a new secret key.

> ⚠️ **Important**: Keep this key secure and **never expose it in client-side code**.

---

### Example of an OpenAI API Key in a Python Environment Variable

```python
import os

# It's best practice to store your API key as an environment variable
# For local testing, you might load it from a .env file or directly assign (not recommended for production)

OPENAI_API_KEY = os.getenv("OPENAI_API_KEY")
```

---

### Pricing

OpenAI's pricing is primarily based on **tokens** for language models (input + output). DALL·E is priced per image generated.

Check the official [OpenAI pricing page](https://openai.com/pricing) for the most up-to-date details.

**Example:**

- GPT-3.5-turbo might be priced at:
  - `$0.0015 / 1K tokens` for input
  - `$0.002 / 1K tokens` for output

So a prompt of 500 tokens and a response of 500 tokens would cost:

```
(0.5 * $0.0015) + (0.5 * $0.002) = $0.00075 + $0.001 = $0.00175
```

---

### JSON Input/Output (Chat Completions Example)

Let's see a Python example using the `openai` library to build a simple chatbot.

```python
import openai
import os

# Load API key securely
openai.api_key = os.getenv("OPENAI_API_KEY")

# Create a simple chat completion
response = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "What's the weather like in Paris today?"}
    ]
)

# Print the assistant's reply
print(response['choices'][0]['message']['content'])
```

---

## Summary

| Aspect           | Description                                                                 |
|------------------|-----------------------------------------------------------------------------|
| API Providers    | OpenAI, Hugging Face                                                        |
| Authentication   | Requires secure API key                                                     |
| Pricing          | Based on tokens, API calls, model type, or output resolution                |
| JSON I/O         | Most GenAI APIs use JSON for requests/responses                             |
| Example          | Python-based chatbot using OpenAI's `ChatCompletion` API                    |

---

*Understanding and working with GenAI APIs is essential for integrating powerful AI features into applications, whether for natural language, image generation, or speech processing.*
