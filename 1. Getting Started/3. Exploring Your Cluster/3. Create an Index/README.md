> [Getting Started](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.$20Getting%20Started) > [Exploring Your Cluster](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started/3.%20Exploring%20Your%20Cluster) > Create an Index  
> 원본 : https://www.elastic.co/guide/en/elasticsearch/reference/current/_create_an_index.html


### Create an Index

이제 우리는 "customer" 라는 인덱스를 만들어 보고, 다시한번 모든 인덱스 리스트를 볼 것입니다.
```
PUT /customer?pretty
GET /_cat/indices?v
```
첫번째 커맨드에서는 PUT 메서드를 이용해 "customer"라는 이름의 인덱스를 만들었습니다. 우리는 간단하게 pretty 문자열을 붙여 이쁘게(?) JSON response 를 출력하도록 할 수 있습니다.

Response 는 다음과 같습니다.
```
health status index    uuid                   pri rep docs.count docs.deleted store.size pri.store.size
yellow open   customer 95SQ4TSUT7mWBT7VNHH67A   5   1          0            0       260b           260b

```
두번째 커멘드의 결과는 우리에게 "customer" 라는 이름의 하나의 인덱스가 있다는 것을 말해주고, 다섯개의 샤드들과 1 레플리카 (default) 를 가지고 있으며 안에 0개의 도큐먼트가 있다는 것을 알 수 있습니다.

당신은 아마도 customer 인덱스가 yellow health 로 태깅된 것을 눈치채셧을 것입니다. 이전의 문서에서 yellow 는 몇몇 레플리카가 아직 할당되지 않았다는 것을 의미합니다. 이 인덱스에 대해 이런 현상이 일어나는 이유는 Elasticsearch 는 default 로 한개의 레플리카를 만들어내기 때문입니다. 우리가 현재 실행중이 노드를 하나만 가지고 있기 때문에, 다른 노드가 클러스터에 join 할 때까지 해당 레플리카를 아직 (고 가용성을 위해) 할당 할 수 없습니다. 레플리카가 두 번째 노드에 할당되면 상태가 green으로 바뀝니다.
