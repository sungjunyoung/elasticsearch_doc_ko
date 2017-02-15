> [Getting Started](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started) > [Exploring Your Cluster](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started/3.%20Exploring%20Your%20Cluster) > Cluster Health  
> 원본 : https://www.elastic.co/guide/en/elasticsearch/reference/current/_cluster_health.html


### Cluster Health

우리의 클러스터가 어떻게 하고 있는지 볼 수 있는 기본적인 health check 로 시작해 봅시다. 우리는 curl 을 사용할 것입니다. 하지만, HTTP/REST 호출을 할수 있는 어떤 툴이든 사용 가능합니다. 우리가 아직 Elasticsearch를 시작했던 그 노드에 있고, command shell 이 열려있다고 가정합니다.

클러스터 health 를 체크하기 위해서는 우리는 [_cat API](https://www.elastic.co/guide/en/elasticsearch/reference/current/cat.html)를 사용합니다. 아래의 커맨드를 [Kibana 콘솔](https://www.elastic.co/guide/en/kibana/5.2/console-kibana.html)에서 "VIEW IN CONSOLE" 을 클릭함으로서 실행하거나, curl 을 복사해 터미널에 붙여넣음으로서 실행할 수 있습니다.
> 해당 문서에서는 못합니다 ㅠ

```
GET /_cat/health?v
```
Response 는 다음과 같습니다
```
epoch      timestamp cluster       status node.total node.data shards pri relo init unassign pending_tasks max_task_wait_time active_shards_percent
1475247709 17:01:49  elasticsearch green           1         1      0   0    0    0        0             0                  -                100.0%

```
"elasticsearch" 라는 이름의 클러스터가 green status 로 올라가 있는 것을 볼 수 있습니다.

언제든지 클러스터의 health 를 질의하면 green, yello, red 중 하나의 status 를 받게 됩니다. green 은 클러스터가 모든 것이 정상이라는 의미이고, yellow 는 모든 데이터가 이용가능하나 몇개의 레플리카들이 아직 할당되지 않았다는 것을 의미합니다. 그리고 red 는 몇개의 데이터가 어떠한 이유로 이용가능하지 않다는 것을 의미합니다. 클러스터 상태가 red 라도, 이것은 아직 부분적으로는 이용가능합니다. 그러나 데이터 손실 가능성이 있기 때문에 가능한 빨리 고쳐야 합니다.

위의 response 에서, 우리는 1개의 노드를 볼 수 있고, 아직 데이터가 없기 때문에 0개의 샤드를 가지고 있다는 것을 알 수 있습니다. 기본 클러스터 이름 (elasticsearch)을 사용하고, Elasticsearch가 기본적으로 unicast(?) 네트워크 검색을 사용하여 같은 컴퓨터에서 다른 노드를 찾았으므로 실수로 컴퓨터에서 둘 이상의 노드를 시작해 두개의 노드 모두 하나의 클러스터에 묶여 있게 될 가능성이 있습니다. 이 시나리오에서는, 당신은 1개 위의 response 에서 한 개 이상의 노드를 볼 수 있습니다.

다음의 명령에서, 클러스터 내의 노드 리스트를 얻을 수 있습니다.
```
GET /_cat/nodes?v
```
Response 는 다음과 같습니다.
```
ip        heap.percent ram.percent cpu load_1m load_5m load_15m node.role master name
127.0.0.1           10           5   5    4.46                        mdi      *      PB2SGZY
```

여기서 우리는 "PB2SGZY" 라는 단일 노드를 볼수 있습니다. 우리의 클러스터 내에 하나의 노드가 존재한다는 뜻입니다.
