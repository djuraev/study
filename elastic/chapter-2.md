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

#### Update Document

<mark>Elasticsearch documents are immutable! </mark>
* How the Update API works<br>
  * The current document is retrieved
  * The field values are changed
  * The existing document is replaced with th modified document
 ```
 PUT /products/_doc/100
{
  "name" : "Toaster",
  "price" : 100,
  "in_stock": 4
}
 ```
 * New fields can be added to existing document. In below example, ```rating``` field is added.
 ```
 POST /products/_update/100
{
  "doc" : {
    "in_stock": 3,
    "rating": 4.5
  }
}
 ```

 #### Scripted Updates
 ```
 POST /products/_update/100
{
  "script" : {
    "source": "ctx._source.in_stock--"
  }
}
 ```

 * Assignment Update
```
POST /products/_update/100
{
  "script" : {
    "source": "ctx._source.in_stock = 10"
  }
}
```
```
POST /products/_update/100
{
  "script": {
    "source": "ctx._source.release -= params.quantity",
    "params" : {
      "quantity": 5
    }
  }
}
```