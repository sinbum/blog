# 컨테이너 만들기

## Dockerfile

* dockerfile,컨테이너 빌드
  * dockerfile 설명
    * 쉽고,간단,명확한 구문을 가진 text file로 Top-Down 으로 해석
    * 컨테이너 이미지를 생성할 수 있는 고유의 지시어를 가짐.
    * 대소문자를 구분하지 않지만 가독성을 위해 사용함.
  * 빌드 명령
    * mkdir build
    * cd build
    * nano dockerfile
      * FROM node: 12
      * COPY hello.js
      * CMD \["node","/hello.js"]
    * docker build -t imagename:tage
  * Dockerfile 문법
    * ### : 주석
    * FROM : 컨테이너의 BASE IMAGE(운영환경)
    * MAINTAINER : 이미지를 생성한 사람의 이름 및 정보
    * LABEL : 컨테이너 이미지에 컨테이너의 정보를 저장.(description)
    * RUN : 컨테이너 빌드를 위해 base image 에서 실행할 명령
    * COPY : 컨테이너 빌드시 호스트의 파일을 컨테이너로 복사.
    * ADD : 컨테이너 빌드시 호스트의 파일(tar, url 포함)을 컨테이너로 복사
    * WORKDIR : 컨테이너 비륻시 명령이 실행될 작업 디렉터리 설정
    * ENV : 환경변수 지정
    * USER : 명령 및 컨테이너 실행시 적용할 유저 설정.
    * VOLUME : 파일 또는 디렉토리를 컨테이너의 디렉토리로 마운트
    * EXPOSE : 컨테이너 동작 시 외부에서 사용할 포트 지정.
    * CMD : 컨테이너 동작 시 자동으로 실행할 서비스나 스크립트 지정
    * ENTRYPOINT : CMD와 함께 사용하면서 command 지정시 사용

## 컨테이너 배포

* 컨테이너 배포
  * docker build -t hellojs:atest .
    * 마지막에 '.' 을 붙이는 것은 현재 디렉토리 기준으로 작업시작을 알림.
    * 예를들어 copy하고자 하는 파일이 tmp 에 있다면 '.' 이 아닌 '현재디렉토리/tmp' 인 'tmp' 로 써주어야함.
  * docker login
  * docker push hellojs:latest
  * [hub.docker.com](https://hub.docker.com)

## \*) nodejs 애플리케이션 컨테이너 만들기

* hellojs 폴더생성 : mkdir hellojs && cd hellojs
*   cat > hello.js 이후 소스코드 js 소스코드입력.

    ```
    const http = require('http');
    const os = require('os');
    console.log("Test server starting..");

    var handler = function(request, response){
      console.log("Received request from " + request.connection.remoteAddress);
      response.writeHead(200);
      response.end("Container Hostname: " + os.hostname() + "\n");
    };

    var www = http.createServer(handler);
    www.listen(8080);
    ```

## \*) 우분투 기반의 웹 서버 컨테이너 만들기

*   hellojs.js 생성

    * cat >(리다이렉션) 파일명은 라인입력으로 글을 작성 가능.
    * 컨트롤 d 로 저장

    ```js
    const http = require('http');
    const os = require('os');
    console.log("Test server starting..");

    var handler = function(request, response){
      console.log("Received request from " + request.connection.remoteAddress);
      response.writeHead(200);
      response.end("Container Hostname: " + os.hostname() + "\n");
    };
      
    var www = http.createServer(handler);  
    www.listen(8080);
    ```
* Dockerfile 만들기

```dockerfile
FROM node:14
COPY hello.js /
CMD ["node","hello.js"]
```

* 도커 빌드하기
  * docker build -t hellojs:latest .
    * latest는 작성하지 않아도 자동으로 인식.
    * 그외 다른 문구 예)"v1.0.1" 이런식으로 쓸경우 docker 허브에 푸시 할 경우 함께 입력 필요.
*   이미지 실행시키기

    ```shell
    docker run -d -p 8080:8080 --name web hellojs
    ```

## \*) 우분투 기반의 웹 서버 컨테이너 만들기2

* hellojs.js 생성

```js
```

* Dockerfile 만들기

```dockerfile
FROM ubuntu:22.04
LABEL maintainer="Sinbum choi <sinbum@kakao.com>"
# install apache

RUN apt-get update \
    && apt-get install -y apache2
RUN echo "TEST WEB" > /var/www/html/index.html
EXPOSE 80
CMD ["/usr/sbin/apache2ctl", "-DFOREGROUND"]
```

* 도커 빌드하기
  * docker build -t webserver:v1 .
    * latest는 작성하지 않아도 자동으로 인식.
    * 그외 다른 문구 예)"v1.0.1" 이런식으로 쓸경우 docker 허브에 푸시 할 경우 함께 입력 필요.
*   이미지 실행시키기

    ```shell
    docker run -d -p 80:80 --name web webserver:v1
    ```

## \*) 데비안 에서의 빌드 및 배포 연습

1. fortune을 실행시 결과 아웃풋을 다음과 같은 html 파일의 경로에 담는다.

```shell
#!/bin/bash
mkdir /htdocs
while :
do
 /usr/games/fortune > /htdocs/index.html
 sleep 10
done
```

1. Dockerfile 에 다음과 같이 스크립트를 작성한다.

```dockerfile
FROM debian:latest
RUN apt-get update \
 && apt-get -y install fortune
WORKDIR /scripts
COPY webpage.sh .
CMD ["chmod","+x","webpage.sh"]
CMD ["bash","webpage.sh"]
```

1. 빌드를 하고 실행한다.
   * docker build -t new\_fortune .
   * docker images
   * docker run -d --name fortune new\_fortune
   * docker ps
   * docker exec fortune cat /htdocs/index.html

## \*) 만든 컨테이너 배포하기

* docker login
* docker tag 명령어로 이름 바꿔주기
* docker push
