# 오브젝트 스토리지

## 오브젝트 스토리지의 필요성

최근 네트워크 에서의 데이터는 비정형 데이터가 주를 이루고 있습니다. 우리가 유튜브를 영상으로 보는 것 또한 비정형데이터와 마찬가지죠.

비정형 데이터가 최근 기하급수적으로 늘어나고 있습니다. 시장 조사 기관인 IDC에 따르면 비정형 데이터는 25년까지 전체 데이터의 80퍼센트까지 차지할 것으로 보고 있습니다

또한 클리우드 기술과 빅데이터 및 인공지능의 기술향상에 따라서 전통적인 데이터 스토리지를 운영하는 기업들은 비정형 데이터를 쉽고 빠르게 이용할 수있는 아키텍처가 필요하게 되었고, 때문에 오브젝트 스토리지가 주요 스토리지로 자리잡게 되었습니다.

## 블록, 파일, 오브젝트

![블록,파일,오브젝트 개념도](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/70918737-7e41-48e7-882e-d946c2159bea/blockfileobject.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220630%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220630T113857Z&X-Amz-Expires=86400&X-Amz-Signature=b3dd501a0d542ee7efcbec7964062c0df973d655a2f1f8c8b0f857aa744a0f3c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22blockfileobject.png%22&x-id=GetObject)

- 블록 저장 방식
    - 데이터를 고정된 크기의 단위로 나누어 스토리지에 저장.
    - 각블록은 저장된 위치를 가리키는 고유의 주소를 가지고 있고 인덱싱을통해 분산저장이 가능하며 저장된 데이터를 찾아 하나의 데이터로 재구성.
- 파일 시스템 저장 방식
    - 윈도우 디렉토리 처럼 트리 형태의 구조로 되어있습니다.
    - 파일마다 위치,크기,생성일,블록위치 등 메타데이터를 가지고 있습니다.
    - 블록스토리지가 데이터를 블록으로 나누어 관리 및 파일 시스템이 계층형 구조로 파일에 저장

## 오브젝트의 특성

- 오브젝트 스토리지는 데이터를 **오브젝트(Object)** 단위로 관리
    - 데이터의 식별번호 (UUID 128비트) 부여
    - 메타데이터
    - 플랫 저장방식
    - 다양하고 방대한 정보를 담는것이 가능
    - 메타데이터의 커스터마이징이 가능 > 데이터 보호

## 오브젝트 스토리지 방식

오브젝트의 특성은 빅데이터 분석에 최적화 되어 있습니다.

예를 들어, CCTV 영상에 해당 영상의 이름이나 찍힌 날짜뿐 아니라 카메라 번호, 위치 정보, 이벤트 발생 시간 북마크 등의 메타데이터를 수집해 영상 검색에 활용하거나 해당 지역의 이벤트 발생 빈도 분석 등에 활용될 수 있습니다.

## 오브젝트, 파일 스토리지 의 비교

- 파일 스토리지
    - 계층형 구조 캐싱
    - 파일이 많을수록 메모리의 리소스 소모
    - 페타바이 트 규모의 환경에서는 성능적 제약 발생
    - 다른시스템으로 분산 필요
    - 성능 면에 있어서 구조가 단순하다는 점과 읽기 속도가 빠름
- 오브젝트 스토리지
    - 평면적 저장에 의한 뛰어난 확장성

### 오브젝트 스토리지의 일부 단점

- 메타데이터의 규모로 인한 입출력 오버헤드 발생
- 수정이 필요할경우 오브젝트 전체를 수정
- 소규모 데이터의 수정이 빈번하게 일어나는 경우 비효율적
- 환경 구성에 따른 성능 튜닝 필요
- 클러스터 내 저장한 위치에 대한 해시 테이블 알고리즘에 따른 성능 의존

![파일시스템과 오브젝트의 차이](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/bc5ef8f5-2bf7-4b5d-92b4-58679b63620f/filesystemvsobject.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220630%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220630T113842Z&X-Amz-Expires=86400&X-Amz-Signature=81ac7a4eb8f332a2d8c32e499903dbd38445e7e6a61456e130f1aeeb58d44feb&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22filesystemvsobject.png%22&x-id=GetObject)

## 오브젝트 스토리지의 활용

대규모 비정형 데이터에 낮은 빈도로 접근하는 환경에서 활용력이 높은 오브젝트 스토리지는 API를 통해 접근이 가능합니다. 이를 통해 직접적으로 접근할 수 있게 되고, 데브옵스(DevOps) 환경을 구성할 수 있게 되었습니다.

이러한 배경은 클라우드 스토리지 환경이 오브젝트 기반이 되는데 큰 역할을 하였습니다. 특히 많이 쓰이는 벤더는 AWS S3, MS Azure, GCP Storage 등이 있습니다.