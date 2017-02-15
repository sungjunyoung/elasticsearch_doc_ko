> [Getting Started](https://github.com/sungjunyoung/elasticsearch_doc_ko/tree/master/1.%20Getting%20Started) > Installation  
> 원본 : https://www.elastic.co/guide/en/elasticsearch/reference/current/_exploring_your_cluster.html

### Installation

> **역자주**  
> MAC 환경에서는 homebrew 로 설치하면 간편합니다! :)

Elasticsearch 는 Java 8 이상을 요구합니다. 특히, 현재 이 DOC에서, Oracle JDK version 1.8.0_73 을 사용하기를 추천합니다. Java 설치는 여기서 자세히 다루지 않습니다. Oracle 이 추천하는 설치 문서는 [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html) 에서 조회할 수 있습니다. Elasticsearch를 설치하기 전에, Java 버전을 다음 명령어로 체크해주십시오 (필요하다면 설치/업그레이드 해 주십시오.)
```bash
java -version
echo $JAVA_HOME
```
Java 가 준비되었으면, Elasticsearch 를 다운로드하고 실행할 수 있습니다. 모든 과거의 릴리즈 binaries 는 [www.elastic.co/downloads](www.elastic.co/downloads) 에서 다운 가능합니다. 각각의 릴리즈에서, 당신은 zip 과 tar 압축파일 중 선택하거나, DEB 혹은 RPM 패키지를 통해 설치 가능합니다. 간단하게, tar 파일로 설치해봅니다.

Elasticsearch 4.2.1 tar 를 다음과 같이 다운받습니다. (Windows 유저는 zip 패키지로 다운받아야 합니다.)
```bash
curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.1.tar.gz
```
이후 압축을 해제합니다. (Windows 유저는 unzip 을 사용해야 합니다.)
```bash
tar -xvf elasticsearch-5.2.1.tar.gz
```
이 명령은 현재 디렉토리에 폴더를 생성할 것입니다. 그 후 bin 폴더로 이동합니다.
```bash
cd elasticsearch-5.2.1/bin
```
이제 노드와 단일 클러스터를 시작할 준비가 되었습니다. (Windows 유저는 elasticsearch.bat 파일을 실행해야 합니다.)
```bash
./elasticsearch
```
만약 모든 것이 잘 진행 된다면, 다음과 같은 메세지들을 보게 될 것입니다.
```bash
[2016-09-16T14:17:51,251][INFO ][o.e.n.Node               ] [] initializing ...
[2016-09-16T14:17:51,329][INFO ][o.e.e.NodeEnvironment    ] [6-bjhwl] using [1] data paths, mounts [[/ (/dev/sda1)]], net usable_space [317.7gb], net total_space [453.6gb], spins? [no], types [ext4]
[2016-09-16T14:17:51,330][INFO ][o.e.e.NodeEnvironment    ] [6-bjhwl] heap size [1.9gb], compressed ordinary object pointers [true]
[2016-09-16T14:17:51,333][INFO ][o.e.n.Node               ] [6-bjhwl] node name [6-bjhwl] derived from node ID; set [node.name] to override
[2016-09-16T14:17:51,334][INFO ][o.e.n.Node               ] [6-bjhwl] version[5.2.1], pid[21261], build[f5daa16/2016-09-16T09:12:24.346Z], OS[Linux/4.4.0-36-generic/amd64], JVM[Oracle Corporation/Java HotSpot(TM) 64-Bit Server VM/1.8.0_60/25.60-b23]
[2016-09-16T14:17:51,967][INFO ][o.e.p.PluginsService     ] [6-bjhwl] loaded module [aggs-matrix-stats]
[2016-09-16T14:17:51,967][INFO ][o.e.p.PluginsService     ] [6-bjhwl] loaded module [ingest-common]
[2016-09-16T14:17:51,967][INFO ][o.e.p.PluginsService     ] [6-bjhwl] loaded module [lang-expression]
[2016-09-16T14:17:51,967][INFO ][o.e.p.PluginsService     ] [6-bjhwl] loaded module [lang-groovy]
[2016-09-16T14:17:51,967][INFO ][o.e.p.PluginsService     ] [6-bjhwl] loaded module [lang-mustache]
[2016-09-16T14:17:51,967][INFO ][o.e.p.PluginsService     ] [6-bjhwl] loaded module [lang-painless]
[2016-09-16T14:17:51,967][INFO ][o.e.p.PluginsService     ] [6-bjhwl] loaded module [percolator]
[2016-09-16T14:17:51,968][INFO ][o.e.p.PluginsService     ] [6-bjhwl] loaded module [reindex]
[2016-09-16T14:17:51,968][INFO ][o.e.p.PluginsService     ] [6-bjhwl] loaded module [transport-netty3]
[2016-09-16T14:17:51,968][INFO ][o.e.p.PluginsService     ] [6-bjhwl] loaded module [transport-netty4]
[2016-09-16T14:17:51,968][INFO ][o.e.p.PluginsService     ] [6-bjhwl] loaded plugin [mapper-murmur3]
[2016-09-16T14:17:53,521][INFO ][o.e.n.Node               ] [6-bjhwl] initialized
[2016-09-16T14:17:53,521][INFO ][o.e.n.Node               ] [6-bjhwl] starting ...
[2016-09-16T14:17:53,671][INFO ][o.e.t.TransportService   ] [6-bjhwl] publish_address {192.168.8.112:9300}, bound_addresses {{192.168.8.112:9300}
[2016-09-16T14:17:53,676][WARN ][o.e.b.BootstrapCheck     ] [6-bjhwl] max virtual memory areas vm.max_map_count [65530] likely too low, increase to at least [262144]
[2016-09-16T14:17:56,731][INFO ][o.e.h.HttpServer         ] [6-bjhwl] publish_address {192.168.8.112:9200}, bound_addresses {[::1]:9200}, {192.168.8.112:9200}
[2016-09-16T14:17:56,732][INFO ][o.e.g.GatewayService     ] [6-bjhwl] recovered [0] indices into cluster_state
[2016-09-16T14:17:56,748][INFO ][o.e.n.Node               ] [6-bjhwl] started
```
많은 메세지들이 생략되어 있지만, "6-bjhwl" 라는 노드의 이름을 볼 수 있습니다. (다른 문자열 일 수 있습니다.) 이 노드는 단일 클러스터에서 마스터로 선출되어 시작되었습니다.

아직 master 의 의미가 무엇인지에 대한 걱정은 하지 마십시오. 가장 중요한 것은 우리가 하나의 클러스터에서 하나의 노드를 시작했다는 것입니다.

이전에 말했듯, 우리는 노드의 이름이나 클러스터의 이름을 오버라이드 할 수 있습니다. 다음의 command line 으로 변경 가능합니다.
```bash
./elasticsearch -Ecluster.name=my_cluster_name -Enode.name=my_node_name

```

또한 http로 표시된 행에 노드에 접근할 수 있는 HTTP 주소 (192.168.8.112) 및 포트 (9200)에 대한 정보가 있습니다. 기본적으로 Elasticsearch는 9200 포트를 사용하여 REST API에 대한 액세스를 제공합니다. 필요한 경우 이 포트를 구성 할 수 있습니다.
