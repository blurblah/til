# Elasticsearch
Index는 RDB에서의 database와 유사한 기능으로 생각하면 될 것으로 보임
Type은 index에서 포함될 documents의 종류
Document 하나하나가 RDB에서의 row와 유사하다고 생각할 수 있음
AWS ES에서 index, type은 적당한 이름으로 지정하면 되고 id의 경우 data에서 특정하기 어려우면 generation 되는 값을 이용 (예 : newuuid())
Index 생성은 원래 ES의 API 호출로 가능
ES에 일반 문자열을 밀어넣었을 때 인식 못함 => JSON을 문자열 변환 후 넣었을 때 인식
AWS ES에 데이터 넣을 때 id가 generation 되는 값이 아니라 고정 문자열이면 같은 document로 인식하고 값을 update 하는 것으로 보임