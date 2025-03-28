---
sidebar_position: 6
---

# MCP Proof of Concept: ChromaDB Integration

## Overview

As part of Sprint 4, we developed a proof of concept (POC) implementation of a Model Context Protocol (MCP) server that integrates with ChromaDB. This POC demonstrates how we can extend AI capabilities by providing access to document repositories through vector similarity search.

## Technical Implementation

### Repository Structure

The ChromaDB-MCP server follows a clean, modular structure:

```
.
├── chroma_db/           # Persistent storage for vector database
├── files/               # Directory for input documents
├── scripts/             # Utility scripts for document processing
├── src/                 # Source code
│   ├── configs/         # Configuration settings
│   ├── infra/           # Infrastructure implementations
│   ├── ports/           # Interface definitions
│   ├── tools/           # MCP tool implementations
│   ├── dependency_manager.py # Dependency injection container
│   └── server.py        # MCP server implementation
├── .env                 # Environment variables
├── main.py              # Application entry point
└── pyproject.toml       # Project dependencies and metadata
```

### Key Components

#### 1. MCP Server Implementation

The core of the POC is the MCP server implementation in `server.py`, which uses the FastMCP framework:

```python
from mcp.server.fastmcp import FastMCP
from src.tools import Tools
from .dependency_manager import DependencyContainer

mcp = FastMCP("chromadb")
tools = Tools(DependencyContainer.get_vector_store())

@mcp.tool()
async def get_similar_chunks(query: str, k: int = 2) -> str:
    """
    Retrieve chunks similar to the input query using the configured vector store.

    Args:
        query: The input text to find similar chunks for
        k: The number of chunks to retrieve

    Returns:
        A JSON containing the chunks and their metadata, or "No results were found" if no chunks found
    """
    return tools.retrieve_similar_chunks(query, k)

def main():
    print("MCP server chromadb started!")
    mcp.run(transport="stdio")
```

This code registers a tool called `get_similar_chunks` that allows AI models to query the vector database for text chunks similar to a given input.

#### 2. Tool Implementation

The actual functionality for retrieving similar chunks is implemented in the `Tools` class:

```python
class Tools:
    def __init__(self, vector_store: VectorStore) -> None:
        self.__vector_store = vector_store

    def retrieve_similar_chunks(self, query: str, k: int = 2) -> str:
        results = self.__vector_store.get_chunks(inputs=[query], k=k)
        if results is None:
            return "No results were found"
        return results.model_dump_json()
```

This class serves as a wrapper for the vector store operations, providing a clean interface for the MCP tools.

#### 3. Dependency Management

We've implemented a dependency injection container to manage service dependencies:

```python
class DependencyContainer:
    __vector_store: Optional[VectorStore] = None

    @classmethod
    def get_vector_store(cls) -> VectorStore:
        if cls.__vector_store is None:
            chroma_client = cls.__get_chroma_client()
            cls.__vector_store = ChromaVectorStore(chroma_client)
        return cls.__vector_store

    @classmethod
    def __get_chroma_client(cls) -> chromadb.ClientAPI:
        persist_directory = os.environ.get(
            "CHROMA_PERSIST_DIRECTORY", "./chroma_db"
        )
        return chromadb.PersistentClient(path=persist_directory)
```

This approach allows for clean dependency management and easier testing.

#### 4. Vector Store Interface

We defined a clear interface for vector store operations:

```python
class VectorStore(Protocol):
    def get_chunks(self, inputs: List[str], k: int = 2) -> Optional[SimilaritySearchResult]:
        """
        Get chunks similar to the input query.
        
        Args:
            inputs: The input queries to find similar chunks for
            k: The number of chunks to retrieve
            
        Returns:
            A SimilaritySearchResult containing chunks and their metadata, or None if no results
        """
        ...
```

This interface allows us to potentially swap out ChromaDB for other vector databases in the future.

#### 5. ChromaDB Implementation

The actual implementation uses ChromaDB for vector storage and retrieval:

