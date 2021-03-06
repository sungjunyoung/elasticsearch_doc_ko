> [Getting Started](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started) > Exploring Your Cluster  
> 원본 : https://www.elastic.co/guide/en/elasticsearch/reference/current/_exploring_your_cluster.html

### Exploring Your Cluster

#### The REST API
이제 우리는 우리의 노드(그리고 클러스터) 를 가지고 있으며, 실행 중입니다. 다음 단계는 어떻게 이 노드와 커뮤니케이션 하는지 알아보는 것입니다. 다행히도, Elasticsearch 는 당신의 클러스터와 상호작용 할수 있는 매우 광범위하고 파워풀한 REST API 를 제공합니다. API로 수행할 수 있는 몇가지의 작업은 다음과 같습니다.

- 당신의 클러스터, 노드, 그리고 인덱스의 health, 상태, 그리고 통계를 체크할 수 있습니다.
- 당신의 클러스터, 노드, 그리고 인덱스 데이터와 메타데이터를 관리할 수 있습니다.
- CRUD (Create, Read, Update, and Delete) 를 수행하고, 당신의 인덱스에 대해 명령을 검색할 수 있습니다.
- 페이징, 정렬, scripting, aggregations 등과 같은 고급 검색 명령을 수행할 수 있습니다.
