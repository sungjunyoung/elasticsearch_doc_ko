> [Getting Started](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started) > [Modifying Your Data](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started/4.%20Modifying%20Your%20Data) > Batch Processing
> 원본 : https://www.elastic.co/guide/en/elasticsearch/reference/current/_batch_processing.html

### Batch Processing

도큐먼트를 인덱싱하고, 업데이트하고, 삭제하는 것 뿐만 아니라, Elasticsearch는 [\_bulk API](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-bulk.html) 를 사용하여 위의 작업들을 배치로 수행 할 수 있는 기능을 제공합니다. 이 기능은 최대한 적은 네트워크의 통신으로 가능한 빠르게 여러 작업을 수행할 수 있는 매우 효율적인 매커니즘을 제공한다는 점에서 중요합니다.

빠른 예제로, 하나의 명령에서 두개의 도큐먼트를 인덱싱하는 것을 보겠습니다. (ID 1 - 성준영, ID 2 - 김예슬)
```json
POST /customer/external/_bulk?pretty
{"index":{"_id":"1"}}
{"name": "성준영" }
{"index":{"_id":"2"}}
{"name": "김예슬" }
```
다음의 예제는 ID 1 의 도큐먼트를 업데이트하고, ID 2 의 도큐먼트를 삭제하는 하나의 명령을 보여줍니다.
```json
POST /customer/external/_bulk?pretty
{"update":{"_id":"1"}}
{"doc": { "name": "성준영 becomes 김예슬" } }
{"delete":{"_id":"2"}}
```
삭제 할때는 해당 도큐먼트의 ID 만 알면 됩니다.

Bulk API 는

Bulk API는 작업 중 하나의 명령이 실패했다고 실패하지 않습니다. 어떠한 이유에서 건 하나의 명령이 실패하면, 그 다음에 나머지 명령을 계속해서 처리합니다. 대량 API가 반환되면 각 액션에 대한 상태가 (전송 된 순서대로) 제공되므로 특정 액션이 실패했는지 여부를 확인할 수 있습니다.
