> [Setup Elasticsearch]() > Installing Elasticsearch  
> 원본 : https://www.elastic.co/guide/en/elasticsearch/reference/current/install-elasticsearch.html

### Installing Elasticsearch
Elasticsearch 다음의 설치 포맷을 제공합니다.

|   format      |Explanation|
|---------------|---|
|   zip/tar.gz  |   zip과 tar.gz 패키지는 어떠한 시스템에나 설치가능하고, Elasticsearch 를 시작하기에 가장 쉬운 선택입니다.   |
|   deb         |   deb 패키지는 Debian, Ubuntu, 그리고 다른 Debian 계열 운영체제에 적절합니다. Debian 패키지는 웹사이트나 Elasticsearch Debian 저장소에서 다운받을 수 있습니다.|
|   rpm         |   rpm 패키지는 Redhat 계열 운영체제에서 설치가능합니다. RPM 역시 웹사이트나 Elasticsearch RPM 저장소에서 다운로드 할 수 있습니다.|
|   docker      |   docker 컨테이너에서 Elasticsearch를 이용가능합니다. X-Pack이 사전 설치되어 제공되며 Elastic Docker Registry에서 다운로드 할 수 있습니다.|

#### Configuration Management Tools
Elasticsearch 는 대규모 배포를 돕기 위한 다음의 설정관리 툴을 제공합니다.

|Tools|Link|
|-----|----|
|Puppet|[puppet-elasticsearch](https://github.com/elastic/puppet-elasticsearch)|
|Chef|[cookbook-elasticsearch](https://github.com/elastic/cookbook-elasticsearch)|
|Ansible|[ansible-elasticsearch](https://github.com/elastic/ansible-elasticsearch)|

> **역자주**  
> 공부 목적으로 제작되어 docker 만 번역합니다.
