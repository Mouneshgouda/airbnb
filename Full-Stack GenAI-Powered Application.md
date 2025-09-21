# Full-Stack GenAI-Powered Application: AI Story Generator

A GenAI-powered application is a full-stack project where a user interacts with a frontend, which sends a request to a backend server, which then communicates with a GenAI API to generate a response.

---

## 📦 Components Overview

### 1. Frontend: User Interface (React)

The frontend is where the user interacts with the application.

#### Why React?

- Component-based architecture for modular UIs
- Efficient updates via Virtual DOM
- Great for handling dynamic, AI-generated content

#### What It Does

- Captures the user's input (story idea)
- Sends it to the backend via a POST request
- Displays the generated story returned from the backend

---

### 2. Backend: API Server (Flask)

The backend is responsible for securely handling API calls to OpenAI.

#### Why Flask?

- Lightweight and easy to set up
- Ideal for rapid prototyping and small applications
- Keeps API keys secure and hidden from frontend

#### What It Does

- Receives prompt from frontend
- Sends it to OpenAI’s API
- Receives the generated response
- Sends the story back to the frontend

---

### 3. GenAI API Integration (OpenAI)

The backend uses OpenAI’s API to generate content using models like `text-davinci-003`.

#### How It Works

- Flask sends a request to OpenAI’s API endpoint
- Includes prompt, model settings (max_tokens, temperature), and an Authorization header
- API returns generated text
- Flask processes and returns this text to the React frontend

---

## 🔁 Application Flow Diagram

```text
User (Browser)
   ↓
React Frontend (User Input)
   ↓
Flask Backend (API Request)
   ↓
OpenAI API (Text Generation)
   ↓
Flask Backend (Response)
   ↓
React Frontend (Display Story)
```

---

## 🛠️ Step-by-Step Guide

### 🔧 Step 1: Backend - Flask API

#### File: `app.py`

```python
from flask import Flask, request, jsonify
from flask_cors import CORS
import openai
import os

# Create Flask app
app = Flask(__name__)
CORS(app)

# Load your API key from an environment variable
openai.api_key = os.getenv("OPENAI_API_KEY")

@app.route('/api/generate_story', methods=['POST'])
def generate_story():
    data = request.get_json()
    prompt = data.get('prompt')

    if not prompt:
        return jsonify({"error": "No prompt provided"}), 400

    try:
        full_prompt = f"Write a short, creative story based on the following idea: '{prompt}'"

        response = openai.Completion.create(
            engine="text-davinci-003",
            prompt=full_prompt,
            max_tokens=250,
            temperature=0.7
        )

        story_text = response.choices[0].text.strip()
        return jsonify({"story": story_text})

    except Exception as e:
        return jsonify({"error": str(e)}), 500

if __name__ == '__main__':
    app.run(debug=True, port=5000)
```

#### 🧪 How to Run the Backend:

1. Install dependencies:

```bash
pip install Flask openai flask-cors
```

2. Set your API key:

```bash
export OPENAI_API_KEY='your_openai_api_key'
```

3. Run the server:

```bash
python app.py
```

---

### 🎨 Step 2: Frontend - React App

#### Create Project:

```bash
npx create-react-app ai-story-app
cd ai-story-app
```

#### Replace `src/App.js` with:

```jsx
import React, { useState } from 'react';
import './App.css';

function App() {
  const [prompt, setPrompt] = useState('');
  const [story, setStory] = useState('');
  const [loading, setLoading] = useState(false);

  const handleSubmit = async (e) => {
    e.preventDefault();
    setLoading(true);
    setStory('');

    try {
      const response = await fetch('http://localhost:5000/api/generate_story', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({ prompt }),
      });

      if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`);
      }

      const data = await response.json();
      setStory(data.story);
    } catch (error) {
      console.error("Failed to fetch story:", error);
      setStory("Failed to generate story. Please try again later.");
    } finally {
      setLoading(false);
    }
  };

  return (
    <div className="App">
      <header className="App-header">
        <h1>GenAI Story Generator 📝</h1>
        <form onSubmit={handleSubmit}>
          <textarea
            value={prompt}
            onChange={(e) => setPrompt(e.target.value)}
            placeholder="Start a story with a simple idea, like 'a robot who dreams of becoming a baker.'"
            rows="4"
            cols="50"
          />
          <button type="submit" disabled={loading || !prompt}>
            {loading ? 'Generating...' : 'Generate Story'}
          </button>
        </form>
        <div className="story-output">
          {story && (
            <>
              <h2>Your Story:</h2>
              <p>{story}</p>
            </>
          )}
        </div>
      </header>
    </div>
  );
}

export default App;
```

#### 🧪 How to Run the Frontend:

1. Navigate to the frontend directory:

```bash
cd ai-story-app
```

2. Start the React development server:

```bash
npm start
```

> Your React app will run on `http://localhost:3000` and will send requests to the Flask backend at `http://localhost:5000`.

---

## ✅ Summary

| Component | Technology | Description |
|----------|-------------|-------------|
| Frontend | React | Captures user input and displays story |
| Backend | Flask | Receives prompt, calls OpenAI API, returns response |
| GenAI API | OpenAI (text-davinci-003) | Generates a story based on user prompt |

---

## 📚 Final Notes

- This project can be extended with authentication, prompt templates, story-saving features, etc.
- You can also switch out the OpenAI API for other providers like Hugging Face or Cohere.
- Remember to **never expose your API keys** in frontend code.

---
*This example shows how you can build a full-stack AI application using modern technologies and a GenAI model to create interactive, dynamic user experiences.*
