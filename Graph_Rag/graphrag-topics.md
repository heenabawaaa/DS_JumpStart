# GraphRAG & Knowledge Graph Topics

## Core Concepts

- Knowledge Graphs (KG) fundamentals
- Entities, Relationships, and Triples (Subject-Predicate-Object)
- Ontology and ontology design
- Ontology and Taxonomy design
- Schema design for graphs
- Graph theory basics (nodes, edges, weights, directed/undirected graphs)
- Property graphs vs RDF graphs
- Vector embeddings vs graph embeddings
- Retrieval-Augmented Generation (RAG) fundamentals
- Difference between Vector RAG and Graph RAG
- Hybrid RAG (Vector + Graph)

## Data Ingestion & Preprocessing

- Document chunking strategies
- Text preprocessing / cleaning
- OCR / PDF parsing (for unstructured data)
- Named Entity Recognition (NER)
- Entity Resolution / Entity Disambiguation
- Entity Linking
- Relation Extraction
- Coreference Resolution
- Event Extraction
- Triple Extraction (LLM-based or rule-based)
- Deduplication of entities/relationships

## Knowledge Graph Construction

- LLM-based graph extraction (prompting LLMs to output triples)
- Schema-guided extraction vs open extraction
- Graph construction pipelines (e.g., LLMGraphTransformer)
- Community detection algorithms:
  - Louvain algorithm
  - Leiden algorithm
  - Label Propagation
  - Girvan-Newman algorithm
- Graph summarization (community summaries)
- Hierarchical clustering of graph communities
- Node/edge property enrichment
- Graph deduplication & merging (entity resolution across documents)

## Graph Algorithms

- Shortest Path algorithms (Dijkstra, A*)
- PageRank / Personalized PageRank
- Betweenness Centrality
- Degree Centrality
- Closeness Centrality
- Eigenvector Centrality
- Random Walk algorithms
- Breadth-First Search (BFS)
- Depth-First Search (DFS)
- Graph traversal & multi-hop reasoning
- Subgraph extraction
- Graph pattern matching
- Motif detection
- Connected Components analysis
- Full Text Search (FTS)

## Embeddings & Representation Learning

- Node2Vec
- DeepWalk
- GraphSAGE
- Graph Convolutional Networks (GCN)
- Graph Attention Networks (GAT)
- Knowledge Graph Embeddings (TransE, DistMult, ComplEx, RotatE)
- Text embedding models (for hybrid retrieval)
- Embedding alignment (text + graph embeddings)

## Retrieval Strategies

- Local search (entity-centric retrieval)
- Global search (community-based/summarized retrieval)
- Multi-hop retrieval
- Subgraph retrieval
- Query-to-entity linking
- Query decomposition
- Cypher/SPARQL query generation from natural language
- Text-to-Cypher / Text-to-SPARQL
- Re-ranking retrieved subgraphs
- Context fusion (merging graph + vector results)
- Graph traversal-based context expansion

## Generation & Reasoning

- Prompt engineering for graph context injection
- Chain-of-thought reasoning over graphs
- Multi-hop question answering
- Graph-grounded answer synthesis
- Hallucination reduction via graph grounding
- Citation/provenance tracking from graph nodes

## Storage & Infrastructure

- **Graph databases:**
  - Neo4j
  - Amazon Neptune
  - TigerGraph
  - ArangoDB
  - Memgraph
  - NebulaGraph
- **Vector databases (for hybrid setups):**
  - Pinecone
  - Weaviate
  - Milvus
  - Qdrant
  - FAISS
- **Query languages:**
  - Cypher
  - SPARQL
  - Gremlin
  - GQL

## Frameworks & Tools

- Microsoft GraphRAG (official framework)
- LangChain (Graph modules — LLMGraphTransformer, GraphCypherQAChain)
- LlamaIndex (Knowledge Graph Index, PropertyGraphIndex)
- Neo4j LLM Knowledge Graph Builder
- NetworkX (graph manipulation in Python)
- RDFLib
- spaCy / Stanford NER (entity extraction)
- Haystack (graph pipelines)

## Evaluation & Optimization

- Retrieval evaluation metrics (precision, recall, MRR, NDCG)
- Answer faithfulness/groundedness evaluation
- Graph quality metrics (density, connectivity, coverage)
- Latency optimization for graph traversal
- Cost optimization (LLM calls during extraction)
- Scalability considerations for large graphs
- Incremental graph updates (handling new documents)

## Advanced/Emerging Topics

- Agentic GraphRAG (agents deciding traversal paths)
- Dynamic graph updates in real-time systems
- Multi-modal GraphRAG (images, tables + graph)
- Temporal Knowledge Graphs (time-aware relationships)
- Federated GraphRAG (across multiple graph sources)
- Graph-based memory for AI agents
- Explainability via graph paths (interpretable retrieval)
