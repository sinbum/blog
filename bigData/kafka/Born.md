## 카프카의 시작
---

![링크드인](https://content.linkedin.com/content/dam/me/business/en-us/amp/brand-site/v2/bg/LI-Logo.svg.original.svg)

2011년 구인/구직 플랫폼 이자 소셜 네트워크인 'Linkedin'은 여러 파편화되어있는 데이터 수집 분배 아키텍처를 운영하는 것에 어려움이 있었습니다.
시간이 지날수록 아키텍처는 거대해졌고 소스 애플리케이션과 타깃 애플리케이션의 개수가 점점 많아지면서 데이터의 흐름이 복잡해지기 시작했습니다.

![복잡한 운영구성 : 아파치 카프카 애플리케이션 프로그래밍|최원영](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F56e79358-20c3-4b7f-a2a6-d0459a778327%2FUntitled.png&blockId=abea803c-fdab-4164-aee2-b13c2f228e1d)


위 그림과 마찬가지로 링크드인 데이터 팀에서는 기존에 있던 사용프레임워크와 오픈소스를 아키텍처에 반영해 데이터 파이프라인의 파편화를 개선하려 노력하였습니다. 그러나 복잡도를 낮추는 아키텍처가 되지는 않았습니다.

다음 그림의 예시를 살펴보도록 하겠습니다.

![카프카를 사용한 통합 구성 : 아파치 카프카 애플리케이션 프로그래밍|최원영](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F77dae714-506c-432c-8170-c42cea02d8f0%2FUntitled.png&blockId=4d387161-deda-4f19-9401-a9b120e458ce)

링크드의 데이터팀은 그러한 고민끝에 위 그림과 같이 아키텍처를 구성할 수 있도록 플랫폼 형태의 어플리케이션을 개발 하였습니다.

카프카는 각각의 애플리케이션 끼리 연결해 데이터를 처리하는 것이 아니라 모든것을 한곳에 모아 처리할 수 있도록 중앙집중화 되었습니다.

![카프카 내부구조 : 아파치 카프카 애플리케이션 프로그래밍|최원영](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F9b9fd6b0-fa66-4914-b841-301851506841%2FUntitled.png&blockId=18fdec0b-90b5-4df9-a1e1-2bb9dfb84658)

기존의 1:1 매칭과는 다르게 데이터 소스는 카프카 내부에 파티션이라는 개념에 저장됩니다. 카프카 내부에 데이터가 저장되는 파티션의 동작은 FIFO 방식으로 적용됩니다.

그림에서 프로듀서로 보이는 것은 데이터가 토픽이라는 공간에 데이터가 들어갈 수있도록 제공하는 역할을 합니다.

컨슈머는 들어간 데이터에서 가져오는 역할을 합니다.