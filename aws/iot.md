# AWS IoT
IoT device를 위한 hub 역할
Azure IoT Hub와 유사(pub/sub)
#### Rule :
- 다른 service와 연동하기 위한 기능
- AWS IoT로 publish되는 message들을 query 형태로 고를 수 있음(attribute, topic, condition)
- 선택된 조건에 부합하는 message들을 S3, Kinesis, ES 등으로 전달 가능