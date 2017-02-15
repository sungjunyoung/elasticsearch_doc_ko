> [Getting Started](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started) > Modifying Your Data
> 원본 : https://www.elastic.co/guide/en/elasticsearch/reference/current/_modifying_your_data.html

### Modifying Your Data

Elasticsearch 는 리얼타임 환경에서의 데이터 수정과 검색을 제공합니다. 기본적으로, 데이터를 색인 / 업데이트 / 삭제할 때부터 검색 결과에 표시 될 때까지 1 초 정도의 지연 (새로고침 간격)이 있습니다. 이는 트랜잭션 완료 후 즉시 데이터를 사용할 수있는 SQL과 같은 다른 플랫폼과 중요한 차이가 있습니다.

#### Indexing/Replace Documents

이전에 오리는 어떻게 단일 도큐먼트를 인덱싱 하는지 살펴보았습니다. 그 커맨드를 다시한번 살펴봅시다.
```json
PUT /customer/external/1?pretty
{
  "name": "성준영"
}
```
다시한번 customer 인덱스에 도큐먼트를 external 타입으로, 1 ID를 주고 인덱싱 하였습니다. 만약 우리가 다시한번 위의 커멘드를 다른 도큐먼트로 실행한다면, Elasticsearch는 해당 ID 의 도큐먼트를 덮어쓸 것입니다.
```json
PUT /customer/external/1?pretty
{
  "name": "김예슬"
}
```
위의 커멘드는 ID 1 의 도큐먼트를 "성준영"에서 "김예슬" 으로 바꿔줍니다. 만약 우리가 다른 ID 를 사용한다면, 새로운 도큐면트가 인덱싱 되고, 기존 ID 1의 도큐먼트는 변하지 않은 채로 남아있을 것입니다.
```json
PUT /customer/external/2?pretty
{
  "name": "성준영"
}
```
위의 커맨드는 ID 2 의 새로운 도큐먼트를 인덱싱 할 것입니다.

인덱싱 할때, ID 부분은 optional 입니다. Elasticsearch가 랜덤한 ID를 생성하고, 도큐먼트를 인덱싱 하기 위해 사용할 것입니다. Elasticsearch가 생성 한 실제 ID (또는 이전 예제에서 명시 적으로 지정한 항목)는 인덱스 API 호출의 일부로 리턴됩니다.

다음의 예제는 특정한 ID 없이 도큐먼트를 인덱싱 하는 방법을 보여줍니다.
```json
POST /customer/external?pretty
{
  "name": "성준영"
}
```
이 경우 PUT 대신 POST 메소드를 쓴다는 점에 유의하세요.
