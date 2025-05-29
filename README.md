# Legal AI Research Assistant for Commercial Courts

A comprehensive system for processing Indian legal documents, building knowledge graphs, and implementing semantic retrieval with graph-based reranking for legal case analysis.

## Overview

This project implements a multi-stage pipeline for legal document analysis that combines semantic embeddings, graph-based relationships, and LLM-powered summarization to enable intelligent legal case retrieval and citation analysis.

## System Architecture

### Data Pipeline Flow
1. **Data Ingestion & Scraping** → **Preprocessing** → **Graph Construction** → **Embedding Generation** → **Retrieval & Reranking** → **LLM Summarization**

## Core Components

### 📄 Data Processing
- **`read_scrape.py`**: 
  - Reads parquet datasets (indiankanoon1.parquet, indiankanoon2.parquet)
  - Filters for commercial cases
  - Extracts and scrapes text into 8 different legal sections
  - Outputs CSV with original dataset fields + 8 extracted sections

- **`preprocess.py`**: 
  - Cleans data by dropping empty rows
  - Fills missing values (NA handling)
  - Outputs ready-to-use CSV for downstream processing

### 🕸️ Graph Construction
- **`buildgraph.py`**: 
  - Takes preprocessed CSV as input
  - Builds Graph RAG (Retrieval Augmented Generation) system
  - Creates nodes and relationships in Neo4j database
  - Establishes legal case connections and citations

### 🔍 Embedding & Vector Storage
- **`embedding.py`**: 
  - Retrieves data from Neo4j graph database
  - Uses **LegalBERT** model for domain-specific legal text embeddings
  - Stores embeddings in **ChromaDB** vector database

### 🎯 Retrieval System
- **`retrieval.py`**: 
  - Performs semantic similarity search for relevant cases/sections
  - Implements **graph reranking** based on graph similarity metrics
  - Combines vector similarity with graph-based relationships

### 🤖 LLM Integration
- **LLM Summarization**: Processes retrieved legal sections and generates summaries
- **Auto Citation**: Implements automatic citation edge detection and creation

## Features

### Current Implementation
- ✅ Commercial legal case filtering
- ✅ Multi-section text extraction (8 sections)
- ✅ Neo4j graph database integration
- ✅ LegalBERT embeddings
- ✅ ChromaDB vector storage
- ✅ Semantic + Graph-based retrieval
- ✅ LLM summarization

### Advanced Features (In Development)
- 🚧 Auto citation edge detection
- 🚧 Advanced GraphRAG features
- 🚧 Case outcome prediction

## Technology Stack

| Component | Technology |
|-----------|------------|
| **Graph Database** | Neo4j |
| **Vector Database** | ChromaDB |
| **Embeddings** | LegalBERT |
| **Data Processing** | Python, Pandas |
| **File Formats** | Parquet, CSV |

## Getting Started

### Prerequisites
- Python 3.8+
- Neo4j Database
- ChromaDB
- Required Python packages (see requirements.txt)

### Installation
```bash
# Clone repository
git clone <repository-url>
cd NLP_Legal

# Setup Neo4j database
# Setup ChromaDB
```

### Usage Pipeline

1. **Data Extraction**:
   ```bash
   python read_scrape.py
   ```

2. **Preprocessing**:
   ```bash
   python preprocess.py
   ```

3. **Graph Construction**:
   ```bash
   python buildgraph.py
   ```

4. **Generate Embeddings**:
   ```bash
   python embedding.py
   ```

5. **Run Retrieval**:
   ```bash
   python retrieval.py
   ```

## Data Flow

```
Parquet Files → Scraping → CSV → Preprocessing → Clean CSV → Graph DB → Embeddings → Vector DB → Retrieval System
```

## Project Structure

```
NLP_Legal/
├── read_scrape.py      # Data extraction and scraping
├── preprocess.py       # Data cleaning and preparation
├── buildgraph.py       # Neo4j graph construction
├── embedding.py        # LegalBERT embeddings generation
├── retrieval.py        # Semantic + graph retrieval
├── data/               # Dataset storage
├── outputs/            # Processed data outputs
└── README.md          # Project documentation
```

## Use Cases

- **Legal Research**: Find semantically and contextually similar legal cases
- **Citation Analysis**: Discover case precedents and citation networks
- **Document Summarization**: Generate concise summaries of legal sections
- **Precedent Discovery**: Identify relevant case law through graph relationships
