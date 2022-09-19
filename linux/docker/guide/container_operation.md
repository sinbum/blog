
## 컨테이너 관리
실행중인 컨테이너의 관리의 대표적인 명령어는 다음과 같습니다.
ps,top,webserver


### 컨테이너 관리 명령어
- 실행중인 컨테이너 목록 확인
  - docker ps webserver
- 포그라운드로 실행중인 컨테이너에 연결
  - docker attach [옵션] 컨테이너 이름
  - docker attach centos
- 동작중인 컨테이너에 NEW 명령어 추가 실행
  - docker exec -it webserver /bin/bash
- 컨테이너에서 동작되는 프로세스 확인
  - docker top
  - docker top {이미지_이름}
    - 도커의 컨테이너가 실행하기위한 프로세스들을 나타냅니다.
    - 도커가 실행중인 웹서버 컨테이너 목록을 나타냅니다.
      docker logs webserver
    - 현재 런닝 중 인 컨테이너의 로그정보를 나타냅니다.
      docker exec webserver /bin/bash
    - 현재 실행중인 컨테이너에 추가로 bash를 실행하고 싶을 때 쓰는 명령어입니다.
- 동작중인 커네팅너가 생성한 로그 보기
  - docker logs
  - docker logs -f

### 하드웨어 리소스 제한
컨테이너는 호스트 하드웨어 리소스의 사용 제한을 받지 않습니다.   
하드웨어의 스펙에 따라서 용량 제한을 걸어두지 않으면 모든자원을 컨테이너가 사용할 수 있습니다. 
따라서 다른 애플리케이션의 효율적인 자원분배를 위해서 리소스를 직접 제한 해 주는 것이 좋습니다.

- 도커 커맨드를 통해 제한할 수 있는 하드웨어 자원들은 다음과 같습니다.
  - CPU
  - Memory
  - Ddisk I/O

### Memory 리소스 제한
제한 단위는 b,k,m,g 로 할당합ㄴ니다.

| 옵션                   | 의미                                                                                                                                                                                                                   |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --memory , -m        | 컨테이너가 사용할 최대 메모리 양을 지정합니다                                                                                                                                                                                            |
| --memory -swap       | 컨테이너가 사용할 스왑 메모리 영역에 대한 설정입니다.<br/> 메모리 + 스왑. 생략 시에는 메모리의 2배가 설정됩니다.                                                                                                                                                 |
| --memory-reservation | --memory 값보다 적은 값으로 구성하는 소프트 제한 값을 설정합니다.                                                                                                                                                                            |
| --oom-kill-disable   | OOM Killer 가 프로세스 Kill을 하지 못하도록 보호시킵니다.                                                                                                                                                                              |
| 명령 예)                | docker run -d -m 512m nginx:latest <br/>docker run -d -m 1g --memory-reservation 500m nginx <br/> docker run -d -m 200m --memory-swap 300m nginx:latest  <br/> docker run -d -m 200m --oom-kill-disable nginx:latest |


### CPU 리소스 제한
| 옵션            | 의미                                                                                                                                                    |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| --cpus        | 컨테이너에 할당할 CPU core 수 를 지정합니다.   <br/> --cpus= "1.5" 컨테이너가 최대 1.5개의 CPU 파워를 사용합니다.                                                                     |
| --cpuset-cpus | 컨테이너가 사용할 수 있는 CPU나 코어를 할당합니다.  <br/> --cpuset-cpus=0-4                                                                                               |
| --cpu-share   | 컨테이너가 사용하는 다른 애플리케이션 대비 CPU 비중을 1024 값을 기반으로 설정합니다. <br/> --cpu-share 2048 기본 값보다 두 배 많은 CPU 자원을 할당 하도록합니다.                                           |
| 명령 예)         | $ docker run -d --CPUS=".5U ubuntu:latest <br/> $ docker run -d --cpu-shares 2048 ubuntu:latest <br/> $ docker run -d --cpuset-cpus 0-3 ubuntu:latest |


### Block I/O 리소스 제한
블록 I/O 리소스는 컨테이너가 i/o 스케줄링을 갖을때 일부 선점을 시키도록 지정을 해줄 수 있습니다. 물리적인 읽기 쓰기 작업 속도를 제한하여 효율적인 리소스 관리를 할 수 있습니다.

| 옵션                                           | 의미                                                                                                                                                                                                                                                                                                                                                                                                                        |
|----------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --mlkio--weight <br/> --mlkio--weight-device | Block IO의 Quota를 설정할 수 있으며 100~1000까지 선택이 가능합니다 default는 500                                                                                                                                                                                                                                                                                                                                                              |
| --device-read-bps <br/> --device-write—bps   | 특정 디바이스에 대한 읽기와 쓰기 작업의 초당 제한을 kb,mb,gb 단위로 설정합니다.                                                                                                                                                                                                                                                                                                                                                                         |
| --device-read-iops <br/> --device-write-iops | 컨테이너의 read/write 속도의 쿼터를 설정합니다. <br/> 초당 quota를 제한해서 읽기 쓰기를 합니다. 0 이상의 정수로 표기함. <br/> 초당 데이터 전송량은 = IOPS * 블럭크기 (단위 데이터 용량)                                                                                                                                                                                                                                                                                               |
| 명령 예)                                        | $ docker run -it --rm --blkio-weight 100 ubuntu :latest /bin/bash <br/> $ docker run -it --rm --device-write-bps /dev/vda:1mb ubuntu:latest /bin/bash <br/> $ docker run -it --rm --device-write-bps /dev/vda:10mb ubuntu:latest /bin/bash <br/> $ docker run -it --rm --device-write-iops /dev/vda:10 ubuntu:latest /bin/bash <br/> $ docker run -it --rm --device-write-iops /dev/vda:100 ubuntu:latest /bin/bash <br/> |

### 컨테이너 모니터링
도커는 다음과 같은 명령어로 모니터링을 할 수 있습니다.

- docker monitoring commands
  - docker stat : 실행중인 컨테이너의 런타임 통계를 확인합니다.
    - docker stats [OPTIONS] [CONTAINER...]
  - docker event : 도커 호스트의 실시간 event 정보를 수집해서 출력합니다.
    - docker events -f container=<MAME>
    - docker image -f container=<MAME>
- cAdvicsor
  - 구글에서 만든 도커 모니터링 툴
  - [ cAdvicsor 깃허브 링크](https://github.com/google/cadvisor)
