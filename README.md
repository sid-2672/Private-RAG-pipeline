# Private RAG Pipeline

### Local-First, Air-Gapped Document Intelligence

![Privacy Badge](https://img.shields.io/badge/Privacy-Air--Gapped-green?style=flat-square&logo=shield)
![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)
![Stack](https://img.shields.io/badge/Stack-LangChain_|_Ollama-orange?style=flat-square)

## 1. Description

**Private-RAG-pipeline** is an enterprise-grade retrieval-augmented generation system engineered for strict data sovereignty. It provides a secure, offline environment for ingesting, indexing, and querying sensitive documentation (Legal, Medical, Financial) without any external data exfiltration. By leveraging local inference engines and on-premise vector stores, it ensures that confidential information remains within the organization's secure perimeter at all times.

## 2. Why This Matters?

In an era of ubiquitous cloud-based AI services, the risk of unintentional data leakage is critical. Standard RAG implementations often rely on external APIs (e.g., OpenAI, Anthropic), necessitating the transmission of proprietary documents to third-party servers for embedding and generation.

*   **Risk:** Compliance violations (GDPR, HIPAA), loss of intellectual property, and exposure of PII.
*   **Solution:** This pipeline executes the entire RAG workflow—from OCR to inference—on local hardware. No network requests are made to external AI providers, guaranteeing 100% data privacy and compliance with strict air-gapped security policies.

## 3. System Architecture

The pipeline implements a unidirectional data flow designed for security and traceability.

```mermaid
graph LR
    subgraph Ingestion [Secure Ingestion Layer]
        PDF[Sensitive PDF] --> OCR[Text Extraction]
        OCR --> Chunk[Semantic Chunking]
    end

    subgraph Storage [Local Knowledge Base]
        Chunk --> Embed[Local Embedding Model]
        Embed --> Vector[Vector Store (ChromaDB)]
    end

    subgraph Inference [Air-Gapped Generation]
        Query[User Query] --> Search[Semantic Retrieval]
        Vector --> Search
        Search --> Context[Prompt Construction]
        Context --> LLM[Local LLM (Ollama)]
        LLM --> Response[Secure Output]
    end
```

## 4. Key Features

<table>
  <tr>
    <th width="30%">Feature</th>
    <th width="70%">Description</th>
  </tr>
  <tr>
    <td><strong>Zero-Trust Architecture</strong></td>
    <td>Complete isolation from public internet AI APIs. All processing (embedding, indexing, inference) occurs on localhost or on-premise servers.</td>
  </tr>
  <tr>
    <td><strong>Multi-Model Support</strong></td>
    <td>Vendor-agnostic integration with open-weights models. Seamlessly swap between Llama 3, Mistral, or Gemma via the Ollama orchestration layer.</td>
  </tr>
  <tr>
    <td><strong>Context Retrieval</strong></td>
    <td>High-precision semantic search retrieval enhances generation accuracy, reducing hallucinations by grounding responses in the provided source text.</td>
  </tr>
  <tr>
    <td><strong>Data Sovereignty</strong></td>
    <td>Ensures full ownership and control of both the raw data and the derived vector embeddings.</td>
  </tr>
</table>

## 5. Installation

### Prerequisites
*   **Python:** 3.8+
*   **Ollama:** Installed and running locally.

### Steps

1.  Clone the repository:
    ```bash
    git clone https://github.com/sid-2672/Private-RAG-pipeline.git
    cd Private-RAG-pipeline
    ```

2.  Install dependencies:
    ```bash
    pip install -r requirements.txt
    ```

3.  Start the Ollama inference server (in a separate terminal):
    ```bash
    ollama serve
    # Pull a preferred model (e.g., Llama 3)
    ollama pull llama3
    ```

## 6. Usage

Launch the interface to begin secure document processing.

```bash
streamlit run app.py
```

**Workflow:**
1.  **Upload:** Select 'Upload Sensitive Document' to ingest PDF files.
2.  **Indexing:** The system locally embeds and stores the document vectors.
3.  **Query:** Use the 'Query via Natural Language' input to ask questions about the document content.

## 7. Roadmap

*   [ ] **OCR Integration:** Enhanced support for scanned PDFs using Tesseract.
*   [ ] **Multi-Modal Inputs:** Support for image-based diagram analysis within documents.
*   [ ] **Role-Based Access Control (RBAC):** Granular permissions for multi-user on-premise deployments.

## 8. License

**MIT License**

Copyright (c) 2026 Siddharth Prabhu. All rights reserved.
