# PaperPilot AI — Retrieval-Augmented Generation Assistant

PaperPilot AI is an AI-powered research assistant that answers questions about research papers using Retrieval-Augmented Generation (RAG). It retrieves relevant passages from a document, reranks them for relevance, and uses Google's Gemini API to generate answers grounded in the retrieved evidence.

## Features

- **PDF text extraction:** Extracts text from research papers using PyMuPDF.
- **Sentence-aware chunking:** Splits extracted text into manageable, overlapping chunks.
- **Semantic search:** Uses Sentence Transformers (`all-MiniLM-L6-v2`) to generate embeddings.
- **Vector retrieval:** Uses FAISS for efficient similarity search.
- **Cross-encoder reranking:** Reranks candidate passages using `cross-encoder/ms-marco-MiniLM-L-6-v2`.
- **Grounded answers:** Uses the Gemini API to generate responses from retrieved context.
- **Basic evidence rejection:** Rejects some questions when retrieved evidence appears insufficient.
- **Interactive interface:** Provides a Gradio chat interface for asking questions and viewing source passages.

## Architecture

PDF Research Paper → Text Extraction → Chunking → Embeddings → FAISS Retrieval → Cross-Encoder Reranking → Evidence Check → Gemini Answer Generation → Gradio Interface

## Technology Stack

- Python
- PyMuPDF
- Sentence Transformers
- FAISS
- Requests
- Google Gemini API
- Gradio
- Google Colab / Jupyter Notebook

## Getting Started

### 1. Open the notebook

Open `PaperPilot_AI_RAG_Assistant.ipynb` in Google Colab or a compatible Jupyter environment.

### 2. Install dependencies

Run the following command in a notebook cell:

```python
%pip install -r requirements.txt
```

If running outside the project directory, provide the correct path to `requirements.txt`.

### 3. Configure the Gemini API key

Obtain an API key through Google AI Studio. The notebook uses `getpass()` to request the key without displaying it while typing.

```python
from getpass import getpass

api_key = getpass("Enter your Gemini API key: ")
```

Never hardcode the API key, commit it to GitHub, or share it publicly.

### 4. Load a research paper

Upload a PDF you are permitted to use and set its path in the notebook. Run the cells in order to extract text, create chunks, generate embeddings, and build the FAISS index.

### 5. Ask questions

Use the retrieval and reranking pipeline to find relevant passages. The Gemini API generates an answer using the retrieved context, and the Gradio interface lets users interact with the system.

## Current Limitations

- Retrieval quality depends on document quality, chunking, embeddings, and reranking.
- The evidence-rejection threshold is a heuristic, not a calibrated confidence score.
- Generated answers can still contain errors; citations and source passages should be checked.
- PDF extraction may not work reliably for scanned documents without OCR.
- API usage may incur costs or be subject to provider quotas and rate limits.
- The notebook downloads pretrained models and may require significant memory and setup time.

## Future Improvements

- Add a more robust evidence-grounding and citation-validation mechanism.
- Evaluate retrieval quality with Recall@K, MRR, and nDCG.
- Evaluate answer faithfulness and correctness using a defined test set.
- Add support for multiple PDFs and persistent document indexes.
- Improve error handling, configuration, and logging.
- Add automated tests and a reproducible evaluation pipeline.

## Project Structure

```text
PaperPilot-AI/
├── PaperPilot_AI_RAG_Assistant.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

## Disclaimer

PaperPilot AI is an educational AI/ML project intended to assist with research-paper exploration. It is not a substitute for reading and verifying the original research.

## Author

Developed as an AI/ML portfolio project.

## Research Paper Used During Development

Vaswani, A. et al. (2017). *Attention Is All You Need.*

https://arxiv.org/abs/1706.03762
