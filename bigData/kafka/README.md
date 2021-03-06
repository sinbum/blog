# 카프카 총정리
---

| 로고                                                                                 | 개념도                                                                                |
|------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| ![아파치카프카](https://i.pinimg.com/564x/f2/80/1a/f2801a2555451906d4e0ced138039b0f.jpg) | ![카프카개념도](https://i.pinimg.com/564x/e5/6a/db/e56adbb7b7761e1f50bf90c8a1765607.jpg) |

## 카프카 기본 개념

- 카프카 : 카프카 클러스터를 포함한 이벤트 스트림 프로세스 아키텍처.
- 브로커 : 카프카 클러스터의 서버 중 하나. 데이터를 저장하고 전달.
- 토픽 : 카프카 클러스터에서 데이터를 구분하는 단위. 토픽은 최소 1개 이상의 파티션을 가짐
- 파티션 : 토픽에서 데이터를 논리적으로 구분하는 단위
- 레코드 : 메시지를 담는 가장 작은 크기.
    - 오프셋 : 프로듀서가 보낸 데이터가 브로커에 저장되었을 시에 받는 고유 번호. 인덱스 번호.
    - 타임스탬프 : 레코드가 프로듀서에서 생성 되었을 때 시간.
    - 헤더 : 레코드의 키/값 저장영역.
    - 메시지 키: 데이터를 구분하는 값. 실제 db에서 사용되는 primary key 또는 json의 키 개념이 비슷하다.
    - 메시지 값: 밸류값.

## 카프카 프로듀서

- 카프카 프로듀서 : 카프카 브로커로 데이터를 전달하는 역할을 하는 어플리케이션.
- 파티셔너 : 메시지 키를 토대로 파티션을 지정하는 클래스. 직접 커스텀하여 로직 변경 가능.
- 어큐뮤레이터 : 레코드 전송시 배치로 묶는 역할.
- acks : 레코드를 카프카 클러스터로 전송시에 전달 신뢰성을 지정함.
- min.insync.replicas : acks=all 일 경우 최소 적재 보장 파티션 개수.
- enable.idempotence : 멱등성 프로듀서로 동작하기 위해 설정하는 옵션.
- transactional.id : 트랜잭션 프로듀서로 동작하기 위해 설정하는 옵션.

## 카프카 컨슈머

- 카프카 컨슈머 : 카프카 클러스터에 저장된 레코드를 받와서 처리하느 어플리케이션.
- 컨슈머 그룹 : 동일한 역할을 하는 컨슈머들의 묶음.
- 컨슈머 랙 : 파티션에서 가장 최근의 레코드 오프셋과 컨슈머 오프셋간의 차이. 또는 차이 시간을 말함.
- 커밋 : 컨슈머가 레코드 처리가 완료되었을 경우 카프카 클러스터에 마지막으로 읽은 레코드의 오프셋 번호를 저장하는 작업.
- 리밸런싱 : 컨슈머 그룹에서 컨슈머 개수의 변화 또는 파티션 개수의 변화로 인해서 할당이 변경되는 작업.
- auto.offset.reset : 컨슈머 그룹이 없을 경우 처음 읽을 오프셋의 위치를 지정하는 옵션.
- isolation.level : 트랜잭션이 완료된 레코드를 읽을 것인지 판단하는 옵션.


## 카프카 스트림즈

- 카프카 스트림즈 : 상태/비상태 기반 스트림 데이터 처리를 수행하는 어플리케이션.
- 태스크 : 스트림즈 어플리케이션 내부에서 생성되어서 로직을 수행하는 최소 단위.
- 프로세서 : 데이터를 처리,가져오기,보내기
- 스트림 : 프로세서로 부터 처리된 데이터를 다른 프로세스로 전달되는 레코드
- 스트림즈DSL : 추상화 되어 스트림 프로세싱에 필요한 메서드들을 정의한 메서드들의 모음.
- 프로세서API : 스트림즈 dsl에서 구현할 수 없는 로직을 구현할 때 사용하는 API.
- KStream : 레코드의 흐름, 컨슈머의 poll()과 유사함.
- kTable : 특정 파티션의 메시지 키를 기준으로 가장 최근의 레코드들의 묶음.
- 코파티셔닝 : 동일한 파티션 개수, 동일한 파티셔닝 전략을 통해 레코드가 저장된 서로 다른 2개의 토픽.

## 카프카 커넥트

- 카프카 커넥트 : 카프카 기반 데이터 파이프라인을 반복적으로 생성할 때 사용하는 어플리케이션.
- 소스 커넥터 : 특정 파일 또는 소스 어플리케이션으로부터 토픽으로 데이터를 보내는 프로듀서.
- 싱크 커넥터 : 토픽에서 특정 파일 또는 소스 어플리케이션으로 데이터를 보내는 컨슈머.
- 오픈소스 커넥터 : 소스/싱크 커넥터를 사용할 수 있도록 jar형태로 배포하는 커넥터.
- 태스크 : 커넥터에서 데이터를 처리하는 최소 로직 단위.
- 단일 모드: 디버깅, 테스트용으로 적합한 1프로세스 단위 커넥트
- 분산 모드: 상용환경 운영에 적합한 멀티 프로세스 단위 커넥트
