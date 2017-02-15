> [Getting Started](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started) > [Modifying Your Data](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started/4.%20Modifying%20Your%20Data) > Deleting Documents
> 원본 : https://www.elastic.co/guide/en/elasticsearch/reference/current/_deleting_documents.html

### Deleting Documents

도큐먼트를 삭제하는것은 매우 간단합니다. 다음의 예제는 ID 2 의 customer 를 삭제하는 방법을 보여줍니다.

```
DELETE /customer/external/2?pretty
```

특정 쿼리와 일치하는 모든 도큐먼트를 삭제하는 방법에 대해서는 다음 [Delete By Query API](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-delete-by-query.html) 을 참고하십시오. Delete By Query API를 사용하여 모든 문서를 삭제하는 대신 전체 색인을 삭제하는 것이 훨씬 더 효율적입니다.
