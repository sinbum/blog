# 그라파나(Grafana)란?

![그라파나 로고](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f5b5d065-3617-4855-a86c-c8fa93a870fb/9c82520bd5e035c892676622e795f2f9fd37978fba110780c33ef4db02d3f3ed.m.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220630%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220630T074100Z&X-Amz-Expires=86400&X-Amz-Signature=98c66db5b445fe49c830bd7a2aa4e8c12909e0b50cb76d4adcd57194d85077e7&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%229c82520bd5e035c892676622e795f2f9fd37978fba110780c33ef4db02d3f3ed.m.png%22&x-id=GetObject)

## 그라파나 설명

그라파나는 오픈소스 메트릭 데이터 시각화 도구 입니다.

그라파이트Graphite, 인플럭스DBInfluxDB, 오픈TSDBOpenTSDB 등을 지원하는 오픈소스 대시보드 도구로 개발 되었습니다.

현재 그라파나 랩Grafana Labs에서 개발하고 있습니다.

### 그라파나의 시작

2019년 10월 시리즈 A $24M, 2020년 8월 시리즈B $50M의 투자를 유치했습니다.

2020년 현재 그라파나 랩은 32개 국가에서 리모트를 기반으로 운영되는 170명 규모의 회사로 성장그라파나 엔터프라이즈Grafana Enterprise와 그라파나 클라우드Grafana Cloud와 같은 상용 서비스도 개발하고 있습니다.

### 사용하는 기업

그라파나를 사용하는 대표적인 기업은 다음과 같습니다.

- 인텔 Intel
- 테드 TED
- 페이팔 Paypal
- 이베이 ebay
- 디지털 오션 Digital Ocean
- 랙스페이스 rackspace,
- 비메오 Video

### 그라파나(Grafana) 와 데이터독(Datadog)

그라파나와 데이터독 같은 클라우드 모니터링 서비스는 메트릭 데이터를 시각화하고 대시보드를 구성할 수 있다는 점에서 비슷한 특징을 가지고 있습니다.

- 그라파나
    - 외부 데이터 소스를 동적으로 시각화함(최신 데이터 확인가능)
    - 오픈소스
- 데이터독
    - 데이터를 일정주기로 가져옴
    - 상용소스

## 도커를 사용해 그라파나 설치하기

- [grafana/grafana - Docker Hub](https://hub.docker.com/r/grafana/grafana/)

그라파나에서는 grafana/grafana 이미지를 공식적으로 제공하고 있습니다.

```
$ docker run -d -p 3000:3000 grafana/grafana
```

기본 계정은 admin / admin입니다.

그라파나를 사용하려면 먼저 데이터 소스를 정의해야 합니다.

## 그라파나 사례 (테슬라 대시보드)

그라파나를 대시보드로 사용해 테슬라 자동차의 데이터를 가져와 시각화한 프로젝트

- [adriankumpf/teslamate: A self-hosted data logger for your Tesla 🚘](https://github.com/adriankumpf/teslamate)

위 내용은 [44BITS](https://www.44bits.io/ko/keyword/grafana)님의 글을 참고하여 정리 및 재작성 되었습니다.