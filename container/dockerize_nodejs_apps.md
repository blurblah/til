# Docker for the node apps
Node 기반의 application을 dockerization 할 때 아래와 유사한 방식을 사용(Angular.js 환경에서 사용해 봄)
1. Base image 지정 (node official image)
2. package.json 복사
3. npm install
4. Copy source files (이 때 node_modules는 복사되지 않도록 .dockerignore 파일에 등록)
5. Expose ports and something...
6. Run application (CMD를 이용 npm start)