```python
class ChromaVectorStore:
    def __init__(self, client: chromadb.ClientAPI) -> None:
        self.__client = client
        self.__collection = self.__get_or_create_collection()

    def __get_or_create_collection(self) -> chromadb.Collection:
        return self.__client.get_or_create_collection(
            name="documents",
            embedding_function=embedding_functions.GoogleGenerativeAiEmbeddingFunction(
                api_key=os.environ.get("GOOGLE_API_KEY"),
                model_name="text-embedding-004"
            )
        )
        
    def get_chunks(self, inputs: List[str], k: int = 2) -> Optional[SimilaritySearchResult]:
        results = self.__collection.query(
            query_texts=inputs,
            n_results=k
        )
        
        if not results or not results['ids'] or len(results['ids'][0]) == 0:
            return None
            
        return SimilaritySearchResult(
            chunks=[
                Chunk(
                    id=result_id,
                    text=documents[i],
                    metadata=metadatas[i] if metadatas else {}
                )
                for i, result_id in enumerate(ids[0])
            ],
            query=inputs[0]
        )
```

This implementation uses Google's text-embedding-004 model for generating embeddings of document chunks.

## Integration with Claude Desktop

A key feature of this POC is its ability to integrate with Claude Desktop. This integration allows Claude to access our document repository directly, enhancing its capabilities with our specific knowledge base.

Configuration example in `claude_desktop_config.json`:

```json
{
   "mcpServers": {
      "chromadb": {
         "command": "/path/to/bin/uv",
         "args": [
         "--directory",
         "/path/to/chromadb-mcp",
         "run",
         "main.py"
         ],
         "env": {
            "INPUT_DIR": "/path/to/files",
            "CHROMA_PERSIST_DIRECTORY": "/path/to/chroma_db",
            "GOOGLE_API_KEY": "API-KEY-HERE"
         }
      }
   }
}
```

## Document Processing

The POC includes scripts for processing documents:

1. **Loading Documents** - Reading files from the specified input directory
2. **Chunking** - Breaking documents into smaller semantic chunks
3. **Embedding** - Converting text chunks to vector embeddings
4. **Storage** - Saving embeddings and metadata in ChromaDB

## Challenges and Solutions

### Challenge: Document Chunking

**Problem**: Determining the optimal chunk size for document storage and retrieval.

**Solution**: We implemented a recursive text splitting approach that balances chunk size with semantic coherence, using paragraph and sentence boundaries as natural split points.

### Challenge: Embedding Quality

**Problem**: Ensuring high-quality embeddings for accurate similarity search.

**Solution**: We selected Google's text-embedding-004 model, which provides state-of-the-art embedding quality for semantic similarity tasks.

### Challenge: MCP Transport

**Problem**: Establishing reliable communication between Claude and our MCP server.

**Solution**: We implemented the stdio transport option in FastMCP, allowing for robust communication through standard input/output streams.

## Lessons Learned

1. **MCP Simplifies Integration** - The MCP standard provides a clean, consistent way for AI models to access external tools.

2. **Dependency Management** - Clear interfaces and dependency injection make the codebase more maintainable and testable.

3. **Vector Database Performance** - ChromaDB provides efficient similarity search capabilities, even with relatively large document collections.

4. **Embedding Quality Matters** - The choice of embedding model significantly impacts search results quality.

## Next Steps

Based on our experience with this POC, we've identified several areas for improvement:

1. **Enhanced Document Processing** - More sophisticated chunking and metadata extraction
2. **Query Refinement** - Adding filters and advanced search options
3. **Multi-collection Support** - Managing multiple document collections
4. **Performance Optimization** - Improving response times for large collections
5. **Error Handling** - More robust error handling and feedback
6. **Authorization** - Adding user-specific access controls to document collections

## Conclusion

The ChromaDB-MCP POC successfully demonstrates the potential of MCP for extending AI capabilities. By providing Claude with direct access to our document repository, we enable more contextually relevant and knowledgeable responses.

This implementation serves as a foundation for more sophisticated MCP servers in our roadmap, proving the viability of our approach to AI capabilities enhancement. 