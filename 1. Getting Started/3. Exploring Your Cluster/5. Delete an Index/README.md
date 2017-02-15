> [Getting Started](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.$20Getting%20Started) > [Exploring Your Cluster](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started/3.%20Exploring%20Your%20Cluster) > Delete an Index
> 원본 : https://www.elastic.co/guide/en/elasticsearch/reference/current/_delete_an_index.html


### Delete an Index

이제, 인덱스를 지우고 다시한번 인덱스 리스트를 보도록 합시다.
```
DELETE /customer?pretty
GET /_cat/indices?v
```
다음은 Response 입니다.
```
health status index uuid pri rep docs.count docs.deleted store.size pri.store.size
```
이 Response 는 인덱스 삭제가 성공적으로 완료되었고, 클러스터 내에는 아무것도 없다는 것을 의미합니다.

넘어가기 전에, 지금까지 알아보았던 API commands 들을 봅시다.
```
PUT /customer
PUT /customer/external/1
{
  "name": "John Doe"
}
GET /customer/external/1
DELETE /customer
```
위의 명령을 신중하게 검토하면 실제로 Elasticsearch에서 데이터에 액세스하는 패턴을 볼 수 있습니다. 이 패턴은 다음과 같이 요약 할 수 있습니다.
```
<REST Verb>/<Index>/<Type>/<ID>
```
이 REST 액세스 패턴은 모든 API 명령 전반에 걸쳐 퍼져 있으며, 간단하게 기억할 수 있다면 Elasticsearch를 배울 때 좋은 출발점이 될 것입니다.
