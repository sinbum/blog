---
description: OGG:OracleGoldenGate
---

## data Integration 의 필요성.

빅데이터 시대에서 데이터의 보관 및 수집은 아주 중요합니다. 그러한 관점에서 데이터 인테그레이션 비용과 운영이 미치는 영향은 상당합니다.
ETL 처리를 위한 데이터양은 무수히 증가 하고있습니다.

이러한 문제를 해결하기 위해 오라클에서는 OGG(OracleGoldenGate)를 CDC의 솔루션으로 가지고 있습니다.

## OGG

OGG는 소스 시스템의 데이터베이스에 접근합니다. 예를들면 Oracle,Mssql,Mysql 등 대표적인 데이터 베이스 시스템에서 타겟이 되는 데이터 베이스 시스템으로 프로듀싱 하는 것과 같습니다. 카프카를 대표적으로 사용하는
컨플루언트 CDC 솔루션에서의 로그마이너와 그 개념이 비슷합니다.

![OGG Process Vriable Method / 출처: 오라클](https://docs.oracle.com/goldengate/1212/gg-winux/GWUAD/img/goldengate_configs2.jpg)

## OGG Architecture

ogg 아키텍쳐는 양방향 데이터 복제 또는 1:다, 다:1 등 으로의 모델이 가능하며 데이터의 redo/Archive log 파일을 두번이씩 읽을 필요가 없어 부하를 최소화 시킬 수  있는 장점이 있습니다.

이처럼 목적에 따라 복제 프로세스를 어떻게 구성하는가에 따라 데이터를 공유하고 통합 할 수 있는것이 OGG의 특징 입니다.

![OGG Architecture1 / 출처: rackspace.com](https://docs.rackspace.com/blog/oracle-goldengate-microservices-architecture/Picture1.png)
![OGG Architecture2 / 출처: 오라클](https://docs.oracle.com/goldengate/1212/gg-winux/GWUAD/img/logicalarch2.jpg)
![OGG Architecture3 / 출처: dataonair](https://dataonair.or.kr/publishing/img/knowledge/okm-2011-autumn-trend4-522338-11.png)

경영의사 결정을 위한 분석통계, 고가용성을 위한 서버운영, 부하 분산 등 CDC솔루션이 가지고 있는 장점은 많습니다. 

오라클에서 내놓은 솔루션인만큼 CDC 에서의 기술력은 확실하지만 입장에 따라서 비용은 누구에게는 부담이 될 수 있고 누구에게는 효율적 일 수 있습니다.

그러므로 오픈소스를 활용한 빅데이터 아키텍처를 제시하기도 합니다.
