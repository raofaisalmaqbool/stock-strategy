# Stock Strategy Chatbot

A small Flask web app that lets you ask natural-language questions about stock investors and tickers.
It looks up relevant rows in a MongoDB collection (for example, `screenertickers.investors`) and uses
OpenAI's Chat Completions API to generate an answer.

## Features

- Simple, modern chat UI.
- Flask backend with CSRF protection.
- MongoDB integration for investor/ticker data.
- OpenAI-powered answers that combine user input with your database content.

## Requirements

- Python 3.9+
- A running MongoDB instance with a `test` database and `screenertickers` collection.
- An OpenAI API key.

## Setup

1. (Optional) Create and activate a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. Create a `.env` file from the example and edit it:

```bash
cp .env.example .env
```

4. Ensure MongoDB is running and that `screenertickers` contains your data.

5. Run the app:

```bash
python app.py
```

The app will start on `http://127.0.0.1:5000` by default, or on the port specified via `PORT`.

## Environment variables

These are loaded from `.env` using `python-dotenv`:

- `OPENAI_API_KEY` – your OpenAI API key.
- `MONGO_URI` – MongoDB connection string, e.g. `mongodb://localhost:27017/test`.
- `OPENAI_MODEL` – (optional) chat model name (default: `gpt-4o`).
- `PORT` – (optional) port for the Flask dev server (default: `5000`).

## How it works

1. The frontend sends your question to the Flask backend as JSON.
2. The backend queries MongoDB for matching investor names in `screenertickers.investors.name`.
3. The matching records plus your question are passed to OpenAI's chat completion endpoint.
4. The generated answer is returned and rendered in the chat interface as a conversation.

You can customize the MongoDB query or the prompt text to better match your specific stock strategy or
research workflow.
