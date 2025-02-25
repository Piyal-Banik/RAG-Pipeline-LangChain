# Retrieval-Augmented Generation (RAG) Pipeline Using FAISS and Falcon-7B

## Overview
This project implements a Retrieval-Augmented Generation (RAG) pipeline using LangChain, FAISS, and Falcon-7B. It extracts information from a Wikipedia page, processes it into a vector database, and enables a question-answering system using a retriever and a generative LLM.

## Project Workflow
1️⃣ **Download and Store Wikipedia Content**
- The script fetches the content of a Wikipedia page.
- The content is saved as a text file (sample.txt) for later processing.
2️⃣ **Load and Split Document**
- The document is loaded using LangChain's TextLoader.
- It is then split into smaller chunks using RecursiveCharacterTextSplitter (chunk size: 500, overlap: 50).
- Splitting ensures that the retrieval system works efficiently by handling smaller, meaningful text segments.

3️⃣ **Create FAISS Vector Store**
- Each text chunk is converted into a numerical vector representation using the MiniLM embedding model (sentence-transformers/all-MiniLM-L6-v2).
- FAISS is used as a vector database to store and retrieve similar text chunks based on user queries.
- The FAISS index is saved locally (faiss_index) for reuse

4️⃣ **Load Falcon-7B Language Model**
- The Falcon-7B Instruct model (tiiuae/falcon-7b-instruct) is used as the LLM to generate responses.
- The model is loaded with 4-bit quantization (BitsAndBytesConfig) to optimize memory usage.
- The HuggingFace Pipeline enables efficient text generation.

5️⃣ **Create Retrieval-Augmented Generation (RAG) Pipeline**
- A retrieval mechanism is created using FAISS to fetch relevant document chunks.
- A system prompt ensures that responses are contextually relevant and concise.
- The create_retrieval_chain function links:
    - Retriever (FAISS) → Finds relevant text chunks.
    - LLM (Falcon-7B) → Generates an answer based on the retrieved content.

6️⃣ **Query Processing**
- The system takes a user query (e.g., "What is Artificial Intelligence?").
- It retrieves relevant document chunks using FAISS.
- The LLM generates a response based on the retrieved information.
- The final answer is returned to the user.

## Key Technologies Used
- **LangChain** → Manages document processing, retrieval, and response generation.
- **FAISS** → Efficient vector storage and fast similarity search.
- **HuggingFace Transformers** → Embeddings & text generation (MiniLM, Falcon-7B).
- **BitsAndBytes Quantization** → Enables efficient inference on Falcon-7B.

## How to Run
Clone the repository:
```bash
git clone https://github.com/Piyal-Banik/RAG-Pipeline-LangChain.git

cd RAG-Pipeline-LangChain
```

Install dependencies:
```bash
pip install -r requirements.txt
```

**This project showcases how retrieval-based question answering can be efficiently implemented using FAISS and Falcon-7B, making it a scalable solution for knowledge-based AI applications.**