# 🎬 Movie Q&A Bot — RAG Powered by OpenRouter

A smart, Retrieval-Augmented Generation (RAG) based chatbot that answers natural language questions about movies using real movie data from the [TMDB 5000 Movie Dataset](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata). Built using Chroma for vector search and OpenRouter for flexible LLM access (GPT-4, Mixtral, Claude, etc.).

---

## 🚀 Features

- 🔍 **Retrieval-Augmented Generation (RAG)**: Answers are based on actual context retrieved from movie metadata.
- 🧠 **Semantic Search**: Uses sentence-transformer embeddings + ChromaDB for vector similarity.
- 🌐 **Model Agnostic via OpenRouter**: Swap between GPT-4, Mixtral, Claude, LLaMA, and more with one config.
- 🎥 **Real Movie Data**: Extracted from `tmdb_5000_movies.csv` and `tmdb_5000_credits.csv`.

---

## 📂 Dataset

This project uses:

- `tmdb_5000_movies.csv`: Movie metadata like title, genres, overview, etc.
- `tmdb_5000_credits.csv`: Cast and crew info.

> 📌 [Download from Kaggle](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata)

---

## ⚙️ How It Works

1. **Data Merging & Cleaning**: Merges credits + metadata into a unified movie document.
2. **Chunking**: Converts each movie into a text chunk for embedding (title, overview, director, cast, etc.).
3. **Embedding**: Uses `all-MiniLM-L6-v2` via `sentence-transformers` to generate vector representations.
4. **Vector DB**: Stores all chunks in a local Chroma vector database.
5. **Query Flow**:
    - User asks a question
    - Relevant chunks are retrieved from Chroma using cosine similarity
    - The question + retrieved context is sent to OpenRouter for final answer generation

---

## 🧪 Example Usage

```python
query = "Who directed Interstellar?"

response = ask_movie_bot(query)

print(response)
# Output: "Interstellar was directed by Christopher Nolan."
