> [Getting Started](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started) > Exploring Your Data  
> 원본 : https://www.elastic.co/guide/en/elasticsearch/reference/current/_exploring_your_data.html

## Exploring Your Data

### Sample Dataset

이제 기본 사항을 엿볼 수있게되었으므로, 보다 현실적인 데이터 세트로 작업 해 보겠습니다. 고객 은행 계좌 정보에 대한 가상의 JSON 문서 샘플을 준비했습니다. 각 문서에는 다음과 같은 스키마가 있습니다.

```json
{
    "account_number": 0,
    "balance": 16623,
    "firstname": "Bradshaw",
    "lastname": "Mckenzie",
    "age": 29,
    "gender": "F",
    "address": "244 Columbus Place",
    "employer": "Euron",
    "email": "bradshawmckenzie@euron.com",
    "city": "Hobucken",
    "state": "CO"
}
```
http://www.json-generator.com/ 에서 데이터를 생성 했으므로 데이터의 실제 값과 의미가 무작위로 생성되더라도 무시하세요.

### Loading the Sample Dataset

[여기](https://raw.githubusercontent.com/elastic/elasticsearch/master/docs/src/test/resources/accounts.json)에서 샘플 데이터 셋(accounts.json)을 다운로드 할 수 있습니다. 다운로드 한 파일을 현재 디렉토리로 추출하고 다음과 같이 클러스터에 로드합니다.
```
curl -XPOST 'localhost:9200/bank/account/_bulk?pretty&refresh' --data-binary "@accounts.json"
curl 'localhost:9200/_cat/indices?v'
```
다음은 Response 입니다.
```
health status index uuid                   pri rep docs.count docs.deleted store.size pri.store.size
yellow open   bank  l7sSYV2cQXmu6_4rJWVIww   5   1       1000            0    128.6kb        128.6kb

```
같은 결과가 나왔다면, account 타입으로 1000개의 도큐먼트를 bank 인덱스에 성공적으로 인덱싱 한 것입니다.
