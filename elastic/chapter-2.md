## ElasticSearch basics

#### Create index
```
PUT /products
{
  "settings": {
    "number_of_shards": 2,
    "number_of_replicas": 2
  }
}
```

#### Indexing document

```
POST /products/_doc
{
  "name" : "P&G",
  "price" : 1000,
  "in_stock": 10
}
```

* Indexing with ID
```
PUT /products/_doc/100
{
  "name" : "Toaster",
  "price" : 100,
  "in_stock": 4
}
```

#### Retrieve Document
* With ID
```
GET /products/_doc/100
```