   ⚙️ How It Works
1. User asks a question in the chat page (templates/chat.html).
2. The browser sends the question to the Flask server with a POST request to the /get route.
3. The server converts the question into embeddings (numerical form) using a Hugging Face embedding model. This is the "Loading     weights" step you see when the app starts
4. The app **searches the knowledge base** for the passages most relevant to the question.
5. The relevant passages and the question are placed into a **prompt template** (`src/prompt.py`).
6. The **language model** reads the prompt and writes the answer.
7. The answer is **sent back to the browser** and shown in the chat window.

```
User Question
     │
     ▼
 Chat Page (HTML/CSS)
     │  POST /get
     ▼
 Flask Server (app.py)
     │
     ├──► Embedding Model ──► Knowledge Base Search
     │                              │
     │◄──────── relevant context ◄──┘
     ▼
 Prompt + Context ──► Language Model ──► Answer
     │
     ▼
 Answer shown in Chat Page
```

## 🛠️ Tech Stack

| Part | Technology |
|------|-----------|
| Language | Python 3.12 |
| Web framework | Flask |
| Frontend | HTML, CSS (and JavaScript in the chat page) |
| Embeddings | Hugging Face embedding model |
| Language model | Large Language Model via API *(add the one you use, e.g. OpenAI / Gemini / Groq)* |
| Vector database | *(add the one you use, e.g. Pinecone / FAISS / Chroma)* |
| Config | python-dotenv (`.env` file) |
| Version control | Git and GitHub |

> ✏️ **Please edit the table above** to match the exact model and database used in your code.

## 📁 Project Structure

```
MEDICAL-CHATBOT/
│
├── app.py                # Main Flask application (routes and chatbot logic)
│
├── src/                  # Helper code used by the app
│   ├── __init__.py       # Makes "src" a Python package
│   ├── helper.py         # Helper functions (data loading, embeddings, etc.)
│   └── prompt.py         # Prompt template given to the language model
│
├── templates/
│   └── chat.html         # Chat page shown in the browser
│
├── static/
│   └── style.css         # Styling for the chat page
│
├── research/             # Notebooks / experiments used while building the project
│
├── .env                  # Secret API keys (NOT uploaded to GitHub)
├── .gitignore            # Files Git should ignore
├── requirements.txt      # Python libraries needed to run the project
└── README.md             # Project documentation (this file)
```
## ✅ Prerequisites

Before you start, make sure you have:

- **Python 3.10 or higher** (the project was run with Python 3.12)
- **pip** (comes with Python)
- **Git** – [download here](https://git-scm.com/download/win)
- API key(s) for the services the project uses (language model and vector database, if any)
- An internet connection (needed the first time to download the embedding model)

## 🚀 Installation and Setup

### 1. Clone the repository

```bash
git clone https://github.com/Ritima07/MEDICAL-CHATBOT.git
cd MEDICAL-CHATBOT
```

### 2. Create a virtual environment (recommended)

```bash
python -m venv venv
```

Activate it:

- **Windows (PowerShell):**
  ```bash
  venv\Scripts\Activate.ps1
  ```
- **Windows (cmd):**
  ```bash
  venv\Scripts\activate
  ```
- **Mac / Linux:**
  ```bash
  source venv/bin/activate
  ```

### 3. Install the requirements

```bash
pip install -r requirements.txt
```

### 4. Create your `.env` file

In the main project folder, create a file named `.env` and add your keys (see the next section).

## 🔑 Environment Variables

Create a file called `.env` in the root folder with content like this:

```
API_KEY_FOR_YOUR_LLM=your_key_here
VECTOR_DB_API_KEY=your_key_here
HF_TOKEN=your_huggingface_token_here
```

> ✏️ Replace the names above with the **exact variable names used in your `app.py`**.

| Variable | Purpose |
|----------|---------|
| Language model key | Lets the app call the AI model to write answers |
| Vector database key | Lets the app search the medical knowledge base *(if used)* |
| `HF_TOKEN` | *(Optional)* Removes the Hugging Face warning about unauthenticated requests and gives faster model downloads |

**Never share your `.env` file or upload it to GitHub.**

## ▶️ Running the App

From the project folder, run:

```bash
python app.py
```

When the app starts you will see something like:

```
* Running on http://127.0.0.1:8080
* Running on http://192.168.x.x:8080
Press CTRL+C to quit
```

Open your browser and go to:

**http://127.0.0.1:8080**
💡
To stop the app, go back to the terminal and press **Ctrl + C**.

> The first start can take a little longer because the embedding model is loaded ("Loading weights"). Later starts are faster.


## 🔮 Future Improvements

- 🌐 Deploy the app online (Render, AWS, Hugging Face Spaces, etc.)
- 💾 Save chat history for each user
- 🗣️ Add voice input and voice output
- 🌍 Support multiple languages
- 📎 Show the source of each answer
- 🚨 Detect emergency symptoms and show a safety message
- 🎨 Improve the design and add a dark mode
- 📱 Make the layout fully mobile friendly

## 👩‍💻 Author

**Ritima Kumari**
GitHub: [@Ritima07](https://github.com/Ritima07)

---

⭐ If you found this project helpful, please give it a star on GitHub!# 🩺 Medical Chatbot

A web-based medical question-answering chatbot built with **Python** and **Flask**. Users type a health-related question into a chat page, and the app returns an answer generated from a medical knowledge source using an AI language model (Retrieval-Augmented Generation, or RAG).

> ⚠️ **Disclaimer:** This chatbot is for educational and informational purposes only. It is **not** a substitute for professional medical advice, diagnosis, or treatment. Always consult a qualified doctor for medical concerns.
