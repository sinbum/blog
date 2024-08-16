# 문자열 바꾸기

sub 함수를 이용하면 정규식과 매치되는 부분을 다른 문자로 쉽게 바꿀수 있습니다.

다음 예제 입니다.

## sub()

```python
import re
p = re.compile('(blue|white|red)')
p.sub('colour', 'blue socks and red shoes') # 'colour socks and colour shoes'
```

sub 함수의 첫번째 매개변수는 바꿀 바꿀 문자열이고 두번째 매개 변수는 대상이 되는 문자열입니다. 앞서 가져온 패턴에서 두번째 인자 로 대상이 되는 문자열을 수정하여 적용할 수 있습니다.

추가 옵션으로 다음과같이 카운트 값을 두어 처음 탐색되는 인자로 한번만 바꿀수 있습니다.

```python
p.sub('colour', 'blue socks and red shoes', count=1) # 'colour socks and red shoes'
```

### sub 함수 참조 구문 사용

sub 메서드를 사용할 때에는 참조 구문을 사용할 수있습니다.

```python
import re

p = re.compile(r"(?P<name>\w+)\s+(?P<phone>(\d+)[-]\d+[-]\d+)")

print(p.sub("\g<phone> \g<name>", "park 010-1234-1234")) # 010-1234-1234 park
```

위 코드에서의 패턴은 각각의 그루핑으로 name과 phone 패턴을 만들어 주었습니다.\
바꾸고 싶은 문자열에 \g<그룹이름> 을 입력한다면 정규식의 그룹과 이름을 참조 할 수 있게됩니다.

### sub 메서드의 매개변수로 함수 사용

매개변수로써 return 값을 가지는 함수를 사용 할 수도 있습니다. 다음 예를 살펴 보도록 하겠습니다.

```python
import re

def hexrepl(match):
    value = int(match.group())
    return hex(value)

p = re.compile(r'\d+')
result = p.sub(hexrepl, 'Call 65490 for printing, 49152 for user code.')

print(result) # 'Call 0xffd2 for printing, 0xc000 for user code.'
```

hexrepl 함수는 매개변수를 match 객체를 입력으로 받아서 16진수로 변환해 돌려주는 함수입니다. sub의 첫번째 매개변수로 함수를 사용 할 경우에 해당 함수의 첫번째 매개변수에는 정규식과 매치된 match객체가 입력이 됩니다.\
그리고 매치되는 문자열은 함수의 반환 값으로 출력됩니다.

## subn() - 부가 함수

sub() 함수와 동일하지만 반환 결과를 튜플의 형식으로 돌려준다는 것에 차이점이 있습니다. 첫번째 요소는 결과값이고 두번째 요소는 바뀐 횟 수를 말합니다.

```python
import re

p = re.compile('(blue|white|red)')
p.subn( 'colour', 'blue socks and red shoes') # ('colour socks and colour shoes', 2)
```
