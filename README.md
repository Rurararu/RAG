# RAG System

This project demonstrates two separate Retrieval-Augmented Generation (RAG) pipelines using **LlamaIndex** to enable question-answering over local CSV and PDF documents, leveraging the power of **OpenAI** for language model capabilities.

## Project Structure

The project consists of Jupyter Notebooks and a dedicated folder for the input data:

```
RAG_Project/
├── data/               # Directory for input files (CSV, PDF, etc.)
│   ├── your_data.csv   # Placeholder for CSV data
│   └── your_doc.pdf    # Placeholder for PDF document
├── RAG_CSV.ipynb       # Jupyter Notebook for querying CSV data
├── RAG_PDF.ipynb       # Jupyter Notebook for querying PDF data
└── .env                # File for storing environment variables (API Key)
```

-----

## Getting Started

### Prerequisites

  * Python 3.x
  * A valid **OpenAI API Key** (required for embedding and LLM functionality).

### Installation and Setup

1.  **Clone the Repository** (or download the files) and navigate to the project directory.

2.  **Set up the Virtual Environment** (highly recommended):

    ```bash
    python -m venv venv
    # Activate the environment (Linux/macOS)
    source venv/bin/activate
    # Activate the environment (Windows)
    .\venv\Scripts\activate
    ```

3.  **Install Dependencies**:

    Install all necessary packages using your requirements.txt file:
4. 
    ```bash
    pip install -r requirements.txt    
    ```

4.  **Configure API Key**:

    Create a file named **`.env`** in the root directory and add your OpenAI API key:

    ```
    OPENAI_API_KEY="YOUR_API_KEY_HERE"
    ```

5.  **Add Data**:

    Place your CSV file (e.g., `data.csv`) and PDF file (e.g., `document.pdf`) into the **`data/`** directory. **Make sure to update the filenames inside the notebooks to match your files.**

-----

## How It Works

This project features two separate notebooks, each implementing a dedicated RAG pipeline optimized for its data type.

### 1\. RAG\_PDF.ipynb (Querying Unstructured Data)

  * **Loading**: The notebook uses the **`SimpleDirectoryReader`** (or a specific PDF loader) to read the text content from the PDF file.
  * **Indexing**: It creates a **Vector Store Index**. The document is chunked, and each chunk is converted into a numerical vector (embedding) using OpenAI's embedding model. These embeddings are stored for efficient semantic search.
  * **Querying**: When a user asks a question, the query engine performs a **semantic search** in the index to retrieve the most relevant text chunks (context) from the PDF.
  * **Generation (RAG)**: The relevant context and the user's question are passed to the OpenAI LLM, which generates a grounded answer based *only* on the provided context.

### 2\. RAG\_CSV.ipynb (Querying Tabular Data)

  * **Loading**: This notebook uses the **Pandas tools**. It loads the CSV file into a Pandas DataFrame.
  * **Indexing/Querying**: Instead of creating a vector index, it uses the **`PandasQueryEngine`**. This engine translates your natural language questions into executable Pandas code (e.g., filtering, aggregation) to get an exact answer from the table.
  * **LLM Role**: The LLM (OpenAI) is used to generate the correct Python/Pandas code and formulate the final answer based on the code output.

