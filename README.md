# Learn Chroma

A minimal, opinionated starter for learning and experimenting with Chroma (vector DB) in small projects. Focuses on simple, reproducible examples and minimal dependencies.

## Goals
- Show core Chroma workflows (index, persist, query) with minimal code.
- Use a tiny, easy-to-understand project layout for learning and demos.
- Keep examples runnable locally.

## Features
- Tiny examples in Python.
- In-memory and on-disk persistence samples.
- Example with synthetic embeddings so you can run without external models.

## Quickstart (Python)

Prerequisites:
- Python 3.8+
- pip

Install (example):
```bash
python -m venv .venv
source .venv/bin/activate   # or .venv\Scripts\activate on Windows
pip install chromadb
```

Minimal usage:
```python
import chromadb
from chromadb.config import Settings
import numpy as np

# Use local in-process Chroma client (no server)
client = chromadb.Client(Settings())

# Create or get a collection
collection = client.create_collection("lean_example")

# Documents and synthetic embeddings
docs = ["apple", "banana", "orange"]
metas = [{"type": "fruit"}] * len(docs)
embeddings = [np.random.rand(128).tolist() for _ in docs]

# Upsert documents with embeddings
collection.upsert(
    documents=docs,
    metadatas=metas,
    embeddings=embeddings,
    ids=["d1", "d2", "d3"]
)

# Query
query_embedding = np.random.rand(128).tolist()
results = collection.query(query_embeddings=[query_embedding], n_results=2)
print(results)
```

Notes:
- Replace the synthetic embeddings with real model embeddings (OpenAI, Hugging Face, etc.) for production accuracy.
- To persist to disk, set the appropriate persist arguments per the Chroma client settings (see Chroma docs).

## Project layout
- README.md — this file
- examples/ — runnable example scripts
- data/ — optional sample datasets
- notebooks/ — exploratory notebooks

## Tips
- Start in-memory to understand how collections and queries behave.
- Keep embedding dimensionality consistent between upserts and queries.
- Use small datasets for quick iteration; add persistence when ready to scale.

## Contributing
Small improvements and clearer examples are welcome. Keep examples focused and reproducible.

## License
MIT