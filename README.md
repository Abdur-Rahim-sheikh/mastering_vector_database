## Mastering Vector Database

কিছু জনপ্রিয় Vector Database এবং তাদের বৈশিষ্ট্য:

| Vectorstore                   | Free Tier / License                       | Delete by ID | Filtering | Search by Vector | Search with score | Async | Passes Standard Tests | Multi Tenancy | IDs in add Documents |
| ----------------------------- | ----------------------------------------- | ------------ | --------- | ---------------- | ----------------- | ----- | --------------------- | ------------- | -------------------- |
| [Chroma](/chroma)             | ✅ Open Source (MIT)                      | ✅           | ✅        | ✅               | ✅                | ✅    | ❌                    | ❌            | ❌                   |
| [FAISS](/faiss/)              | ✅ Open Source (Facebook AI)              | ✅           | ✅        | ✅               | ✅                | ✅    | ❌                    | ❌            | ❌                   |
| [QdrantVectorStore](/qdrant/) | ✅ Open Source & Free Cloud Tier          | ✅           | ✅        | ✅               | ✅                | ✅    | ❌                    | ❌            | ❌                   |
| Weaviate                      | ✅ Open Source & Free Cloud Tier          | ✅           | ✅        | ✅               | ✅                | ✅    | ❌                    | ✅            | ❌                   |
| [Milvus](/milvus/)            | ✅ Open Source (LF AI Foundation)         | ✅           | ✅        | ✅               | ✅                | ✅    | ✅                    | ✅            | ✅                   |
| PGVector                      | ✅ Open Source (PostgreSQL extension)     | ✅           | ✅        | ✅               | ✅                | ✅    | ❌                    | ❌            | ❌                   |
| Redis                         | ✅ Open Source (RediSearch)               | ✅           | ✅        | ✅               | ✅                | ✅    | ❌                    | ❌            | ❌                   |
| openGauss                     | ✅ Open Source (Huawei)                   | ✅           | ✅        | ✅               | ✅                | ❌    | ✅                    | ❌            | ✅                   |
| Clickhouse                    | ✅ Open Source                            | ✅           | ✅        | ❌               | ✅                | ❌    | ❌                    | ❌            | ❌                   |
| InMemoryVectorStore           | ✅ In-memory mock (for testing only)      | ✅           | ✅        | ❌               | ✅                | ✅    | ❌                    | ❌            | ❌                   |
| ElasticsearchStore            | ✅ Free tier (OpenSearch or OSS version)  | ✅           | ✅        | ✅               | ✅                | ✅    | ❌                    | ❌            | ❌                   |
| PineconeVectorStore           | ✅ Cloud Free Tier (1 pod, 5M vec)        | ✅           | ✅        | ✅               | ❌                | ✅    | ❌                    | ❌            | ❌                   |
| MongoDBAtlasVectorSearch      | ✅ Free Tier (shared cluster)             | ✅           | ✅        | ✅               | ✅                | ✅    | ❌                    | ❌            | ❌                   |
| AstraDBVectorStore            | ✅ Free Tier (DataStax Astra 10GB)        | ✅           | ✅        | ✅               | ✅                | ✅    | ❌                    | ❌            | ❌                   |
| DatabricksVectorSearch        | 🟡 Free with Databricks Community Edition | ✅           | ✅        | ✅               | ✅                | ✅    | ❌                    | ❌            | ❌                   |
| CouchbaseVectorStore          | 🟡 Enterprise (limited community edition) | ✅           | ✅        | ❌               | ✅                | ✅    | ❌                    | ❌            | ❌                   |
| SQLServer                     | ❌ Proprietary (Express lacks vector ops) | ✅           | ✅        | ✅               | ✅                | ❌    | ❌                    | ❌            | ❌                   |
