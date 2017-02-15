> [Getting Started](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/Getting%20Started) > [Exploring Your Cluster](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/Getting%20Started/Exploring%20Your%20Cluster) > Cluster Health  
> ORIGINAL : https://www.elastic.co/guide/en/elasticsearch/reference/current/_cluster_health.html


### Cluster Health

우리의 클러스터가 어떻게 하고 있는지 볼 수 있는 기본적인 health check 로 시작해 봅시다. 우리는 curl 을 사용할 것입니다. 하지만, HTTP/REST 호출을 할수 있는 어떤 툴이든 사용 가능합니다. 우리가 아직 Elasticsearch를 시작했던 그 노드에 있고, command shell 이 열려있다고 가정합니다.

클러스터 health 를 체크하기 위해서는 우리는 [_cat API](https://www.elastic.co/guide/en/elasticsearch/reference/current/cat.html)를 사용합니다. 아래의 커맨드를 [Kibana 콘솔](https://www.elastic.co/guide/en/kibana/5.2/console-kibana.html)에서 "VIEW IN CONSOLE" 을 클릭함으로서 실행하거나, curl 을 복사해 터미널에 붙여넣음으로서 실행할 수 있습니다.
> 해당 문서에서는 못합니다 ㅠ

```bash
GET /_cat/health?v
```
