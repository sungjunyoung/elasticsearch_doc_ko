> [Getting Started](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.$20Getting%20Started) > [Exploring Your Cluster](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started/3.%20Exploring%20Your%20Cluster) > Index and Query a Document  
> 원본 : https://www.elastic.co/guide/en/elasticsearch/reference/current/_index_and_query_a_document.html


### Index and Query a Document

이제 우리의 customer index 에 무언가를 넣어 봅시다. 도큐먼트를 인덱싱하기 위해서는, 우리는 Elasticsearch에게 색인의 어떤 유형으로 가야하는지 말해야합니다.(?)

customer 인덱스에 간단한 ID는 1이고, "external" 타입인 costomer 도큐먼트를 색인해 봅시다.
```
PUT /customer/external/1?pretty
{
    "name": "John Doe"
}
```
다음은 Response 입니다.
```json
{
  "_index" : "customer",
  "_type" : "external",
  "_id" : "1",
  "_version" : 1,
  "result" : "created",
  "_shards" : {
    "total" : 2,
    "successful" : 1,
    "failed" : 0
  },
  "created" : true
}
```
위에서 볼 수 있듯이, 우리는 새로운 costomer 도큐먼트가 성공적으로 customer 인덱스 안에 external 타입으로 만들어졌음을 볼 수 있습니다. 이 도큐먼트는 우리가 정해줫듯이 1 이라는 id 를 가지고 있습니다.

Elasticsearch에서는 문서를 인덱싱하기 전에 먼저 인덱스를 명시적으로 작성하지 않아도된다는 점에 유의해야합니다. 이전 예제에서 Elasticsearch는 사전에 이미 존재하지 않는 고객 인덱스를 자동으로 생성합니다.

우리가 인덱싱 했던 도큐먼트를 불러와 봅시다.

```
GET /customer/external/1?pretty
```
다음은 Response 입니다.
```json
{
  "_index" : "customer",
  "_type" : "external",
  "_id" : "1",
  "_version" : 1,
  "found" : true,
  "_source" : { "name": "John Doe" }
}
```
"found" 필드에서 id 가 1인 도큐먼트를 찾았는지에 대한 상태가 반환되고, "_source" 필드에서는 도큐먼트의 full JSON 을 보여줍니다.
