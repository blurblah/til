# Spring boot 기반 application을 docker image로 만들기
### Dockerfile
Jar로 packaging 된 것을 container 안에 넣도록 파일명등을 강제로 설정할 수도 있는데 아래와 같은 방법도 가이드되고 있음
상세 내용은 [공식문서][spring-boot-docker-link] 참조
```bash
FROM openjdk:8-jdk-alpine
VOLUME /tmp
ARG JAR_FILE
ADD ${JAR_FILE} app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]
```
이 때 JAR_FILE 이라는 argument는 maven이나 gradle을 이용한다면 자동으로 packaging 된 이름을 넣어줄 수 있음
```xml
<properties>
   <docker.image.prefix>springio</docker.image.prefix>
</properties>
<build>
    <plugins>
        <plugin>
            <groupId>com.spotify</groupId>
            <artifactId>dockerfile-maven-plugin</artifactId>
            <version>1.3.6</version>
            <configuration>
                <repository>${docker.image.prefix}/${project.artifactId}</repository>
	<buildArgs>
		<JAR_FILE>target/${project.build.finalName}.jar</JAR_FILE>
	</buildArgs>
            </configuration>
        </plugin>
    </plugins>
</build>
```
Spotify의 build plugin으로 아래와 같은 maven command로 docker image build까지 가능함
```bash
# Build jar package
mvn clean package
# Build docker image
mvn dockerfile:build
```

[spring-boot-docker-link]: https://spring.io/guides/gs/spring-boot-docker/