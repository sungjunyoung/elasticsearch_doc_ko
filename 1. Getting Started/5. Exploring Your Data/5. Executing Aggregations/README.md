> [Getting Started](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started) > [Exploring Your Data](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started/5.%20Exploring%20Your%20Data) > Executing Aggregations  
> 원본 : https://www.elastic.co/guide/en/elasticsearch/reference/current/_executing_aggregations.html#_executing_aggregations

## Executing Aggregations

Aggregation 은 당신의 데이터에서 수치를 뽑아내거나, 그룹을 짓는 등의 능력을 제공합니다. 가장 쉽게 Aggregation 을 이해하는 방법은 SQL의 GROUP BY 구문을 생각하는 것입니다. Elasticsearch에서, 당신은 결과를 (hits) 반환하는 검색 수행 능력을 가지며, 동시에 aggregate 된 결과를 hits 과는 별개로 한번의 응답으로 받을 수 있습니다. 이것은 단 한번의 API 커넥션으로 다중의 aggregation에 대한 결과와 쿼리에 대한 결과를 동시에 받을 수 있다는 점에서 매우 강력하며, 효율적입니다.

다음의 모든 도큐먼트들을 state 로 묶고, 그리고 갯수에 따른 내림차순(default) 으로 10개(default) 를 출력하는 예제입니다.
```json
GET /bank/_search
{
  "size": 0,
  "aggs": {
    "group_by_state": {
      "terms": {
        "field": "state.keyword"
      }
    }
  }
}
```
SQL 문에서는, 위의 Aggregation 은 다음의 구문으로 나타낼 수 있습니다.
```SQL
SELECT state, COUNT(*) FROM bank GROUP BY state ORDER BY COUNT(*) DESC
```
그리고 그에대한 응답입니다. (부분적으로 보여드립니다.)
```json
{
  "took": 29,
  "timed_out": false,
  "_shards": {
    "total": 5,
    "successful": 5,
    "failed": 0
  },
  "hits" : {
    "total" : 1000,
    "max_score" : 0.0,
    "hits" : [ ]
  },
  "aggregations" : {
    "group_by_state" : {
      "doc_count_error_upper_bound": 20,
      "sum_other_doc_count": 770,
      "buckets" : [ {
        "key" : "ID",
        "doc_count" : 27
      }, {
        "key" : "TX",
        "doc_count" : 27
      }, {
        "key" : "AL",
        "doc_count" : 25
      }, {
        "key" : "MD",
        "doc_count" : 25
      }, {
        "key" : "TN",
        "doc_count" : 23
      }, {
        "key" : "MA",
        "doc_count" : 21
      }, {
        "key" : "NC",
        "doc_count" : 21
      }, {
        "key" : "ND",
        "doc_count" : 21
      }, {
        "key" : "ME",
        "doc_count" : 20
      }, {
        "key" : "MO",
        "doc_count" : 20
      } ]
    }
  }
}
```
우리는 ID (Idaho)주에 27명의 고객, TX(Texas)주에 27명의 고객이 있다는 것 등을 알수 있습니다.

> aggregation 에 대한 결과만 보고 싶었기 때문에 size=0 으로 지정했습니다.

다음의 예제는 state 별 평균 잔액을 계산합니다 (내림차순으로 된 상위 10 개 state).
```json
GET /bank/_search
{
  "size": 0,
  "aggs": {
    "group_by_state": {
      "terms": {
        "field": "state.keyword"
      },
      "aggs": {
        "average_balance": {
          "avg": {
            "field": "balance"
          }
        }
      }
    }
  }
}
```
group_by_state 안의 average_balance 를 포함시킨 것에 주목하세요. 이것은 모든 aggregation 의 공통된 패턴입니다. 우리는 원하는 데로 aggregation 에 aggregation 구문을 포함시킬 수 있습니다.

아래의 aggregation을 작성함으로서, 평균 잔액을 내림차순으로 정렬해 봅시다.
```json
GET /bank/_search
{
  "size": 0,
  "aggs": {
    "group_by_state": {
      "terms": {
        "field": "state.keyword",
        "order": {
          "average_balance": "desc"
        }
      },
      "aggs": {
        "average_balance": {
          "avg": {
            "field": "balance"
          }
        }
      }
    }
  }
}
```

다음의 예제는 20~29세, 30~39세, 40~49세 같은 방식과 함께 성(gender)으로 구분짓는 방법을 보여줍니다. 그리고 마지막에는 평균 잔액을 나이 범위별, 성별로 보여줍니다.

```json
GET /bank/_search
{
  "size": 0,
  "aggs": {
    "group_by_age": {
      "range": {
        "field": "age",
        "ranges": [
          {
            "from": 20,
            "to": 30
          },
          {
            "from": 30,
            "to": 40
          },
          {
            "from": 40,
            "to": 50
          }
        ]
      },
      "aggs": {
        "group_by_gender": {
          "terms": {
            "field": "gender.keyword"
          },
          "aggs": {
            "average_balance": {
              "avg": {
                "field": "balance"
              }
            }
          }
        }
      }
    }
  }
}
```

여기서 자세히 설명하지 않는 다른 많은 aggregation 기능이 있습니다. 더 많은 예제는 [aggregations reference guide](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations.html) 를 참고하세요.
