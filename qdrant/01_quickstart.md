## Qdrant এর লোকাল সেটাপ

```bash
docker pull qdrant/qdrant
docker run -p 6333:6333 -v "$(pwd)/qdrant_data:/qdrant/storage:z" qdrant/qdrant
```

- REST API: http://localhost:6333
- gRPC API: localhost:6334
- Web UI: http://localhost:6333/dashboard

## 1. Qdrant এর সংযোগ

```python
from qdrant_client import QdrantClient
client = QdrantClient(url="http://localhost:6333")
```

## 2. একটি নতুন Collection তৈরি করা

```python
from qdrant_client.models import Distance, VectorParams

client.create_collection(
    collection_name="test_collection",
    vectors_config=VectorParams(size=4, distance=Distance.DOT),
)
```

## 3. ডেটা যোগ করা

```python
from qdrant_client.models import PointStruct

operation_info = client.upsert(
    collection_name="test_collection",
    wait=True,
    points=[
        PointStruct(id=1, vector=[0.05, 0.61, 0.76, 0.74], payload={"city": "Berlin"}),
        PointStruct(id=2, vector=[0.19, 0.81, 0.75, 0.11], payload={"city": "London"}),
    ],
)

print(operation_info)
```

here

- **wait=True**: এই অপশনটি নিশ্চিত করে যে, ডেটা আপলোড সম্পূর্ণ না হওয়া পর্যন্ত প্রোগ্রাম থামবে না।

### Response

```python
operation_id=0 status=<UpdateStatus.COMPLETED: 'completed'>
```

## 4. ডেটা অনুসন্ধান করা

এখানে আমরা একটি ভেক্টর দিয়ে অনুসন্ধান করবো এবং ফলাফলগুলো পেইলোড ছাড়া ফিরিয়ে দেবো।

```python
search_result = client.query_points(
    collection_name="test_collection",
    query=[0.2, 0.1, 0.9, 0.7],
    with_payload=False,
    limit=3
).points

print(search_result)
```

### Response

```python
[
  {
    "id": 4,
    "version": 0,
    "score": 1.362,
    "payload": null,
    "vector": null
  },
  {
    "id": 1,
    "version": 0,
    "score": 1.273,
    "payload": null,
    "vector": null
  }
]
```

## 5. ফিল্টার যুক্ত করে অনুসন্ধান করা

```python
from qdrant_client.models import Filter, FieldCondition, MatchValue

search_result = client.query_points(
    collection_name="test_collection",
    query=[0.2, 0.1, 0.9, 0.7],
    query_filter=Filter(
        must=[FieldCondition(key="city", match=MatchValue(value="London"))]
    ),
    with_payload=True,
    limit=3,
).points

print(search_result)
```

### Response

```python
[
    {
        "id": 2,
        "version": 0,
        "score": 0.871,
        "payload": {
            "city": "London"
        },
        "vector": null
    }
]
```

**নোট**: ফিল্টার্ড অনুসন্ধানকে ফাস্ট করতে পেলোড ইনডেক্স ব্যবহার করতে হবে।

```python
client.create_payload_index(
    collection_name="{collection_name}",
    field_name="name_of_the_field_to_index",
    field_schema="keyword",
)
```

### Available Field Schemas

- `keyword`: সাধারণ টেক্সট ফিল্ড `match` ফিল্টার সমর্থন করে
- `integer`: পূর্ণসংখ্যা ফিল্ড `match` এবং `range` ফিল্টার সমর্থন করে
- `float`: ফ্লোট ফিল্ড `range` ফিল্টার সমর্থন করে
- `bool`: বুলিয়ান ফিল্ড `match` ফিল্টার সমর্থন করে
- `datetime`: ডেটটাইম ফিল্ড `range` ফিল্টার সমর্থন করে
- `geo`: জিওগ্রাফিক্যাল ফিল্ড `geo-bounding-box` এবং `geo-radius` ফিল্টার সমর্থন করে
- `text`: এটি `keyword` এর একটি বিশেষ ইন্ডেক্সিং যা ফুল্টেক্সট সার্চ সমর্থন করে।
- `uuid`: ইউনিক আইডেন্টিফায়ার ফিল্ড `match` ফিল্টার সমর্থন করে

## বিস্তারিত যানতে

Qdrant এর অফিসিয়াল ডকুমেন্টেশন দেখুন: [Qdrant Documentation](https://qdrant.tech/documentation/)
