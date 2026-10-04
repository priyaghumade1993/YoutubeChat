# YoutubeChat
RAG Based YouTube Chat
# 🎥 YouTube Chat — RAG Based Question Answering System

A **Retrieval-Augmented Generation (RAG)** application that allows users to ask questions about a YouTube video's transcript.

The system retrieves relevant information from the video transcript and uses an LLM to generate an accurate answer based on the retrieved context.

---

## 🚀 Project Overview

This project demonstrates how to build a **RAG pipeline using LangChain LCEL**.

### How it works

```text
YouTube Video
      ↓
Transcript
      ↓
Document Creation
      ↓
Text Splitting
      ↓
Embeddings
      ↓
FAISS Vector Store
      ↓
Retriever
      ↓
Relevant Documents
      ↓
Context Formatting
      ↓
Prompt
      ↓
LLM
      ↓
Final Answer
```

---

## 🧠 Technologies Used

* Python
* LangChain
* LangChain Core
* OpenAI API
* OpenAI Embeddings
* FAISS
* YouTube Transcript
* LCEL (LangChain Expression Language)
* Python-dotenv

---

## 📁 Project Structure

```text
RAG -YoutubeChat/
│
├── Youtube_Chat.py
├── requirements.txt
├── .gitignore
├── README.md
│
├── ragenv/
└── faiss_index/
```

> `ragenv/`, `.env`, and generated vector-store files are excluded from Git using `.gitignore`.

---

## 🔑 Environment Variables

Create a `.env` file in the project root:

```env
OPENAI_API_KEY=your_openai_api_key
```

**Do not commit the `.env` file to GitHub.**

---

## 📦 Installation

### 1. Clone the repository

```bash
git clone https://github.com/your-username/youtube-chat-rag.git
```

### 2. Move into the project directory

```bash
cd "RAG -YoutubeChat"
```

### 3. Create a virtual environment

```bash
python -m venv ragenv
```

### 4. Activate the virtual environment

### Windows PowerShell

```powershell
.\ragenv\Scripts\Activate.ps1
```

### Windows CMD

```cmd
ragenv\Scripts\activate
```

---

## 📥 Install Dependencies

```bash
pip install -r requirements.txt
```

---

## ▶️ Run the Project

Run:

```bash
python Youtube_Chat.py
```

The application will process the YouTube transcript, create embeddings, retrieve relevant content, and generate an answer using the LLM.

---

## 🔄 RAG Pipeline

### 1. Load YouTube Transcript

The video's transcript is loaded and converted into documents.

### 2. Split Documents

Large transcript content is divided into smaller chunks using a text splitter.

### 3. Generate Embeddings

Each chunk is converted into a numerical vector using OpenAI embeddings.

### 4. Store Embeddings

The embeddings are stored in a FAISS vector store.

### 5. Retrieve Relevant Content

When the user asks a question, the retriever searches for the most relevant transcript chunks.

### 6. Format Context

The retrieved documents are combined into a single context.

### 7. Generate Answer

The context and user's question are passed to the LLM through a prompt.

### 8. Parse Output

`StrOutputParser` converts the LLM response into a clean string.

---

## 🔗 LangChain LCEL

The project uses **LangChain Expression Language (LCEL)** to build the RAG chain.

The main chain follows:

```text
Retriever
    ↓
Context Formatting
    ↓
RunnableParallel
    ↓
Prompt
    ↓
LLM
    ↓
StrOutputParser
    ↓
Final Answer
```

Example:

```python
main_chain = (
    parallel_chain
    | prompt
    | llm
    | parser
)
```

---

## 🧩 Main Components

### RunnableParallel

Runs multiple operations in parallel.

```python
parallel_chain = RunnableParallel({
    "context": retriever | RunnableLambda(format_docs),
    "question": RunnablePassthrough()
})
```

It creates:

```text
context  → Retrieved documents
question → Original user question
```

---

### RunnableLambda

Used to transform retrieved documents into a single context string.

```python
def format_docs(retrieved_docs):
    return "\n\n".join(
        doc.page_content
        for doc in retrieved_docs
    )
```

---

### RunnablePassthrough

Passes the original question without modifying it.

```python
"question": RunnablePassthrough()
```

---

### StrOutputParser

Converts the LLM output into a clean string.

```python
parser = StrOutputParser()
```

---

## 🎯 Example

### User Question

```text
What is the main topic discussed in the video?
```

### RAG System

```text
Question
   ↓
Retriever
   ↓
Relevant Transcript Chunks
   ↓
Prompt + Context
   ↓
LLM
   ↓
Answer
```

### Generated Answer

```text
The main topic of the video is ...
```

---

## 💡 Key Concepts Demonstrated

This project demonstrates practical knowledge of:

* RAG
* Embeddings
* Vector databases
* Semantic search
* Document chunking
* Retrievers
* Prompt engineering
* LLM integration
* LangChain
* LCEL
* RunnableParallel
* RunnableLambda
* RunnablePassthrough
* Output parsers
* FAISS
* YouTube transcript processing

---

## 🔐 Security

Never expose your API key in source code.

❌ Avoid:

```python
OPENAI_API_KEY = "sk-xxxxxxxx"
```

✅ Use `.env`:

```env
OPENAI_API_KEY=your_openai_api_key
```

and load it using:

```python
from dotenv import load_dotenv

load_dotenv()
```

---

## 📌 Future Improvements

Possible improvements include:

* Add Streamlit UI
* Support multiple YouTube videos
* Add conversation memory
* Add chat history
* Add source citations
* Add LangSmith tracing
* Add evaluation dataset
* Add hybrid search
* Add reranking
* Add streaming responses
* Deploy using Docker
* Deploy on AWS/Azure

---

## 👩‍💻 Author

**Priya Ghumade**

AI / Agentic AI Developer
Python | LangChain | LangGraph | RAG | LLMs

---

## ⭐ Project Purpose

This project was created as a practical implementation of **Retrieval-Augmented Generation using LangChain and LCEL**, with the goal of understanding how transcript data can be transformed into a searchable knowledge base and used to generate context-aware answers with an LLM.
