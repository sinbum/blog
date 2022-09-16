
## 컨테이너 보관

- Registry : 컨테이너 이미지를 저장하는 저장소.
- Docker Hub : hub.docker.com
- Private Registry : 사내 컨테이너 저장소.

### 도커 허브

도커 허브는 깃허브와 마찬가지로 도커를 보관하는 웹 저장소의 개념입니다.

- https://hub.docker.com/
- image 종류 : Official Images, Verified Publisher 등등
- 이미지 검색 : $docker search ${keyword}

### Private Registry
registry 컨테이너를 이용해서 개인적, 또는 사내 컨테이너로 운영이 가능합니다.

```shell
docker run -d -p 5000:5000 --restart always --name registry registry:2
```

도커를 실행 후 다음과 같이 호스트네임과 포트번호를 입력 후 이미지 이름을 적어 주도록 합니다.

- image repository
    - localhost:5000/ubuntu:18.04
    - docker.example.com:5000/ubuntu:18.04


