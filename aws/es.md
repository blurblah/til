# AWS ES(Elasticsearch Service)
AWS에서 Elasticsearch를 SaaS 형태로 제공하고 있음
**Price**: Instance type 중에 작은 것(t2.small)도 고를 수 있고 비용은 Oregon 기준 $0.036/h (t2.small)
**Characteristics**:
- Cluster 구성 가능
- Domain만 만들면 연결 가능한 endpoint가 자동으로 만들어짐 (with Kibana)
- Kibana는 기본적으로 사용자 인증부분이 없는데 AWS에서는 이것을 Access Policy로 해결
- Access Policy : IAM, IP기반, public open 등 몇가지 옵션 제공. 설정 변경시 시간이 꽤 걸림
- Index 추가할 때 id는 ${newuuid()} 형태도 사용 가능
<h4>Elasticsearch</h4>
Index는 RDB에서의 database와 유사한 기능으로 생각하면 될 것으로 보임  
Type은 index에서 포함될 documents의 종류  
Document 하나하나가 RDB에서의 row와 유사하다고 생각할 수 있음  
AWS ES에서 index, type은 적당한 이름으로 지정하면 되고 id의 경우 data에서 특정하기 어려우면 generation 되는 값을 이용 (예 : newuuid())  
Index 생성은 원래 ES의 API 호출로 가능  
ES에 일반 문자열을 밀어넣었을 때 인식 못함 => JSON을 문자열 변환 후 넣었을 때 인식  
AWS ES에 데이터 넣을 때 id가 generation 되는 값이 아니라 고정 문자열이면 같은 document로 인식하고 값을 update 하는 것으로 보임  
<h4>AWS IoT</h4>
IoT device를 위한 hub 역할  
Azure IoT Hub와 유사(pub/sub)  
<strong>Rule:</strong>  
- 다른 service와 연동하기 위한 기능
- AWS IoT로 publish되는 message들을 query 형태로 고를 수 있음(attribute, topic, condition)
- 선택된 조건에 부합하는 message들을 S3, Kinesis, ES 등으로 전달 가능
<h4>더 살펴볼 문서</h4>
- [엘라스틱서치 이해하기][elasticsearch_slideshare]

[elasticsearch_slideshare]: https://www.slideshare.net/dahlmoon/20160612