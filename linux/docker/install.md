
## 도커 설치

* 도커 설치시 필요한 요소
* 사양
  * 운영체제 : 리눅스, windows
  * cpu:2core, memory: 2GB 이상
* 도커 설치하기
* VirtualBox 설치 - 네트워크 구성 - VM(가상머신)만들기
  * VM에 Ubuntu 20.04 설치하고 기본환경 구성
  * VM에 centos 설치하고 기본환경 구성
  * Ubuntu/CentOS Server에 Docker 설치

### VirtualBox 설치 - 네트워크 구성 - VM(가상머신)만들기

* VirtualBox 다운로드 후 설치
  * [https://www.virtualbox.org/](https://www.virtualbox.org/)
  * [vmware 설치 방법 링크](https://hiseon.me/linux/ubuntu/ubuntu-virtualbox-install/)
* VirtualBox - Network 구성
  * NAT 네트워크 추가 : 파일 - 환경설정 -네트워크 -추가
  * 네트워크 이름 : localNetwork
  * 네트워크 CIDR: 10.100.0.0/24
  * DHCP 지원
  * 포트포워딩
* 가상머신 만들기
  1. docker-ubuntu (cpu:2core, memory: 2GB 이상,network(local),disk(20GB))
  2. docker-centos (cpu:2core, memory: 2GB 이상,network(local),disk(20GB))

### VM에 Ubuntu 20.04 설치하고 기본환경 구성

* GUI 로그인 : guru / work
* 서버구성 : 네트워크설정
  * IP address : 동적할당 된 어드레스
  * hostname 변경 : /etc/hostname : docker-ubuntu.example.com
  * /etc/hosts 파일에 호스트 정보 추가 하기
* Text 부팅으로 수정
* root password 설정 : sudo passwd root - password
* SSH 서버 설치 후 운영
  * apt-get update && apt-get install -y openssh-server curl vim tree
* Xshell 로 로그인 구성하기.(원격 접속)
  * 그래픽 모드 : sudo systemctl isolate graphical.target
  * 텍스트 모드 : sudo systemctl isolate multi-user.target

### VM에 centos 설치하고 기본환경 구성

* CentOs 다운로드 링크 [https://centos.org](https://centos.org)
* 설치 후 환경구성하기.
  * 관리자 계정 : {id입력} / work\\
  * root password : {password입력}
  * 해상도 조절
  * 네트워크 구성:10.100.0.106/24,GW:10.100.0.1,DNS:10.100.0.1,
    * hostname:docker-centos.example.com
    * /etc/hosts 구성하기
      * 연결되어있는 네트워크 지정해주기.
      * 예) 10.100.0.106 {hostname 입력} {name 입력}
      * 예) 10.100.0.106 docker-centos.example.com docker-centos
    * text-login 구성
      * systemctl set-default multi-user.target
    * sshd 서비스 동작상태 확인하기.
      * systemctl status sshd
    * MobaXterm으로 세션 로그인 설정 후 접속. - 우분투에서의 원격 접속과 같음.

### Ubuntu/CentOS Server에 Docker 설치

* Docker 설치
  * 도커 문서 : [https://docs.docker.com](https://docs.docker.com)
* 설치방법
  * Repository를 이용해 설치
  * Download 후 직접 설치하기
  * Script를 이용한 설치
* 설치후 동작 상태 확인
  * 센트os 환경에서 os 부팅시 도커 작동 활성화
    * systemctl enable docker
* 사용자 도커 권한 할당.
  1. 수퍼유저 계정 접속. - su
  2. 도커에 권한 유저 추가 - usermod -a -G docker {사용계정 userid}\\
