# airflow

---

![airflow 로고](https://miro.medium.com/max/1400/1*c9NU5f4LQ_AAeV352szvMw.png)

---


## 에어플로우란  

airbnb에서 만든 workflow management tool

workflow는 작업의 흐름을 말합니다.
airflow는 ETL 에서 의 워크플로우를 작서아혹,스케줄링,모니터링 하는 작업을 말합니다.

데이터 엔지니어 영역에서 많이 사용되는 sw입니다.

Airflow는 특징이 되는 컴포넌트들이 있으며 각 컴포넌트들 사이에서의 아키텍처는 다음의 이미지로 표현됩니다.

![에어플로우 아키텍처](https://airflow.apache.org/docs/apache-airflow/stable/_images/arch-diag-basic.png)

## 에어플로우의 3가지 구성요소  

- Webserver
- Scheduler
- Executor
- Workers

### Airflow Webserver
Airflow의 웹 서버는 Airflow의 로그를 보여주거나 스케줄러에 의해 생산된 DAG목록, Task 상태 등을 시각화 해서 보여줍니다. 즉, UI를 통해서 사용자에게 시각적으로 정보를 제공해 주는 요소 입니다.

### Airflow Scheduler
Airflow 스케줄러는 airflow로 할당된 work들을 스케줄링 해주는 component 입니다. Scheduled 된 workflow들의 트리거링과 실행하기 위해서 executor에게 task를 제공해주는 역학을 수행합니다.



### Airflow Executor
Airflow Executor는 실행중인 task를 핸들링 하는 컴포넌트 입니다. 기본설치시에 scheduler에 있는 모든 것 들을 다 실행시키지만, production 수준에서의 executor는 worker에게 task 를 push 하도록 합니다.

### Airflow Worker
Airflow worker는 실제로 task를 실행하는 주체입니다.

### Airflow Database
Airflow database는 airflow에 있는 DAG, Task 등의 metadata를 저장하고 관리합니다.


###DAG(Directed Acyclic Graph)
DAG는 비순환 그래프로써 순환하는 사이클이 없는 그래프입니다. 즉, 노드와 노드가 단반향으로 연결되어 있어 그노드로 향하게 되면 돌아오지 않는다는 특성을 가지고 있습니다. Airflow에서는 이러한 DAG를 이용해 Workflow를 구성하여 어떤 순서로 task를 실행시킬 것인지 dependency를 어떻게 표현할 것인지 등을 설정합니다.
