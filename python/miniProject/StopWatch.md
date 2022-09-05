---
description : 간단한 스탑워치 만들기.
---

## 스탑워치 만들기.

- 필요한 라이브러리
- 클래스 개념필요.
- 코드 만들기.

## 필요한 라이브러리
스탑워치에 필요한 라이브러리는 datetime 만 필요합니다. 
실질적으로 datetime은 로그를 위해 직접 코드개발시 많이  효율적으로 사용하기 위해 많이 사용하는 라이브러리 이므로 기본적으로 알아두셔서 꼭 필요한 곳에 쓰시길 바라겠습니다!

##클래스 개념.

### init 메소드

클래스는 객체를 표현하기 위한 문법으로 개념이나 모양을 코드로 특정화 및 프로그래밍 한것을 객체 지향 프로그래밍이라고 합니다.
클래스에는 크게 속성과 메소드로 구분되는데, 속성의 경우 매개변수를 받고 사용하기 위한 값을 정의하며 메소드는 만들어진 속성들을 이용해서 어떤 행위를 하는 실행 코드라고 생각 하시면 됩니다.

파이썬 코드에서 '\_\_init\_\_' 메소드는 인스턴스를 생성할 떄 호출되는 특별한 메소드 입니다. 인스턴스를 초기화 하고 순서에 맞춰 각 인수를 self.속성값 으로 할당 합니다.

### 인스턴스 속성과 클래스 속성
이렇게 사용된 itit메소드나 각각 메소드에서 self로 사용한 속성을 인스턴스 속성이라고합니다.
인스턴스 속성은 인스턴스별로 각자 다른 값을 가지게 됩니다.


## 아래와 같이 코드를 생성합니다. datetime 라이브러리와 클래스를 사용해 간단히 구성합니다. 



```python
# coding=utf-8
from datetime import datetime


class StopWatch:
    def __init__(self):
        self.end_datetime = None
        self.start_datetime = None
        self.reset()

    def reset(self):
        self.start_datetime = None
        self.end_datetime = None

    def start(self):
        self.reset()
        self.start_datetime = datetime.now()

    def stop(self):
        self.end_datetime = datetime.now()
        print(self.get_elapsed_seconds())
        return self.get_elapsed_seconds()

    def get_elapsed_seconds(self):
        assert isinstance(self.start_datetime, datetime), 'call start() first'
        assert isinstance(self.end_datetime, datetime), 'call end() first'

        return self.end_datetime - self.start_datetime 

stopWatch = StopWatch()

stopWatch.start()
for i in range(100000000): pass
stopWatch.stop()

```
