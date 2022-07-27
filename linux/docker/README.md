---
description:도커를 설명 합니다.
---


# 도커란 무엇인가?

- 목차 
  - 도커 설명 
  - 도커 설치
  - 컨테이너 살펴보기
  - 컨테이너 만들기
  - 컨테이너 보관
  - 컨테이너 사용
  - 컨테이너 관리
  - 컨테이너 볼륨
  - 컨테이너 통신
  - 빌드 운영

## 도커 설명
- 컨테이너를 배우는 이유
- 리눅스 사용에서의 도커
- 일반 프로그램과 컨테이너의 차이
- 도커 사용의 편리함


### 컨테이너를 배우는 이유
소프트웨어의 운영 플랫폼 변화
온프레미스 > 가상화 솔루션 사용 > 컨테이너 엔진의 사용

- 하드웨어의 효율성 극대화  
하드웨어의 가격은 낮아지고, 성능은 좋아짐으로써 운영되는 서버의 용량은 대용량화 되어 가면서 가상화 플랫폼을 사용 하였습니다.  
이후 가상화 플랫폼에서 부터 서버 운영시 자원 사용의 효율을 극대화 하기 위하여 그 패러다임은 진화 하기 시작하였습니다.  

- 시대의 변화   
시대가 변화 함에 따라, 클라우드 서비스의 가속화에 따라서 컨테이너 엔진의 사용 요구는 기하 급수적으로 늘어나게 되었습니다.

### 리눅스 사용에서의 도커
- 독립된 공간 형성
- isolate 기능 지원
- cgroup 필요한 만큼의 하드웨어지원

윈도우즈나 맥os 에서 도커를 사용하려면 하이퍼바이저(hipervisor)를 활성화 시켜야 합니다.  
그러나 리눅스의 경우는 리눅스 커널을 직접 사용하고 실제 현장에서는 라이센스 비용이 들어가지 않습니다.  
이러한 이유로 우리는 리눅스 환경에서 도커를 사용합니다.

### 일반 프로그램과 컨테이너의 차이
예를 들어 프론트에서 운영되는 Node.js 에서의 프론트 앱을 개발했다고 하는 경우, 일반 시스템에서 작동하는 경우 Node.js 환경이 필요합니다.  
또한 필요에 의해서 의존성을 가지거나 추가로 애플리케이션이 필요한 경우에 직접적으로 설치 할 필요성이 생깁니다.  
컨테이너 기반의 애플리케이션의 경우 Node.js 전용 환경 컨테이너를 설치하고,컨테이너 내 코드파일을 넣어 사용 합니다.

### 도커 사용의 편리함

- 개발자가 만든 그대로가 어디서든 사용이 가능함
- scale out / scale in 의 편리함
    - 적응 용량으로 빠르게 확장성이 가능.
- MSA(Micro Service Architecture),Devops(Development & Operations) 적합
    - 고객의 요구를 빠르게 처리해서 바로바로 응대 할 수 있는 환경.
- 예) 개발자가 어플리케이션을 개발한 경우
  - 컨테이너에 개발한 어플리케이션은 어떤 환경에서든 컨테이너를 제공 받아 즉각 적으로 사용이 가능함.
  - 환경에 영향을 받지 않음.


## 도커 설치

- 도커 설치시 필요한 요소
- 사양
    - 운영체제 : 리눅스, windows
    - cpu:2core, memory: 2GB 이상
- 도커 설치하기
- VirtualBox 설치 - 네트워크 구성 - VM(가상머신)만들기
    - VM에 Ubuntu 20.04 설치하고 기본환경 구성
    - VM에 centos 설치하고 기본환경 구성
    - Ubuntu/CentOS Server에 Docker 설치

