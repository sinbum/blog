# ELT,ETL 이란?

---

추출하고 변환하고 적재하는 과정으로써 데이터가 생기는 지점이나 원천 데이터로부터 데이터를 가져오고 그것을 재사용하기 위해 통일성(데이터프레임)을 갖춘 형태를 가지며
다시 적재하는 과정을 말합니다.

쉽게 표현하면 여러 데이터를 가지고 변환해서 이쁘게 담는 것이라고 생각하면 됩니다.

- E: Extract
- T: Transform
- L: Load

ETL 과 ELT 사이에서는 사용 목적과 ‘key’ 차이에 있어서 아주 중요 하게 고려되어야 합니다.


## ETL
![참고 이미지](https://rivery.io/wp-content/uploads/2020/05/ETL-Process-for-linkedin3-1024x535.png)
[참고링크 : rivery.io/blog](https://rivery.io/blog/etl-vs-elt/)

ETL (Extract, Transform, Load)은  데이터 인테그레이션 기술로써 소스로부터 원천데이터를 변환 시켜 가져오도록합니다.
ETL은 1970년대 부터 시작된 방식이며, 온프레미스 데이터 방식에서 아주 강력하게 사용 되었습니다.
그러나 온라인 시장에서의 흐름으로 클라우드 서비스가 제공되며 그흐름이 점차 바뀌고 있습니다.



## ELT
![참고 이미지](https://rivery.io/wp-content/uploads/2020/05/ETL-Process-for-linkedin.png)
[참고링크 : rivery.io/blog](https://rivery.io/blog/etl-vs-elt/)

ETL과는 다르게 변환과 적재 방식에서 차이가 있습니다. 어떤 원천 데이터 소스로부터 먼저 적재 하는 방식으로 써 쓰입니다.
ELT는 새로운 개발 방식이며 온라인서비스의 시작으로 그 방법론이 변화되고 있습니다.   
예를 들어 ELT의경우 모든 데이터를 추출하고  Snowflake, Amazon Redshift, Google BigQuery 등 클라우드 서비스 등에 적재를 시작합니다. 필요할때마다 연산처리와 함께 먼저 적재된 데이터를 가지고 변환 및 데이터를 그때그때 받아볼 수 있습니다.
현재는 많이 사용 되는 방식은 아니지만 점점 유명해지는 추세이며 클라우드 인프라에서 그방식이 사용 되어지고 있습니다.

ELT를 사용하는 경우 다음과 같을때가 훨씬 효용가치가 있습니다.
- 방대한 양의 데이터를 보유한경우.
    - 현 시대에서는 방대한 양이 데이터가 증가되고 있습니다.
- 가능한 한 빨리 데이터를 보관해야 하는경우.
    - 연산처리가 이루어지기 전에 데이터를 적재하여 미리 로드합니다.
- 데이터를 처리 하는 자원이 부족한 경우.
    - ETL시 웨어하우스에 도착전 파이프라인에서 연산 및 데이터 변환 처리가 일어나야 합니다. 이때 자원사용량이 많을 수 있으므로 ELT 방식을 구축한다면 경제적으로 유연성을 가질 수 있습니다.