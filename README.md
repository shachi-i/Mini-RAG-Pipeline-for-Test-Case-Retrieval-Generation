# Mini RAG Pipeline for Test Case Retrieval & Generation
This project demonstrates a mini Retrieval-Augmented Generation (RAG) pipeline to improve test case generation by retrieving relevant examples based on a user prompt.
## Tools & Libraries Used

| Tool                        | Purpose                                                                 |
|-----------------------------|-------------------------------------------------------------------------|
| `sentence-transformers`     | Convert test cases into embeddings using `all-MiniLM-L6-v2`             |
| `FAISS`                     | Efficient similarity search to find the most relevant test cases        |
| `transformers` (HuggingFace)| Generate new test cases using models like GPT2                         |

---

## Pipeline Overview

### 1. Input Chunking & Embedding

- Each test case is structured with:
  - `title`
  - `steps` (list of strings)
  - `expected_result` (list of strings)
### 2. Retrieval with FAISS

- All embeddings are indexed using `FAISS` (`IndexFlatL2`).
- The user prompt is also embedded.
- The top-k most similar test case embeddings are retrieved using vector similarity.

### 3. Generation with LLM

- The retrieved test cases are used as input context.
- A prompt template is added:
```text
Based on the above examples, generate a new test case with this format:
Title: <title>
Steps:
- Step 1
- Step 2
