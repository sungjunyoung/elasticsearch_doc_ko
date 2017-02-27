> Setup Elasticsearch  
> 원본 : https://www.elastic.co/guide/en/elasticsearch/reference/current/setup.html

### Setup Elasticsearch

다음의 섹션은
- 다운로드
- 인스톨
- 시작
- 설정
을 포함하여 어떻게 Elasticsearch를 세팅하는지에 대한 정보를 포함합니다.

#### Supported platforms

공식적으로 지원하고 있는 운영체제와 JVM 에 관한 정보들은 이곳에서 볼 수 있습니다. : [Supported Matrix](https://www.elastic.co/support/matrix). 이곳에 나와있는 플랫폼에서 테스트가 되었지만, 다른 플랫폼에서도 작동합니다.

#### JAVA (JVM) Version

Elasticsearch는 Java 로 만들어 졌습니다. 실행하기 위해서는 [Java 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 이상이 필요합니다. 오라클 공식 자바와 OpenJDK 만이 지원됩니다. 모든 Elasticsearch 노드와 클라이언트에 대해서 같은 버전의 JVM 이 사용되어야 합니다.

1.8.0_73 버전이나 그 이후의 버전을 설치하기를 권고합니다. Elasticsearch 는 잘못된 버전의 Java 가 쓰여진다면 시작되지 않을 것입니다.

Elasticsearch 를 사용할 자바의 버전은 JAVA_HOME 환경변수를 지정함으로서 설정 가능합니다.

> Elasticsearch는 64 비트 서버 JVM에서의 실행이 디폴트입니다. 32 비트 클라이언트 JVM을 사용하는 경우 jvm.options에서 -server를 제거해야하며 32 비트 JVM을 사용하는 경우 스레드 스택 크기를 -Xss1m에서 -Xss320k로 재구성해야합니다.
