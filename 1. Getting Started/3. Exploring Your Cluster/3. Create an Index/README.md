> [Getting Started](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/Getting%20Started) > [Exploring Your Cluster](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started/3.%20Exploring%20Your%20Cluster) > Create an Index
> 원본 : https://www.elastic.co/guide/en/elasticsearch/reference/current/_create_an_index.html


### Create an Index

이제 우리는 "customer" 라는 인덱스를 만들어 보고, 다시한번 모든 인덱스 리스트를 볼 것입니다.
```
PUT /customer?pretty
GET /_cat/indices?v
```
