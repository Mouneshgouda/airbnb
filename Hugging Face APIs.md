## 2. Hugging Face APIs (Inference API)

Hugging Face is a hub for open-source AI models and tools. Their **Inference API** allows you to easily use thousands of models hosted on their platform without setting up your own infrastructure.

---

### Authentication

#### Sign Up & Get API Token:

1. Go to [Hugging Face Hub](https://huggingface.co).
2. Create an account.
3. Navigate to your **profile settings** → **Access Tokens**.
4. Generate a new token with at least **"read" access** (for inference).

---

### Example of a Hugging Face API Token in a Python Environment Variable

```python
import os

HUGGINGFACE_API_TOKEN = os.getenv("HUGGINGFACE_API_TOKEN")
```

---

### Pricing

Hugging Face offers a **Free Inference API** tier, which is great for testing and hobby projects but may have **rate limits** and **slower performance**.

For production use and **dedicated resources**, they offer **Inference Endpoints**. Pricing depends on:

- **GPU/CPU instance type**: The compute power required.
- **Uptime**: How long your endpoint is active.
- **Traffic**: Number of requests made.

> 🔗 Check the [Hugging Face Inference Endpoints Pricing](https://huggingface.co/inference-endpoints/pricing) for current details.

---

### JSON Input/Output (Example: Text Generation)

You can use the `requests` library in Python to interact with the Hugging Face Inference API for a variety of tasks, such as text generation.

**Example Application: Text Generation with a Specific Model**

```python
import requests
import os

API_URL = "https://api-inference.huggingface.co/models/gpt2"
headers = {
    "Authorization": f"Bearer {os.getenv('HUGGINGFACE_API_TOKEN')}"
}

def query(payload):
    response = requests.post(API_URL, headers=headers, json=payload)
    return response.json()

output = query({
    "inputs": "Once upon a time, in a land far away,",
})

print(output)
```

This example sends a prompt to the `gpt2` model and prints the generated output.

---

## Summary

| Aspect           | Description                                                                 |
|------------------|-----------------------------------------------------------------------------|
| API Provider     | Hugging Face                                                                |
| Authentication   | Requires API token with read access                                         |
| Pricing          | Free tier available; production usage requires Inference Endpoints          |
| JSON I/O         | Request/response handled via JSON using the `requests` library              |
| Example          | Python-based text generation using GPT-2 model via Inference API            |

---

*Hugging Face makes it easy to experiment with and deploy open-source models for tasks like text generation, translation, classification, and more—all accessible through simple APIs.*
