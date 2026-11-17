# 01 — Document Loading

`01_documents_loading.ipynb` is the first notebook in the **CompleteRAG** series. It covers how a RAG pipeline takes in raw data: wrapping text in LangChain `Document` objects and loading files with LangChain document loaders.

## What it covers

1. **Stack overview.** The planned components for the RAG pipeline:
   - **LLM:** Groq (needs an API key)
   - **Vector store:** Qdrant, with in-memory options such as FAISS and Chroma
   - **Embeddings:** Google, Hugging Face or Cohere
2. **The `Document` object.** Builds a `langchain_core.documents.Document` by hand to show its two fields:
   - `page_content`: the text itself
   - `metadata`: a dict describing the text (page number, source file, author, total pages, user ID). Metadata is used later for filtering and citing sources.
3. **Text file loading.** Uses `TextLoader` from `langchain_community` to read a `.txt` file into a list of `Document` objects, then checks how many came back.

## Setup

From the project root:

```bash
python -m venv ragEnv
source ragEnv/bin/activate
pip install -r requirements.txt
```

Create a `.env` file in the project root with your API keys (for example `GROQ_API_KEY=...`). Keep it out of version control.

## Running the notebook

1. Open `notebooks/01_documents_loading.ipynb` in Jupyter or VS Code and select the `ragEnv` kernel.
2. Put a `sample.txt` file in the `notebooks/` folder. `TextLoader("sample.txt")` resolves the path relative to the notebook's working directory.
3. Run the cells from top to bottom.

The `pip install` cells for `langchain-community` and `beautifulsoup4` are only needed if you skipped `requirements.txt`.

## Key takeaways

- Every loader in LangChain returns a `list[Document]`.
- Good metadata now makes filtering, citation and multi-user separation possible later in the pipeline.
- `TextLoader` returns one `Document` per file. PDF loaders (`pypdf`, `pymupdf`, both in `requirements.txt`) usually return one per page.

## Next steps

Later notebooks will cover more loaders (PDF, web via BeautifulSoup), text splitting, embeddings, vector storage in Qdrant, and retrieval plus generation with Groq.