### VirtualBox 설치 - 네트워크 구성 - VM(가상머신)만들기
- VirtualBox 다운로드 후 설치
  - [https://www.virtualbox.org/](https://www.virtualbox.org/)
  - [vmware 설치 방법 링크](https://hiseon.me/linux/ubuntu/ubuntu-virtualbox-install/)
- VirtualBox - Network 구성
  - NAT 네트워크 추가 : 파일 - 환경설정 -네트워크 -추가
  - 네트워크 이름 : localNetwork
  - 네트워크 CIDR: 10.100.0.0/24
  - DHCP 지원
  - 포트포워딩 
- 가상머신 만들기
  1. docker-ubuntu (cpu:2core, memory: 2GB 이상,network(local),disk(20GB))     
  2. docker-centos (cpu:2core, memory: 2GB 이상,network(local),disk(20GB))



### VM에 Ubuntu 20.04 설치하고 기본환경 구성
- GUI 로그인 : guru / work
- 서버구성 : 네트워크설정
  - IP address : 동적할당 된 어드레스
  - hostname 변경 : /etc/hostname : docker-ubuntu.example.com
  - /etc/hosts 파일에 호스트 정보 추가 하기
- Text 부팅으로 수정
- root password 설정 : sudo passwd root - password
- SSH 서버 설치 후 운영
  - apt-get update && apt-get install -y openssh-server curl vim tree
- Xshell 로 로그인 구성하기.(원격 접속)
  - 그래픽 모드 : sudo systemctl isolate graphical.target
  - 텍스트 모드 : sudo systemctl isolate multi-user.target


### VM에 centos 설치하고 기본환경 구성
- CentOs 다운로드 링크 [https://centos.org](https://centos.org)
- 설치 후 환경구성하기.
  - 관리자 계정 : {id입력} / work\
  - root password : {password입력}
  - 해상도 조절
  - 네트워크 구성:10.100.0.106/24,GW:10.100.0.1,DNS:10.100.0.1,
    - hostname:docker-centos.example.com
    - /etc/hosts 구성하기
      - 연결되어있는 네트워크 지정해주기.
      - 예) 10.100.0.106 {hostname 입력} {name 입력}
      - 예) 10.100.0.106 docker-centos.example.com docker-centos
    - text-login 구성
      - systemctl set-default multi-user.target
    - sshd 서비스 동작상태 확인하기.
      - systemctl status sshd        
    - MobaXterm으로 세션 로그인 설정 후 접속. - 우분투에서의 원격 접속과 같음.

### Ubuntu/CentOS Server에 Docker 설치
- Docker 설치
  - 도커 문서 : [https://docs.docker.com](https://docs.docker.com)
- 설치방법
  - Repository를 이용해 설치
  - Download 후 직접 설치하기
  - Script를 이용한 설치
- 설치후 동작 상태 확인
  - 센트os 환경에서 os 부팅시 도커 작동 활성화
    - systemctl enable docker
- 사용자 도커 권한 할당.
  1. 수퍼유저 계정 접속. - su
  2. 도커에 권한 유저 추가 - usermod -a -G docker {사용계정 userid}\




## 컨테이너 동작방식 설명

- Docker Host (Linux Kernel)
- Docker Daemon : systemctl start docekr 로 실행한 도커.
- Docker Client Command : 기본명령어는 docker를 붙여 사용.
- Docker Hub : 깃허브와 마찬가지로 컨테이너 자체를 클라우드 환경에서 배포 관리 저장하는 장소.
- Container Images : 컨테이너 전체를 하나로 통합한 이미지 형태.
- Container : 도커 컨테이너.

1. 도커 허브 에서 컨테이너 이미지를 검색.
   - docker search nginx
2. 컨테이너 이미지 다운로드 후 Image Layer 보기.
   - su
   - cd val/lib/docker/overlay2
   - docker images
   - docker pull nginx:latest
   - docker images (다시실행 - nginx 이미지가 다운로드 됨)
   
3. 컨테이너 실행하고 확인
  - docker run --name web -d -p 80:80 nginx
  - docker ps
  - docker stop web
  - docker rm web
  - docker rmi nginx


## 컨테이너 만들기

### MSA(Micro Service Architecture)

- 컨테이너의 적재 대상
  - 개발한 프로그램과 실행환경을 모두 컨테이너로 만들 수 있음.
  - MSA(Micro Service Architecture) 환경의 Polyglot 애플리케이션 운영
![Monolithic Architecture -참고: KHOA DINH ](http://khoadinh.github.io/assets/media/monolithic_architecture_diagram.png)

![Microservice Architecture -참고: KHOA DINH ](http://khoadinh.github.io/assets/media/microservices_architecture_diagram.png)

### Dockerfile
- dockerfile,컨테이너 빌드
  - dockerfile 설명
    - 쉽고,간단,명확한 구문을 가진 text file로 Top-Down 으로 해석
    - 컨테이너 이미지를 생성할 수 있는 고유의 지시어를 가짐.
    - 대소문자를 구분하지 않지만 가독성을 위해 사용함.
  - 빌드 명령
    - mkdir build
    - cd build
    - nano dockerfile 
      - FROM node: 12 
      - COPY hello.js 
      - CMD ["node","/hello.js"]
    - docker build -t imagename:tage
  - Dockerfile 문법
    - # : 주석
    - FROM : 컨테이너의 BASE IMAGE(운영환경)
    - MAINTAINER : 이미지를 생성한 사람의 이름 및 정보
    - LABEL : 컨테이너 이미지에 컨테이너의 정보를 저장.(description)
    - RUN : 컨테이너 빌드를 위해 base image 에서 실행할 명령
    - COPY : 컨테이너 빌드시 호스트의 파일을 컨테이너로 복사.
    - ADD : 컨테이너 빌드시 호스트의 파일(tar, url 포함)을 컨테이너로 복사
    - WORKDIR : 컨테이너 비륻시 명령이 실행될 작업 디렉터리 설정
    - ENV : 환경변수 지정
    - USER : 명령 및 컨테이너 실행시 적용할 유저 설정.
    - VOLUME : 파일 또는 디렉토리를 컨테이너의 디렉토리로 마운트
    - EXPOSE : 컨테이너 동작 시 외부에서 사용할 포트 지정.
    - CMD : 컨테이너 동작 시 자동으로 실행할 서비스나 스크립트 지정
    - ENTRYPOINT : CMD와 함께 사용하면서 command 지정시 사용

### 컨테이너 배포
- 컨테이너 배포
  - docker build -t hellojs:atest .
    - 마지막에 '.' 을 붙이는 것은 현재 디렉토리 기준으로 작업시작을 알림.
    - 예를들어 copy하고자 하는 파일이 tmp 에 있다면 '.' 이 아닌 '현재디렉토리/tmp' 인 'tmp' 로 써주어야함. 
  - docker login
  - docker push hellojs:latest
  - [hub.docker.com](https://hub.docker.com)

### *) nodejs 애플리케이션 컨테이너 만들기
- hellojs 폴더생성 : mkdir hellojs && cd hellojs
- cat > hello.js 이후 소스코드 js 소스코드입력.
  ```node
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


### *) 우분투 기반의 웹 서버 컨테이너 만들기
- hellojs.js 생성
  - cat >(리다이렉션) 파일명은 라인입력으로 글을 작성 가능.
  - 컨트롤 d 로 저장
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

- Dockerfile 만들기

```dockerfile
FROM node:14
COPY hello.js /
CMD ["node","hello.js"]
```

- 도커 빌드하기
  - docker build -t hellojs:latest .
    - latest는 작성하지 않아도 자동으로 인식.
    - 그외 다른 문구 예)"v1.0.1" 이런식으로 쓸경우 docker 허브에 푸시 할 경우 함께 입력 필요.
 
- 이미지 실행시키기
  ```shell
  docker run -d -p 8080:8080 --name web hellojs
  ```

### *) 우분투 기반의 웹 서버 컨테이너 만들기2
- hellojs.js 생성
```js

```
- Dockerfile 만들기
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

- 도커 빌드하기
  - docker build -t webserver:v1 .
    - latest는 작성하지 않아도 자동으로 인식.
    - 그외 다른 문구 예)"v1.0.1" 이런식으로 쓸경우 docker 허브에 푸시 할 경우 함께 입력 필요.

- 이미지 실행시키기
  ```shell
  docker run -d -p 80:80 --name web webserver:v1
  ```
### *) 데비안 에서의 빌드 및 배포 연습
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
2. Dockerfile 에 다음과 같이 스크립트를 작성한다.
```dockerfile
FROM debian:latest
RUN apt-get update \
 && apt-get -y install fortune
WORKDIR /scripts
COPY webpage.sh .
CMD ["chmod","+x","webpage.sh"]
CMD ["bash","webpage.sh"]
```
3. 빌드를 하고 실행한다.
   - docker build -t new_fortune .
   - docker images
   - docker run -d --name fortune new_fortune
   - docker ps
   - docker exec fortune cat /htdocs/index.html



### *) 만든 컨테이너 배포하기

- docker login
- docker tag 명령어로 이름 바꿔주기
- docker push



## 컨테이너 보관

## 컨테이너 사용

## 컨테이너 관리

## 컨테이너 볼륨

## 컨테이너 통신

## 빌드 운영