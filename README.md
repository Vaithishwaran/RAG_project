RAG Question Answering using LangChain, FAISS, Sentence Transformers and Qwen

This project implements a simple Retrieval-Augmented Generation (RAG) system that retrieves relevant information from a custom text document and uses the Qwen language model to generate answers.

1)Document Input:
The project takes a text file as the knowledge source. For example, sam_file_AI.txt contains information that can be queried by the user.

2)Document Loading:
The project uses LangChain's TextLoader to load the text document into the application.

3)Text Splitting:
The loaded document is divided into smaller chunks using RecursiveCharacterTextSplitter.

4)The project uses:

chunk_size = 300

chunk_overlap = 50

5)Text Embeddings:

Each document chunk is converted into a numerical vector using the Sentence Transformers model:

sentence-transformers/all-MiniLM-L6-v2

6)Vector Database:

The generated embeddings are stored in a FAISS vector database. FAISS is used for efficient similarity search.

7)User Question:

The user provides a question related to the information available in the knowledge base.

For example:

What is Vaithi's age?

8)Similarity Search:

The user's question is converted into an embedding and compared with the stored document embeddings.
Document Retrieval:

FAISS retrieves the most relevant document chunks related to the user's question.

9)Context Creation:

The retrieved document chunks are combined to create the context that will be provided to the language model.

10)Prompt Generation:

A prompt is created containing the retrieved context and the user's question.

The model is instructed to use only the provided context:

You are an AI assistant. Use ONLY the provided context to answer.
If the answer is not in the context, say "I don't know".

11)Large Language Model:

The project uses the Qwen instruction-tuned language model:

Qwen/Qwen2.5-1.5B-Instruct

The model generates the final answer using the retrieved context.

12)Answer Generation:

The generated response is returned to the user based on the information retrieved from the knowledge base.

13)Context-Based Answering:

The system is designed to answer questions using the provided document context rather than relying only on the model's pretrained knowledge.

Unknown Information:

If the requested information is not available in the retrieved context, the model is instructed to respond:

I don't know

14)Generated Output:

For example, if sam_file_AI.txt contains:

Name: Vaithi
Age: 25
Location: Chennai

and the user asks:

What is Vaithi's age?

The system can generate:

Vaithi is 25 years old.

15)Main Technologies:

Python – Core programming language

LangChain – Used for document loading, text splitting, embeddings, retrieval, and LLM integration

FAISS – Vector database used for similarity search and document retrieval

Sentence Transformers – Used to generate text embeddings

Hugging Face Transformers – Used to load and run the language model

Qwen 2.5 – Instruction-tuned language model used for answer generation

16)Models Used:

Embedding Model

sentence-transformers/all-MiniLM-L6-v2

Language Model

Qwen/Qwen2.5-1.5B-Instruct

Installation:

Install the required Python packages:

pip install langchain langchain-community langchain-text-splitters faiss-cpu sentence-transformers huggingface-hub transformers torch


17)overall process:

Place the knowledge file inside the data folder:
data/sam_file_AI.txt

Enter a question in the prompt.eg:Ask a question: What is Vaithi's age?

Then run:
python rag_app.py

The system retrieves the relevant information and generates the answer using Qwen.
