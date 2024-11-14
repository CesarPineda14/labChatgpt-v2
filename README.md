# Web Content Search Using Langchain and OpenAI Embeddings

This project leverages Langchain, OpenAI embeddings, and Chroma to load, process, and query the content of a webpage. The application extracts text from a given webpage, splits the text into chunks, stores it in a vector index using Chroma, and then generates responses based on a query.

## Project Architecture and Components

The project consists of the following main components:

1. **Web Content Loader**:  
   Uses `WebBaseLoader` from Langchain to scrape content from a webpage.
   
2. **Text Splitter**:  
   Splits the loaded content into smaller chunks using `RecursiveCharacterTextSplitter` to prepare the text for efficient processing.

3. **Chroma Index**:  
   Chroma is used to store the text chunks as embeddings. The embeddings are generated using OpenAI's API through the `OpenAIEmbeddings` class.

4. **Query Processing**:  
   Once the text is split and indexed, the system retrieves relevant documents based on the provided query using Chroma’s vector store and returns an answer based on the most relevant content.

5. **OpenAI Integration**:  
   OpenAI's API key is used for generating embeddings for the content, which allows the system to perform semantic search efficiently.

### Project Flow
1. **Content Loading**:  
   A URL is provided, and the content from the webpage is fetched using `WebBaseLoader`.
   
2. **Text Splitting**:  
   The text is split into smaller chunks (with a size limit of 1000 characters and an overlap of 200 characters).
   
3. **Chroma Indexing**:  
   The split text is converted into embeddings using OpenAI's API, and these embeddings are stored in Chroma's vector store.
   
4. **Querying**:  
   A query is passed to the vector store, and the most relevant chunks of text are retrieved to generate a response.

## Installation and Setup

Follow the instructions below to get the project up and running:

### Prerequisites

- Python 3.7 or higher
- OpenAI API key

### Install Dependencies

1. Clone the repository:

    ```bash
    git clone https://github.com/CesarPineda14/RAGproject.git
    cd web-content-search
    ```

2. Install required Python packages:

    ```bash
    pip install -r requirements.txt
    ```

    The `requirements.txt` should include:

    ```plaintext
    langchain
    langchain-openai
    langchain_chroma
    langchain_community
    langchain_core
    langchain_text_splitters
    openai
    beautifulsoup4
    ```

3. Set your OpenAI API key:

    Replace the placeholder API key in the `create_chroma_index` function:

    ```python
    os.environ["OPENAI_API_KEY"] = "your-api-key-here"
    ```

4. Run the application:

    You can run the app by executing:

    ```bash
    python app.py
    ```

    Make sure to replace the URL and query in the script as needed.

## Example

In the example below, the script loads content from a Wikipedia page about Artificial Intelligence and queries for the main topic:

```python
url = "https://es.wikipedia.org/wiki/Inteligencia_artificial"
query = "What is the main topic of the website?"
main(url, query)

```

The application will print the relevant response based on the query, which will be extracted from the page content.

# Expected Output:

```csharp
Loading content from https://es.wikipedia.org/wiki/Inteligencia_artificial...
Loaded 1 document(s) from the webpage.
Splitting text into chunks...
Split into 3 chunks.
Creating Chroma index...
Generating response for query: What is the main topic of the website?
Generated Response: 
Artificial intelligence (AI) is the simulation of human intelligence processes by machines, especially computer systems...

```
