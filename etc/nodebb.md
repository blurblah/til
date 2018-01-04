# Nodebb terms
게시판은 category
게시물은 topic
게시물을 구성하는 글(답글? 포함) post
category > topic > post와 같은 구조

# Nodebb APIs
Nodebb는 URL이 resource를 표현하고 있기 때문에 api endpoint만 지정하고 나머지 url을 붙이면 가능함
예를 들어, 메인 화면에 진입하면 category list가 보이는데 url이 http://nodebb_host/ 라면, 아래처럼 호출.
```bash
# category list sample
curl http://nodebb_host/api
```
Endpoint가 /api 인데, 다른 화면에서도 표시되는 url들을 endpoint와 조합하면 json 형태의 정보 획득 가능
/api 호출시 나타나는 category list에서 특정 category의 게시물들을 보고 싶다면 해당 category의 slug값을 이용한다.
예를 들어, Announcements category의 slug key의 값이 1/announcements 인 경우 해당 category의 게시물 리스트를 보고싶다면, 아래처럼 조합한다.
**API endpoint + /category/ + category slug**
```bash
# post list of the category numbered 5 as cid
# category slug printed 5/posts got from above command
curl http://nodebb_host/api/category/5/posts
```
게시물 리스트를 얻어오고 나서 특정 게시물의 정보를 얻고싶다면 게시물 리스트의 item 별로 할당되어 있는 slug를 역시 이용하고 아래처럼 호출.
**API endpoint + /topics/ + topic slug**
```bash
# topic information
# topic slug from above is 10/test-article-09
curl http://nodebb_host/api/topic/10/test-article-09
```

# Nodebb에 NginX로 reverse proxy 적용하는 방법
Nodebb 기본 구성 후 상위에 reverse proxy를 두려고 할 때 설정하는 방법
기본적인 nginx 설정 방법은 [공식 문서][nodebb-nginx-doc-link]를 참고하면 됨
Root context 이외의 경로를 root로 잡고자 할 때에는 몇가지 추가 과정이 필요함
NginX는 기본 설정에서 context path 추가하는 형태로 하면 되고 (아래 참조)
```bash
location /community {
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_set_header Host $http_host;
    proxy_set_header X-NginX-Proxy true;

    proxy_pass http://127.0.0.1:4567/community;
    proxy_redirect off;

    # Socket.IO Support
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
}
```
proxy_pass 되는 경로를 root가 아니라 다른 경로로 잡아주는게 편한데 nodebb의 config.json 변경 필요
Nodebb의 설정 메뉴에서 변경 안되고 nodebb 설치 경로의 config.json 파일을 수정하고 restart 해야함
config.json 파일에 url 부분을 nginx에서 보내는 경로로 맞춰주면 완료
이 상태에서 nodebb에 접속해보면 socket.io 문제가 발생했음
이유는 외부에서 직접 nodebb url로 접속하지 않고 nginx를 통해서만 접속 가능하도록 하기 위해
url에 host ip 대신 127.0.0.1을 지정했는데 접속은 nginx의 ip나 nginx에 설정된 도메인으로 진행했기 때문
이와 같은 경우 nodebb의 config.json에 아래와 유사하게 socket.io에 대한 설정 추가하면 됨
```json
"socket.io": {
  "origins": "*:*"
}
```

[nodebb-nginx-doc-link]: https://nodebb.readthedocs.io/en/latest/configuring/proxies/nginx.html
