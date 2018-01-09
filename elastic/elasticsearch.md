# Elasticsearch
Index는 RDB에서의 database와 유사한 기능으로 생각하면 될 것으로 보임
Type은 index에서 포함될 documents의 종류
Document 하나하나가 RDB에서의 row와 유사하다고 생각할 수 있음
AWS ES에서 index, type은 적당한 이름으로 지정하면 되고 id의 경우 data에서 특정하기 어려우면 generation 되는 값을 이용 (예 : newuuid())
Index 생성은 원래 ES의 API 호출로 가능
ES에 일반 문자열을 밀어넣었을 때 인식 못함 => JSON을 문자열 변환 후 넣었을 때 인식
AWS ES에 데이터 넣을 때 id가 generation 되는 값이 아니라 고정 문자열이면 같은 document로 인식하고 값을 update 하는 것으로 보임

### Elasticsearch on Docker
1. Memory
macOS에서 elasticsearch와 kibana를 같이 띄울 때 docker engine의 기본 메모리 설정이 2GB로 되어있는 경우 elasticsearch가 올라오고 죽는 문제가 있는데 4GB로 할당하니 문제 없음

2. Elasticsearch
아래의 command 실행. 상세 내용은 [문서][es-docker-link] 참조
```bash
docker run -p 9200:9200 -p 9300:9300 \
    -e "discovery.type=single-node" \
    docker.elastic.co/elasticsearch/elasticsearch:5.5.3
```

3. Kibana
상세 내용은 [문서][kibana-docker-link]에 있음
```bash
docker run -p 5601:5601 \
    -e "ELASTICSEARCH_URL=http://elasticsearch_host:9200" \
    docker.elastic.co/kibana/kibana:5.5.3
```

### Index 생성
**PUT /index/index_name** 만 호출해도 elasticsearch에서는 index가 생성된다.
그 이후에 Kibana에서 index pattern을 등록해주면 됨.

### Index에서 custom date format 적용
Index 생성시 아래처럼 특정 type에 properties를 정의해주면 된다.
아래의 경우 log data 중 datetime field의 format을 재정의하는 내용.
```json
{
  "mappings": {
    "type1": {
      "properties": {
        "datetime": {
          "type": "date",
          "format": "dd/MMM/yyyy:HH:mm:ss Z"
        }
      }
    }
  }
}
```

### 더 살펴볼 문서
- [엘라스틱서치 이해하기](https://www.slideshare.net/dahlmoon/20160612)

[es-docker-link]: https://www.elastic.co/guide/en/elasticsearch/reference/5.5/docker.html
[kibana-docker-link]: https://www.elastic.co/guide/en/kibana/5.5/_configuring_kibana_on_docker.html