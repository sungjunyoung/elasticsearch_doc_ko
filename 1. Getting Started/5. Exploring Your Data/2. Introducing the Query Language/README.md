> [Getting Started](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started) > [Exploring Your Data](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started/5.%20Exploring%20Your%20Data) > Introducing the Query Language  
> 원본 : https://www.elastic.co/guide/en/elasticsearch/reference/current/_introducing_the_query_language.html

## The Search API

Elasticsearch 는 당신이 쿼리를 실행시킬 수 있는 JSON 스타일의 도메인 기준의 [Query DSL](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html)이라고 부르는 언어를 제공합니다. 쿼리 언어는 매우 포괄적이어서 처음 보면 두려워 할 수 있지만 실제로 배울 수있는 가장 좋은 방법은 몇 가지 기본 예제부터 시작하는 것입니다.

우리의 마지막 예제로 돌아가 봅시다. 우리는 다음의 쿼리를 실행시켰습니다.
```json
GET /bank/_search
{
  "query": { "match_all": {} }
}
```
하나하나 살펴봅시다. query 필드는 쿼리로 무엇을 날릴 것인지에 대한 정의입니다. match_all 필드는 우리가 실행시키려는 쿼리의 타입입니다. match_all 쿼리는 단순히 지정된 인덱스(bank) 에 대해 모든 도큐먼트를 검색합니다.

그리고, 다른 파라미터를 넘김으로서 우리의 검색 결과에 영향을 줄 수 있습니다. 예를들어, 우리는 size 를 넘길것입니다.
```json
GET /bank/_search
{
  "query": { "match_all": {} },
  "size": 1
}
```
> size 를 지정하지 않으면 default 는 10 이 됩니다.

이 예제는 도큐먼트 11부터 20까지를 리턴합니다.
```json
GET /bank/_search
{
  "query": { "match_all": {} },
  "from": 10,
  "size": 10
}
```
from 파라미터는 (default: 0) 시작할 도큐먼트의 인덱스를 지정할 수 있습니다. size 파라미터 (default: 10) 는 리턴할 도큐먼트의 갯수를 지정합니다. 검색 결과에 대한 paging 기능을 구현할 떄 유용하게 사용할 수 있습니다.

다음의 예제는 결과를 balance 기준으로 내림차순 정렬하여 디폴트인 10개의 도큐먼트를 리턴합니다.
```json
GET /bank/_search
{
  "query": { "match_all": {} },
  "sort": { "balance": { "order": "desc" } }
}
```
