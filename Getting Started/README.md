## Getting Started

 Elasticsearch 는 확장성있는 full-text 검색과 분석 엔진입니다. Elasticsearch 는 당신에게 큰볼륨의 데이터를 빠르게, 그리고 실시간으로 저장하고, 검색하고, 분석할수 있게 합니다. 일반적으로 복잡한 검색 기능과 요구 사항이있는 응용 프로그램을 구동하는 엔진 혹은 기술로 사용됩니다.

 다음은 Elasticsearch 를 사용할 수 있는 use-case 들입니다.

	- 쇼핑몰을 운영하며, 당신의 고객에게 당신이 팔고 있는 제품을 검색할 수 있도록 합니다. 당신은 고객에게 전체 제품 카탈로그, 인벤토리를 저장하고, 검색과 자동완성을  Elasticsearch 를 통해 제공할 수 있습니다.
	- 로그와 통신내역 데이터를 모으길 원할 때, 이 데이터들을 통해 트랜드를 파악하는 등의 작업을 하기를 원할 때 사용할수 있습니다. 이런 경우, 당신은 Logstash(Elasticsearch/Logstash/Kibana Stack) 의 데이터를 Elasticsearch 로 공급함으로서 모으고, 분석할 수 있습니다. 일단 이 데이터들이 Elasticsearch 에 있으면, 당신은 당신이 원하는 정보를 얻기 위해 검색 등의 작업을 수행할 수 있습니다.
	- “특정 전자 장치를 구입하는 데 관심이 있으며 다음 달의 모든 공급 업체에서 가제트 가격이 $ X 이하로 떨어지면 알림을 받고 싶습니다" 와 같은 규칙을 지정할 수있는 가격 알림 플랫폼을 운영한다면, 이 경우 공급 업체 가격을 긁어내어 Elasticsearch로 밀어 넣고 역방향 검색 (Percolator) 기능을 사용하여 가격 변동을 고객 쿼리와 대조하고 결과가 일치하면 고객에게 알림을 푸시 할 수 있습니다.
	- analytics 혹은 business-intelligence에서 요구 사항이 있으며 많은 데이터에 대해 신속하게 조사, 분석, 시각화를하고 싶을 때, (수백만 또는 수십억 개의 레코드에서), Elasticsearch 에 당신의 데이터를 저장하고, Kibana(Elasticsearch/Logstash/Kibana Stack)  를 통해 시각화 할 수 있습니다. 게다가, 데이터에 대해 복잡한 쿼리를 위해 Elasticsearch aggregations functionality 를 사용할 수도 있습니다.

 나머지 튜토리얼을 위해, Elasticsearch 를 띄우고 실행시키고, 당신의 데이터에 대해 인덱싱, 검색, 수정의 기본적인 명령을 수행하는 가이드를 제공할 것입니다. 튜토리얼의 끝에는, 당신은 Elasticsearch에 대한 좋은 아이디어를 가질 수 있으며, Elasticsearch를 어떻게 사용할 지에 대한 영감을 얻을 수 있습니다.
