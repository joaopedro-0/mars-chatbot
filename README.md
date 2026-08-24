# Mars ChatBot 

A simple **RAG (Retrieval-Augmented Generation) chatbot** that lets you upload a PDF and ask questions about its content. Built with **Streamlit**, **LangChain**, and **Google's Gemini API**.

This project was built while studying a GenerativeAI course on Udemy (provided through TCS), originally taught using the OpenAI API. It was adapted here to use Google Gemini's free tier instead.

## Features

- Upload any PDF and extract its text
- Splits the document into chunks for better context retrieval
- Generates embeddings and stores them in a FAISS vector database
- Ask natural language questions and get answers grounded in the document
- Powered by Gemini's embedding and chat models

## Tech Stack

- [Streamlit](https://streamlit.io/) — web interface
- [LangChain](https://www.langchain.com/) — orchestration (retriever, prompt, chain)
- [Google Gemini API](https://ai.google.dev/) — embeddings + chat model
- [FAISS](https://github.com/facebookresearch/faiss) — vector similarity search
- [pdfplumber](https://github.com/jsvine/pdfplumber) — PDF text extraction

## How It Works

1. The user uploads a PDF file.
2. The text is extracted and split into overlapping chunks.
3. Each chunk is converted into a vector embedding using Gemini's embedding model.
4. The embeddings are stored in a FAISS vector store.
5. When the user asks a question, the most relevant chunks are retrieved (MMR search) and passed as context to the Gemini chat model.
6. The model generates an answer based only on the retrieved context.

## Setup

**1. Clone the repository**
```bash
git clone [https://github.com/joaopedro-0/mars-chatbot.git](https://github.com/joaopedro-0/mars-chatbot.git)
cd mars-chatbot
```

**2. Create and activate a virtual environment**
```bash
python -m venv .venv
.venv\Scripts\activate      # Windows
source .venv/bin/activate   # macOS/Linux
```

**3. Install dependencies**
```bash
pip install -r requirements.txt
```

**4. Configure your API key**

Copy `.env.example` to `.env` and add your own Gemini API key (get one for free at [Google AI Studio](https://aistudio.google.com/apikey)):
```
GOOGLE_API_KEY=your_key_here
```

**5. Run the app**
```bash
streamlit run "chatbot_mars.py"
```

## Notes

- Google's embedding/chat model names change fairly often. If you get a `404 NOT_FOUND` error, check which models are currently available for your API key:
```python
import google.generativeai as genai
genai.configure(api_key="your_key_here")
for m in genai.list_models():
    print(m.name)
```

## License

This project is for educational purposes as part of a Udemy course exercise.
