> [Getting Started](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started) > [Exploring Your Data](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started/5.%20Exploring%20Your%20Data) > Executing Searches
> 원본 : https://www.elastic.co/guide/en/elasticsearch/reference/current/_executing_searches.html

## Executing Searches

우리는 몇개의 검색 파라미터를 알아보았습니다. 이제 Query DSL 을 조금 더 심화해봅시다. 리턴된 도큐먼트 필드를 보겠습니다. 기본적으로, 전체 JSON 도큐먼트가 검색의 일부로 리턴됩니다. 도큐먼트의 일부분의 소스만 리턴되기를 원한다면 이것을 \_source 필드로 지정할 수 있습니다.

이 예제는 어떻게 account_number 와 balance 필드만 리턴할 수 있는지 보여줍니다. 검색에서,
```json
GET /bank/_search
{
  "query": { "match_all": {} },
  "_source": ["account_number", "balance"]
}
```
> 위의 예제는 단순히 \_source 필드를 줄입니다. \_source라는 필드 하나만 반환하지만 account_number 및 balance 필드는 포함됩니다.

만약 당신이 SQL 을 경험해 보았다면, SELECT FROM 구문과 유사한 컨셉이라는 것을 알아차릴 수 있을 것입니다.

이제, query 필드로 넘어가 봅시다. 우리는 이전에 모든 도큐먼트를 불러오기 위해 match_all 쿼리를 사용해 보았습니다. 이제는, match 라고 불리는 새로운 쿼리를 소개합니다. 이 쿼리는 기본 필드가 지정된 검색 쿼리 (즉, 특정 필드 나 필드 집합에 대해 일치하는 것을 찾는 검색)로 생각할 수 있습니다.

account_number 가 20인 도큐먼트를 리턴해 봅시다.
```json
GET /bank/_search
{
  "query": { "match": { "account_number": 20 } }
}
```
아래 예제는 address 에 'mill' 이라는 단어가 들어간 모든 도큐먼트를 리턴합니다.
```json
GET /bank/_search
{
  "query": { "match": { "address": "mill" } }
}
```
아래의 예제는 address 에 'mill' 또는 'lane' 이 들어간 모든 도큐먼트를 리턴합니다.
```json
GET /bank/_search
{
  "query": { "match": { "address": "mill lane" } }
}
```
다음의 예제는 주소에 'mill lane' 이라는 구문을 포함하는 모든 계정을 반환하는 match 의 변형된 쿼리입니다.
```json
GET /bank/_search
{
  "query": { "match_phrase": { "address": "mill lane" } }
}
```
다음은 [bool(ean) query](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-bool-query.html)를 소개합니다. bool 쿼리를 사용하면 참/거짓 논리를 사용하여보다 작은 쿼리를 더 큰 쿼리로 작성할 수 있습니다.

다음의 예제는 두개의 match 쿼리들로 작성되어 있으며, address에 'mill'과 'lane' 을 동시에 포함하는 도큐먼트를 모두 반환합니다.
```json
GET /bank/_search
{
  "query": {
    "bool": {
      "must": [
        { "match": { "address": "mill" } },
        { "match": { "address": "lane" } }
      ]
    }
  }
}
```
위의 예제에서, bool - must 안의 모든 쿼리가 true 인 도큐먼트를 리턴합니다.

대조적으로, 다음의 예제는 두개의 match 쿼리들로 작성되어 있으며, address 에 'mill' 또는 'lane'을 포함하는 도큐먼트를 모두 반환합니다.
```json
GET /bank/_search
{
  "query": {
    "bool": {
      "should": [
        { "match": { "address": "mill" } },
        { "match": { "address": "lane" } }
      ]
    }
  }
}
```
위의 예제에서, bool - should 안의 쿼리 중 하나라도 true 인 도큐먼트를 리턴하게 됩니다.

이번 예제는 또다시 두개의 match 쿼리들로 작성되어 있으며, address에 'mill' 또는 'lane' 을 포함하지 않는 도큐먼트를 모두 반환합니다.

```json
GET /bank/_search
{
  "query": {
    "bool": {
      "must_not": [
        { "match": { "address": "mill" } },
        { "match": { "address": "lane" } }
      ]
    }
  }
}
```
위의 예제에서는,  bool - must_not 안의 쿼리 중 아무것도 true 가 아닌 도큐먼트를 리턴합니다.

우리는 must, should, must_not 구문들을 bool 쿼리 안에 적절하게 조합해 사용할 수 있습니다. 게다가, multi-level의 boolean 로직을 모방하기 위해 우리는 bool 쿼리를 bool 쿼리 안에서 조합할 수 있습니다.

다음은 40살이지만, ID 주(state) 에는 살지 않는 모든 도큐먼트를 리턴합니다.
```json
GET /bank/_search
{
  "query": {
    "bool": {
      "must": [
        { "match": { "age": "40" } }
      ],
      "must_not": [
        { "match": { "state": "ID" } }
      ]
    }
  }
}
```
