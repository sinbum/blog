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
이러한 이유로 우리는 리눅스 환경에서 도커를 사용합니다. 우

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




## 컨테이너 살펴보기

## 컨테이너 만들기

## 컨테이너 보관

## 컨테이너 사용

## 컨테이너 관리

## 컨테이너 볼륨

## 컨테이너 통신

## 빌드 운영