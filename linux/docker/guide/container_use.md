
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

