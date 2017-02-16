> [Getting Started](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started) > [Exploring Your Data](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started/5.%20Exploring%20Your%20Data) > The Search API  
> 원본 : https://www.elastic.co/guide/en/elasticsearch/reference/current/_the_search_api.html

## The Search API

이제 몇개의 간단한 검색을 시작해 보겠습니다. 두가지 검색 방법이 있습니다. 그중 하나는 검색 파라미터를 [REST request URI](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-uri-request.html)를 통해 보내는 것이고, 다른 하나는 [REST request body](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-request-body.html)를 통해 보내는 것입니다. request body 메서드는 더 표현 가능하게 하며, 좀더 읽기쉬운 JSON 포맷으로 당신의 검색을 정의해줍니다. 우리는 request URI 메서드의 한 가지 예를 시도 할 것이지만, 이 튜토리얼의 나머지 부분에서는 request body 메서드 만 사용할 것입니다.

검색 용 REST API는 \_search 엔드 포인트에서 액세스 할 수 있습니다. 이 예에서는 은행 인덱스의 모든 문서를 반환합니다.
```
GET /bank/_search?q=*&sort=account_number:asc&pretty
```
위 예제를 분리해서 생각해봅시다. 우리는 bank 인덱스에서 검색하는 중이며, q=* 파라미터는 Elasticsearch가 인덱스의 모든 문서를 불러오도록 지시합니다. sort=account_number 파라미터는 결과를 account_number 필드에 따라 오름차순으로 정렬하도록 지시합니다. pretty 파라미터는, 알다시피 JSON 결과를 예쁘게 출력하도록 합니다.

다음은 그에대한 Response 입니다.
```json
{
  "took" : 63,
  "timed_out" : false,
  "_shards" : {
    "total" : 5,
    "successful" : 5,
    "failed" : 0
  },
  "hits" : {
    "total" : 1000,
    "max_score" : null,
    "hits" : [ {
      "_index" : "bank",
      "_type" : "account",
      "_id" : "0",
      "sort": [0],
      "_score" : null,
      "_source" : {"account_number":0,"balance":16623,"firstname":"Bradshaw","lastname":"Mckenzie","age":29,"gender":"F","address":"244 Columbus Place","employer":"Euron","email":"bradshawmckenzie@euron.com","city":"Hobucken","state":"CO"}
    }, {
      "_index" : "bank",
      "_type" : "account",
      "_id" : "1",
      "sort": [1],
      "_score" : null,
      "_source" : {"account_number":1,"balance":39225,"firstname":"Amber","lastname":"Duke","age":32,"gender":"M","address":"880 Holmes Lane","employer":"Pyrami","email":"amberduke@pyrami.com","city":"Brogan","state":"IL"}
    }, ...
    ]
  }
}
```
response 에서, 우리는 다음을 찾을 수 있습니다.
- took : millisecond 단위의 Elasticsearch가 검색하는데 수행된 시간입니다.
- timed_out : time out 인지 아닌지 말해줍니다.
- \_shards : 얼마나 많은 샤드가 검색됬는지 뿐만 아니라, 검색된 샤드의 성공 여부의 갯수를 말해줍니다.
- hits : 검색 결과
- hits.total : 쿼리에 매칭된 검색 결과의 전체 갯수입니다.
- hits.hits : 검색 결과의 실제 배열입니다. (default : 처음으로부터 10개의 배열)
- hits.sort : 결과의 정렬 키 (score 로 정렬되었다면 없습니다.(?))
- hits.\_score and max_score : 지금은 무시하세요.

다음은 request body method 를 사용한 위와 동일한 검색입니다.
```json
GET /bank/_search
{
  "query": { "match_all": {} },
  "sort": [
    { "account_number": "asc" }
  ]
}
```
> **역자주**  
> POST 로 쏴도 같은 결과가 나옵니다.  

여기서 다른 점은  q=* 를 넘겨주는 대신, JSON-style 의 쿼리 requst body 를 \_search API 로 보냈습니다. 우리는 다음 섹션에서 이 JSON 쿼리에 이야기해볼 것ㅂ입니다.

일단 당신이 검색 결과를 받으면, Elasticsearch request 요청을 완전히 끝낸 것이며, 어떠한 서버측 리소스도 가지고 있지 않습니다. 이것은 원하는 다른 결과를 얻기 위해 서버와 계속적으로 통신해야 하는 SQL 과는 극명히 대조됩니다.(?)
