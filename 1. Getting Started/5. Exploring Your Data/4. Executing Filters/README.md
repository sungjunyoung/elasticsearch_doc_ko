> [Getting Started](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started) > [Exploring Your Data](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started/5.%20Exploring%20Your%20Data) > Executing Filters  
> 원본 : https://www.elastic.co/guide/en/elasticsearch/reference/current/_executing_filters.html

## Executing Searches

이전 섹션에서, 우리는 검색 결과의 \_score 필드에 대한 설명을 조금 건너 뛰었습니다. score 는 도큐먼트가 얼마나 검색 쿼리에 적합한지에 대한 숫자로 된 값입니다. 높은 score 를 가질수록 도큐먼트의 관련성이 높아집니다.

그러나 도큐먼트 집합을 "필터링"하는 데에만 사용되는 경우 스코어를 생성 할 필요가 없습니다. Elasticsearch는 이러한 상황을 감지하고 쓸모없는 점수를 계산하지 않도록 쿼리 실행을 자동으로 최적화합니다.

이젠 섹션에서 소개했던 [bool query](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-bool-query.html)도 역시 filter 구문을 지원합니다. 필터 절을 지원하므로 쿼리를 사용하여 score 계산 방법을 변경하지 않고도 다른 절과 일치하는 도큐먼트를 제한 할 수 있습니다(?). 예를들어 [range query](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-range-query.html)를 소개합니다. range query 는 값의 범위로 도큐먼트를 필터링 할 수 있게 합니다. 주로 수치 데이터에 대해서 많이 사용합니다.

다음은 balance 가 20000과 30000 사이인 모든 도큐먼트 (유저)를 반환하는 예제입니다.  
> gte : greater than or equal  
> lte : less than or equel

```json
GET /bank/_search
{
  "query": {
    "bool": {
      "must": { "match_all": {} },
      "filter": {
        "range": {
          "balance": {
            "gte": 20000,
            "lte": 30000
          }
        }
      }
    }
  }
}
```
위의 명령을 뜯어보면, bool 쿼리는 match_all 쿼리와 range 쿼리로 이루어져 있습니다.

match_all, match, bool 및 range 쿼리 외에도 사용할 수있는 다른 많은 쿼리들이 있지만, 여기서는 다루지 않을 것입니다. 어떻게 작동하는지에 대한 기본적인 이해가 이미 있으므로 다른 지식 유형을 배우고 실험 할 때 이 지식을 적용하는 것은 별로 어렵지 않을 것입니다.
