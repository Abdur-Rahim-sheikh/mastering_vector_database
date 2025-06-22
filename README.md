## Mastering Vector Database

কিছু জনপ্রিয় Vector Database এবং তাদের বৈশিষ্ট্য:

| Vectorstore              | Delete by ID | Filtering | Search by Vector | Search with score | Async | Passes Standard Tests | Multi Tenancy | IDs in add Documents |
| ------------------------ | ------------ | --------- | ---------------- | ----------------- | ----- | --------------------- | ------------- | -------------------- |
| AstraDBVectorStore       | ✅           | ✅        | ✅               | ✅                | ✅    | ❌                    | ❌            | ❌                   |
| [Chroma](/chroma)        | ✅           | ✅        | ✅               | ✅                | ✅    | ❌                    | ❌            | ❌                   |
| Clickhouse               | ✅           | ✅        | ❌               | ✅                | ❌    | ❌                    | ❌            | ❌                   |
| CouchbaseVectorStore     | ✅           | ✅        | ❌               | ✅                | ✅    | ❌                    | ❌            | ❌                   |
| DatabricksVectorSearch   | ✅           | ✅        | ✅               | ✅                | ✅    | ❌                    | ❌            | ❌                   |
| ElasticsearchStore       | ✅           | ✅        | ✅               | ✅                | ✅    | ❌                    | ❌            | ❌                   |
| FAISS                    | ✅           | ✅        | ✅               | ✅                | ✅    | ❌                    | ❌            | ❌                   |
| InMemoryVectorStore      | ✅           | ✅        | ❌               | ✅                | ✅    | ❌                    | ❌            | ❌                   |
| Milvus                   | ✅           | ✅        | ✅               | ✅                | ✅    | ✅                    | ✅            | ✅                   |
| MongoDBAtlasVectorSearch | ✅           | ✅        | ✅               | ✅                | ✅    | ❌                    | ❌            | ❌                   |
| openGauss                | ✅           | ✅        | ✅               | ✅                | ❌    | ✅                    | ❌            | ✅                   |
| PGVector                 | ✅           | ✅        | ✅               | ✅                | ✅    | ❌                    | ❌            | ❌                   |
| PineconeVectorStore      | ✅           | ✅        | ✅               | ❌                | ✅    | ❌                    | ❌            | ❌                   |
| QdrantVectorStore        | ✅           | ✅        | ✅               | ✅                | ✅    | ❌                    | ❌            | ❌                   |
| Redis                    | ✅           | ✅        | ✅               | ✅                | ✅    | ❌                    | ❌            | ❌                   |
| Weaviate                 | ✅           | ✅        | ✅               | ✅                | ✅    | ❌                    | ✅            | ❌                   |
| SQLServer                | ✅           | ✅        | ✅               | ✅                | ❌    | ❌                    | ❌            | ❌                   |
