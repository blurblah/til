# Docker registry

### 구축
Container만 올리면 됨
인증을 넣기 위해서 key, crt도 필요한 것으로 보임

##### Health check
Health check 기능은 기본적으로 활성화되어 있는 것으로 생각됨
무시하고 진행하면 아래와 같은 오류 발생
```json
status=503 SERVICE_UNAVAILABLE {"errors":[{"code":"UNAVAILABLE","message":"service unavailable","detail":"health check failed: please see /debug/health"}]}
```
오류를 없애기 위해서는 http debug addr 속성을 container 올릴 때 넣어줘야 함
[Configuration 문서][docker_registry_configuration] 참조

### S3 연동
Docker image 저장을 외부에 있는 storage에 할 수 있는 기능이 있음
그 중 S3 연동을 했을 경우 health check에 문제가 생기는 경우가 있음
:5001/debug/health (이 중 5001은 debug addr port)를 호출했을 때 아래와 같은 응답
```json
{"storagedriver_s3":"s3aws: Path not found: /"}
```
특별히 잘못 설정한 것은 아니고 버그로 생각됨
[Issue 문서][s3_health_check_issue] 참조
Docker registry image를 2.5 버전으로 사용하면 문제없음

### Image push 절차
1. Insecure registry를 daemon에 등록하고 restart
```bash
sudo vi /etc/docker/daemon.json
{
    "insecure-registries": [
        "registry_host:port"
    ]
}
sudo service docker restart
```
2. Registry에 login
```bash
sudo docker login registry_host:port
```
3. Local machine에 생성한 image의 tag 생성
```bash
sudo docker tag local_image_name registry_host:port/user/image_name
```
4. Image push
이 때 login 된 username으로만 push 할 수 있는 것으로 보임
권한을 full로 주면 다른 경로로도 올릴 수 있을지도 모르겠음
```bash
sudo docker push registry_host:port/user/image_name
```

### Image pull
Insecure registry 등록과 로그인은 동일
read 권한이 있어야 함
Image pull도 push 할 때 처럼 **registry_host:port**를 image 앞에 지정해줘야함

[docker_registry_configuration]: https://github.com/docker/distribution/blob/master/docs/configuration.md#debug
[s3_health_check_issue]: https://github.com/docker/distribution/issues/2292