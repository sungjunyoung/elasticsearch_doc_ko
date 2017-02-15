> [Getting Started](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started) > [Modifying Your Data](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started/4.%20Modifying%20Your%20Data) > Updating Documents
> 원본 : https://www.elastic.co/guide/en/elasticsearch/reference/current/_modifying_your_data.html

### Updating Documents

도큐먼트를 인덱싱하고, 대체할 뿐만 아니라, 업데이트도 할 수 있습니다. 우리가 업데이트를 수행할 때, Elasticsearch는 이전 도큐먼트를 삭제하고, 한번에 새로운 도큐먼트를 인덱싱합니다.

이 예제는 "name" 필드를 "김예슬"로 변경하면서 어떻게 우리의 이전 도큐먼트 (ID 1)를 업데이트 하는지 보여줍니다.
```json
POST /customer/external/1/_update?pretty
{
  "doc": { "name": "김예슬" }
}

```
다음의 예제는 이전 도큐먼트에 (ID 1) "name" 필드를 "김예슬" 로 변경하면서, 동시에 "age" 필드를 추가를 하는 방법을 보여줍니다.
```json
POST /customer/external/1/_update?pretty
{
  "doc": { "name": "김예슬", "age": 23 }
}
```
업데이트는 간단한 스크립트를 통해 수행될 수도 있습니다. ID 1 도큐먼트의 age 에 +5 를 시키는 방법입니다.
```json
POST /customer/external/1/_update?pretty
{
  "script" : "ctx._source.age += 5"
}
```
위의 예제에서 ctx._source는 업데이트하려고하는 현재 소스 문서를 참조합니다.

이 글을 쓰는 시점에서 한 번에 하나의 문서에 대해서만 업데이트를 수행 할 수 있습니다. 앞으로 Elasticsearch는 쿼리 조건 (예 : SQL UPDATE-WHERE 문)이있는 여러 문서를 업데이트 할 수있는 기능을 제공 할 수도 있습니다.
