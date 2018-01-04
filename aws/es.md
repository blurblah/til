# AWS ES(Elasticsearch Service)
AWS에서 Elasticsearch를 SaaS 형태로 제공하고 있음
#### Price :
Instance type 중에 작은 것(t2.small)도 고를 수 있고 비용은 Oregon 기준 $0.036/h (t2.small)
#### Characteristics :
- Cluster 구성 가능
- Domain만 만들면 연결 가능한 endpoint가 자동으로 만들어짐 (with Kibana)
- Kibana는 기본적으로 사용자 인증부분이 없는데 AWS에서는 이것을 Access Policy로 해결
- Access Policy : IAM, IP기반, public open 등 몇가지 옵션 제공. 설정 변경시 시간이 꽤 걸림
- Index 추가할 때 id는 ${newuuid()} 형태도 사용 가능