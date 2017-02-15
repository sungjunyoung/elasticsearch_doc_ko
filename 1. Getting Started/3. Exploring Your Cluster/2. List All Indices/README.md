> [Getting Started](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/Getting%20Started) > [Exploring Your Cluster](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started/3.%20Exploring%20Your%20Cluster) > List All Indices
> 원본 : https://www.elastic.co/guide/en/elasticsearch/reference/current/_list_all_indices.html


### List All Indices

이제 우리 인덱스들을 살펴보겠습니다.
```
GET /_cat/indices?v
```
Response 는 다음과 같습니다.
```
health status index uuid pri rep docs.count docs.deleted store.size pri.store.size
```
클러스터 내에 아직 인덱스가 존재하지 않는다는 것을 의미합니다.
