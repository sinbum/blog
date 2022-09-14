
## 컨테이너 사용

### 컨테이너 이미지 사용방법

- 이미지 검색
- 이미지 다운로드
- 다운받은 이미지 목록 출력
- 다운받은 이미지 상세
- 이미지 삭제


#### 이미지 검색
 - docker search [옵션] <이미지이름:태그명>
 - 예) docker search database
 - 예) docker search nginx
 #### 이미지 다운로드
 - docker pull [옵션] <이미지이름:태그명>
 - 예) docker pull mysql:latest
 #### 다운받은 이미지 목록 출력하기
 - docker images
 #### 다운받은 이미지 상세보기
 - docker inspect [옵션] <이미지이름:태그명>
 - docker inspect nginx:latest
 #### 이미지삭제
 - docker rmi [옵션] <이미지이름>
 - docker rmi nginx



### 컨테이너 실행,종료

- 컨테이너 생성
- 컨테이너 실행
- 컨테이너 생성/실행
- 실행중인 컨테이너 목록 확인
- 동작중인 컨테이너 중지
- 컨테이너 삭제

#### 컨테이너 생성
docker create --name webserver nginx
#### 컨테이너 실행
docker start webserver
#### 컨테이너 생성/실행
docker run --name webserver -d nginx:latest
#### 실행중인 컨테이너 목록 확인
docker ps
#### 동작중인 컨테이너 중지
docker stop webserver
#### 컨테이너 삭제
docker rm webserver

### run 과 pull의 차이

도커의 사용 주기는 다음과 같다.

pull >> create >> start >> stop
run >> stop


### 컨테이너 관리
실행중인 컨테이너의 관리의 대표적인 명령어는 다음과 같습니다.
ps,top,webserver

- 실행중인 컨테이너 목록 확인
- 포그라운드로 실행중인 컨테이너에 연결
- 동작중인 컨테이너에 NEW 명령어 추가 실행
- 컨테이너에서 동작되는 프로세스 확인
- 동작중인 커네팅너가 생성한 로그 보기

#### 실행중인 컨테이너 목록 확인
docker ps webserver
#### 포그라운드로 실행중인 컨테이너에 연결
docker attach [옵션] 컨테이너 이름
docker attach centos
#### 동작중인 컨테이너에 NEW 명령어 추가 실행
docker exec -it webserver /bin/bash
#### 컨테이너에서 동작되는 프로세스 확인
docker top
#### 동작중인 커네팅너가 생성한 로그 보기
docker logs
docker logs -f

docker top 이미지
- 도커의 컨테이너가 실행하기위한 프로세스들을 나타냅니다.
- 도커가 실행중인 웹서버 컨테이너 목록을 나타냅니다.
docker logs webserver
- 현재 런닝 중 인 컨테이너의 로그정보를 나타냅니다.
docker exec webserver /bin/bash
- 현재 실행중인 컨테이너에 추가로 bash를 실행하고 싶을 때 쓰는 명령어입니다.

#### 도커 연습
1. 아파치 웹서버 컨테이너 이미지를 검색 후 다운로드 search,create
2. 다운로드한 아파치 웹서버를 백그라운드 실행(detach), 컨테이너 이름: web 으로 동작 시키기 (run)
3. 동작중인 컨테이너 목록 확인 후 web 컨테이너가 running 중인지 확인해보기 (ps)
4. 실행중인 web 컨테이너의 ip Address 확인 (inspect)
5. curl 명령으로 접속시도해보기.
6. web 컨테이너가 만들어내는 로그 출력
7. 실행중인 모든 컨테이너를 중지하고 삭제해보기.
8. 다운로드 된 컨테이너 이미지 삭제하기.