# RAG Q&A Application

This repository contains the implementation of a Retrieval Augmented Generation (RAG) Q&A application. The application utilizes LangChain, Chroma, and Google Generative AI to answer questions based on specific source information.

## Table of Contents

- [Introduction](#introduction)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Architecture](#architecture)
- [Contributing](#contributing)
- [License](#license)

## Introduction

The RAG Q&A application is a sophisticated question-answering chatbot that leverages Retrieval Augmented Generation. It retrieves relevant documents based on a query and then generates an answer using a language model. This approach combines the strengths of information retrieval and generative models to provide accurate and contextually relevant answers.

The application takes data from a URL and then answers queries based on that. It first loads the document ,splits into chunks,these chunks are then embedded and stored in a vector store. The embedding is done using huggingface inference API and the vectorstore used is chroma. 
The app then takes a user question, searches for documents relevant to that question, passes the retrieved documents and initial question to a model, and returns an answer.

## Requirements

- Python 3.8+
- `bs4`
- `langchain_community`
- `langchain_text_splitters`
- `dotenv`
- `langchain_chroma`
- `langchain_google_genai`
- `google-generativeai`

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/rag-qa-app.git
   cd rag-qa-app
   ```

2. Create a virtual environment and activate it:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
   ```

3. Install the required packages:
   ```bash
   pip install -r requirements.txt
   ```

4. Set up your environment variables:
   - Create a `.env` file in the root directory.
   - Add your Hugging Face and Google Cloud API keys to the `.env` file:
     ```
     HF_API_KEY=your_hugging_face_api_key
     GCP_API_KEY=your_google_cloud_api_key
     ```

## Usage

1. Run the script:
   ```bash
   python main.py
   ```

2. The application will load documents, split them into manageable chunks, and store them in a vector store.

3. The script will then retrieve relevant documents based on the query and generate an answer using the Google Generative AI model.

## Architecture

1. **Document Loading**: The application uses `WebBaseLoader` from `langchain_community` to load documents from a specified URL. BeautifulSoup is used to parse specific parts of the web page.

2. **Text Splitting**: The `RecursiveCharacterTextSplitter` splits the documents into smaller chunks to make them more manageable for embedding and retrieval.

3. **Embedding and Vector Store**: Documents are embedded using the `HuggingFaceInferenceAPIEmbeddings` and stored in a Chroma vector store.

4. **Retrieval**: The `vectorstore.as_retriever` method is used to retrieve the most similar documents based on the query.

5. **Generation**: The retrieved documents are passed to the Google Generative AI model to generate the final answer.

6. **Chaining**: The retrieval and generation steps are chained together using LangChain to form a cohesive RAG pipeline.

