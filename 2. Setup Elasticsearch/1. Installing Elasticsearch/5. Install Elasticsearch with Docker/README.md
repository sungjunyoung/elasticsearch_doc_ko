> [Setup Elasticsearch]() > [Installing Elasticsearch](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/2.%20Setup%20Elasticsearch/1.%20Installing%20Elasticsearch) > Install Elasticsearch with Docker  
> 원본 : https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html

### Install Elasticsearch with Docker
Elasticsearch 는 Docker 이미지로도 제공됩니다. 이미지는 X-Pack 으로 제작되어있습니다.

#### Security Notes
> [X-Pack](https://www.elastic.co/guide/en/x-pack/5.2/index.html)은 이 이미지 내에서 이미 인스톨 되어 있습니다. [X-Pack Security](https://www.elastic.co/guide/en/x-pack/5.2/security-getting-started.html)와, 어떻게 기본 비밀번호를 변경하는지에 대해 친숙해 지고 사용해주시기 바랍니다. elastic 유저의 기본 비밀번호는 changeme 입니다.

> X-Pack 은 30일 trial licence 를 포함하고 있습니다. 그 이후에는, [available subcriptions](https://www.elastic.co/subscriptions)로 구독하거나, [disable Security](https://www.elastic.co/guide/en/x-pack/5.2/security-settings.html) 해야합니다. 기본 라이센스는 무료로 제공되며, [Monitoring](https://www.elastic.co/products/x-pack/monitoring) 확장팩을 포함하고 있습니다.

`docker pull` 커맨드로 간단하게 Docker 로 Elasticsearch 를 설치할 수 있습니다.  

다음의 커멘드로 Docker 이미지를 얻을 수 있습니다.

```sh
docker pull docker.elastic.co/elasticsearch/elasticsearch:5.2.1
```

#### Running Elasticsearch from the command line
##### Developing Mode
Elasticsearch 는 개발이나 테스트를 위해 다음의 커맨드로 쉽게 시작할 수 있습니다.
```
docker run -p 9200:9200 -e "http.host=0.0.0.0" -e "transport.host=127.0.0.1" docker.elastic.co/elasticsearch/elasticsearch:5.2.1
```

##### Production Mode
> **Important**  
> 프로덕션 용도로 사용 시 `vm_max_map_count` 커널 설정을 최소 262144 이상으로 설정해야 합니다. (?)
> 당신의 플랫폼에 따라 달라집니다.
> - Linux  
> /etc/sysctl.conf 에서 설정할 수 있습니다.  
> `$grep vm.max_map_count /etc/sysctl.conf`  
> `vm.max_map_count=262144`  
> live system type 에서 : `sysctl -w vm.max_map_count=262144`
> - OSX with [Docker for Mac](https://docs.docker.com/docker-for-mac/)  
> vm_max_map_count 세팅은 xhyve 가상머신 안에 설정해야 합니다.  
> `$screen ~/Library/Containers/com.docker.docker/Data/com.docker.driver.amd64-linux/tty`  
> 패스워드 없이 `root`로 접속 후에, 리눅스와 마찬가지로 `sysctl` 세팅을 설정하세요.  
> `sysctl -w vm.max_map_count=262144`
> - [Docker Toolbox](https://docs.docker.com/docker-for-mac/) OSX  
> vm_max_count 세팅은 docker-machine 에서 이루어져야 합니다.
> `docker-machine ssh`
> `sudo sysctl -w vm.max_map_count=262144`

다음 예제에서는 두 개의 Elasticsearch 노드로 구성된 클러스터를 표시합니다. 클러스터를 가져 오려면 docker-compose.yml을 사용하고 다음을 입력하십시오.
```
docker-compose up
```

> docker-compose 는 리눅스에서 사전 인스톨 되어있지 않습니다. 설치 방법은 [docker-compose webpage](https://docs.docker.com/compose/install/#install-using-pip)를 참고하십시오.

elasticsearch1 노드는 localhost:9200에서 수신 대기하고 elasticsearch2는 Docker 네트워크에서 elasticsearch1과 통신합니다.

이 예제에서는 eserata1 및 esdata2라는 Docker 볼륨도 사용합니다 (아직없는 경우 생성됩니다).

`docker-compose.yml`:

```yaml
version: '2'
services:
  elasticsearch1:
    image: docker.elastic.co/elasticsearch/elasticsearch:5.2.1
    container_name: elasticsearch1
    environment:
      - cluster.name=docker-cluster
      - bootstrap.memory_lock=true
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    ulimits:
      memlock:
        soft: -1
        hard: -1
      nofile:
        soft: 65536
        hard: 65536
    mem_limit: 1g
    cap_add:
      - IPC_LOCK
    volumes:
      - esdata1:/usr/share/elasticsearch/data
    ports:
      - 9200:9200
    networks:
      - esnet
  elasticsearch2:
    image: docker.elastic.co/elasticsearch/elasticsearch:5.2.1
    environment:
      - cluster.name=docker-cluster
      - bootstrap.memory_lock=true
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
      - "discovery.zen.ping.unicast.hosts=elasticsearch1"
    ulimits:
      memlock:
        soft: -1
        hard: -1
      nofile:
        soft: 65536
        hard: 65536
    mem_limit: 1g
    cap_add:
      - IPC_LOCK
    volumes:
      - esdata2:/usr/share/elasticsearch/data
    networks:
      - esnet

volumes:
  esdata1:
    driver: local
  esdata2:
    driver: local

networks:
  esnet:
    driver: bridge
```

클러스터를 중지시키기 위해서는, `docker-compose down`을 입력하세요. 데이터 볼륨이 지속되므로 docker-compose up을 사용하여 동일한 데이터로 클러스터를 다시 시작할 수 있습니다. 클러스터 및 데이터 볼륨을 파괴하려면 `docker-compose down -v`를 입력하십시오.

##### 클러스터의 상태를 보려면
```sh
curl -u elastic http://127.0.0.1:9200/_cat/health
Enter host password for user 'elastic':
1472225929 15:38:49 docker-cluster green 2 2 4 2 0 0 0 0 - 100.0%
```
로그 메시지는 콘솔로 이동하여 구성된 Docker 로깅 드라이버가 처리합니다. 기본적으로 `docker logs` 로그에 액세스 할 수 있습니다.

#### Configureing Elasticsearch with Docker
Elasticsearch 의 설정은 `/usr/share/elasticsearch/config/`에서 불러와집니다. 이 파일을 설정하는 방법은, [Configuring Elasticsearch](https://www.elastic.co/guide/en/elasticsearch/reference/current/settings.html) 와 [Setting JVM options](https://www.elastic.co/guide/en/elasticsearch/reference/current/setting-system-settings.html#jvm-options)에서 볼 수 있습니다.

이미지는 맞춤 검색 파일 (예 : elasticsearch.yml)을 제공하는 기존 방식을 사용하여 탄성 검색 설정을 구성하는 여러 가지 방법을 제공하지만 환경변수를 사용하여 옵션을 설정할 수도 있습니다.
