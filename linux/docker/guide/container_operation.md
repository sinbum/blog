
## 컨테이너 관리
실행중인 컨테이너의 관리의 대표적인 명령어는 다음과 같습니다.
ps,top,webserver

- 실행중인 컨테이너 목록 확인
- 포그라운드로 실행중인 컨테이너에 연결
- 동작중인 컨테이너에 NEW 명령어 추가 실행
- 컨테이너에서 동작되는 프로세스 확인
- 동작중인 커네팅너가 생성한 로그 보기

### 실행중인 컨테이너 목록 확인
docker ps webserver
### 포그라운드로 실행중인 컨테이너에 연결
docker attach [옵션] 컨테이너 이름
docker attach centos
### 동작중인 컨테이너에 NEW 명령어 추가 실행
docker exec -it webserver /bin/bash
### 컨테이너에서 동작되는 프로세스 확인
docker top
### 동작중인 커네팅너가 생성한 로그 보기
docker logs
docker logs -f

docker top 이미지
- 도커의 컨테이너가 실행하기위한 프로세스들을 나타냅니다.
- 도커가 실행중인 웹서버 컨테이너 목록을 나타냅니다.
  docker logs webserver
- 현재 런닝 중 인 컨테이너의 로그정보를 나타냅니다.
  docker exec webserver /bin/bash
- 현재 실행중인 컨테이너에 추가로 bash를 실행하고 싶을 때 쓰는 명령어입니다.
