## মিল্ভাস সেটাপ

### মিল্ভাস ইনস্টলেশন

```bash
pip install -U pymilvus
```

### মিল্ভাস ক্লায়েন্ট তৈরি

```python
from pymilvus import MilvusClient
client = MilvusClient("milvus_demo.db")
```

### মিল্ভাস কালেকশন তৈরি

```python
client.create_collection(
    collection_name="test_collection",
    dimension=768,
)
```

### ডেটা প্রস্তুত করা

```bash
pip install "pymilvus[model]"
```

```python
from pymilvus import model
embedding_fn = model.DefaultEmbeddingFunction()

docs = [
    "Artificial intelligence was founded as an academic discipline in 1956.",
    "Alan Turing was the first person to conduct substantial research in AI.",
    "Born in Maida Vale, London, Turing was raised in southern England.",
]

vectors = embedding_fn.encode_documents(docs)
data = [
    {"id": i, "vector": vectors[i], "text": docs[i], "subject": "history"}
    for i in range(len(vectors))
]

```

### ডেটা মিল্ভাসে যোগ করা

```python
res = client.insert(
    collection_name="test_collection",
    data=data,
)
```

```json
{ "insert_count": 3, "ids": [0, 1, 2], "cost": 0 }
```

### ডেটা অনুসন্ধান করা

#### ভেক্টর অনুসন্ধান

```python
query_vectors = embedding_fn.encode_queries(["Who is Alan Turing?"])

res = client.search(
    collection_name="demo_collection",
    data=query_vectors,
    limit=2,
    output_fields=["text", "subject"],
)
print(res)
```

```python
data: ["[{'id': 2, 'distance': 0.5859944820404053, 'entity': {'text': 'Born in Maida Vale, London, Turing was raised in southern England.', 'subject': 'history'}}, {'id': 1, 'distance': 0.5118255615234375, 'entity': {'text': 'Alan Turing was the first person to conduct substantial research in AI.', 'subject': 'history'}}]"] ,
extra_info: {'cost': 0}
```

#### মেটাডাটা ফিল্টারিং

```python
res = client.search(
    collection_name="test_collection",
    data=query_vectors,
    limit=2,
    output_fields=["text", "subject"],
    filter="subject == 'history'",
)
print(res)

```

```python
data: ["[{'id': 4, 'distance': 0.27030569314956665, 'entity': {'text': 'Computational synthesis with AI algorithms predicts molecular properties.', 'subject': 'biology'}}, {'id': 3, 'distance': 0.16425910592079163, 'entity': {'text': 'Machine learning has been used for drug design.', 'subject': 'biology'}}]"] ,
extra_info: {'cost': 0}

```

#### ফিল্টারের বেসিক অপারেটর

- `Comparison Operators`: `==`, `!=`, `<`, `<=`, `>`, `>=`
  - `filter="subject == 'history'"`
- `Logical Operators`: `AND`, `OR`, `NOT`
  - `filter="subject == 'history' AND text LIKE '%Alan Turing%'"`
- `Range Filters`: `in`, `LIKE`
  - `filter="subject IN ['history', 'biology']"`
- `Arithmetic Operators`: `+`, `-`, `*`, `/`
  - `filter="age > x+y"`

**নোট** :
`filter = "age > {age} AND city in {city}"`
`filter_params = {"age": 25, "city": ["北京", "上海"]}`

আমরা `filter` স্ট্রিংয়ে `{}` ব্যবহার করে ভেরিয়েবল ইন্টারপোলেশন করতে পারি। এই ক্ষেত্রে, `filter_params` ডিকশনারিতে `{age}` এবং `{city}` এর মান প্রদান করতে হবে।

আরো ডাটা টাইপ স্পেসেফিক যেমন জেসন, অ্যারে ইত্যাদি ফিল্টারিংয়ের জন্য মিল্ভাসের [ডকুমেন্টেশন](https://milvus.io/docs/boolean.md) দেখতে পারেন।

### ডেটা কুয়েরি vs সার্চ

সার্চে আমরা N ভেক্টরের মধ্যে সবচেয়ে কাছের K ভেক্টর খুঁজে বের করি, যেখানে কুয়েরিতে আমরা নির্দিষ্ট শর্ত অনুযায়ী সব ভেক্টর খুঁজে বের করি।

```python
res = client.query(
    collection_name="demo_collection",
    filter="subject == 'history'",
    output_fields=["text", "subject"],
)

```

```python
res = client.query(
    collection_name="demo_collection",
    ids=[0, 2],
    output_fields=["vector", "text", "subject"],
)

```

### ডাটা ডিলেট করা

```python
res = client.delete(collection_name="demo_collection", ids=[0, 2])

print(res)

res = client.delete(
    collection_name="demo_collection",
    filter="subject == 'biology'",
)

print(res)
```

### সম্পূর্ণ কালেকশন মুছে ফেলা

```python
client.drop_collection(collection_name="demo_collection")
```
