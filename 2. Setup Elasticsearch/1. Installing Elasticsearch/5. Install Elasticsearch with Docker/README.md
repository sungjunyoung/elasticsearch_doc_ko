> [Setup Elasticsearch]() > [Installing Elasticsearch](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/2.%20Setup%20Elasticsearch/1.%20Installing%20Elasticsearch) > Install Elasticsearch with Docker  
> 원본 : https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html

### Install Elasticsearch with Docker
Elasticsearch 는 Docker 이미지로도 제공됩니다. 이미지는 X-Pack 으로 제작되어있습니다.

#### Security Notes
> [X-Pack](https://www.elastic.co/guide/en/x-pack/5.2/index.html)은 이 이미지 내에서 이미 인수톨 되어 있습니다. [X-Pack Security](https://www.elastic.co/guide/en/x-pack/5.2/security-getting-started.html)와, 어떻게 기본 비밀번호를 변경하는지에 대해 친숙해 지고 사용해주시기 바랍니다. elastic 유저의 기본 비밀번호는 changeme 입니다.

> X-Pack 은 30일 trial licence 를 포함하고 있습니다. 그 이후에는, [available subcriptions](https://www.elastic.co/subscriptions)로 구독하거나, [disable Security](https://www.elastic.co/guide/en/x-pack/5.2/security-settings.html) 해야합니다. 기본 라이센스는 무료로 제공되며, [Monitoring](https://www.elastic.co/products/x-pack/monitoring) 확장팩을 포함하고 있습니다.

`docker pull` 커맨드로 간단하게 Docker 로 Elasticsearch 를 설치할 수 있습니다.  

다음의 커멘드로 Docker 이미지를 얻을 수 있습니다.

```sh
docker pull docker.elastic.co/elasticsearch/elasticsearch:5.2.1
```

#### Running Elasticsearch from the command line
##### Developing Mode
Elasticsearch 는 개발이나 테스트하기위해 다음의 커맨드로 쉽게 시작할 수 있습니다.
```
docker run -p 9200:9200 -e "http.host=0.0.0.0" -e "transport.host=127.0.0.1" docker.elastic.co/elasticsearch/elasticsearch:5.2.1
```

##### Production Mode
