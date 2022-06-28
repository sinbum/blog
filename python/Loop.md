# 반복문

자동화 혹은 컴퓨팅 프로그램을 위한 필수 조건은 제가 생각하기에 **반복**과 **조건**입니다.
반복과 조건을 통해 코드가 완성이 되고 알고리즘 잘 표현해 낼 수 있는 영역입니다. 

아직 감이 잘 안오신다구요? 저와 함께 시작해보시죠.

## 파이썬의 기본 구조.
파이썬의 기본구조는 다음과 같습니다.

```python
for 반복문내변수 in 리스트:
    수행할 문장1 또는 함수1
    수행할 문장2 또는 함수2    
```

1. 전형적인 반복문
```python
list_test = ['apple', 'banana', 'mango'] 
for i in test_list: 
print(i)
```

2. 다양한 반복문 사용
```python
a = [(1,2), (3,4), (5,6)]
for (first, last) in a:
    print(first + last)
```
## for문과 continue
for 문은 숫자 리스트를 자동으로 만들어 주는 range함수와 함께 경우 하는 경우가 많습니다.

반복문에서의 'continue' 는 'while' 을 포함하여 어디서든 사용이 가능합니다.
'continue'는 반복문의 다음 시점으로 이동을 말합니다. 반복문 내에서는 반복이 지속됨으로 써 오류가 발생하거나, 하위 코딩을 실행시키거나, 불필요 할때 많이 사용합니다.

아래는 예제 입니다.

```python
# marks2.py 
marks = [90, 25, 67, 45, 80]

number = 0 
for mark in marks: 
    number = number +1 
    if mark < 60:
        continue 
    print("%d번 학생 축하합니다. 합격입니다. " % number)
```

점수가 60점 미만인 경우 하위 코드를 더이상 실행하지 않고 조건문이 만족하거나 만족하지 못할 경우 continue 실행 시키기 위한
코딩이 된다고 말할 수 있습니다. 

```python
C:\doit>python marks2.py
1번 학생 축하합니다. 합격입니다.
3번 학생 축하합니다. 합격입니다.
5번 학생 축하합니다. 합격입니다.
```

## Comprehension
리스트를 만드는 강력하고 간결한 방법입니다
초보자에게는 쉽지 않을 수도 있지만 주어진 리스트에서 홀수만 뽑아내는 코드를 작성해 보도록 하겠습니다

```python
print()pyhthon
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
odd_numbers = []

for number in numbers:
if number % 2 == 1:  # 2로 나눴을 때 1이 남으면 홀수입니다.
odd_numbers.append(number)
```
```python
odd_numbers = [number for number in numbers if number % 2 == 1]
```

**컴프리헨션을**이용하면코드가 훨씬 간편해 질 수 있습니다. 
[number for number in numbers if number % 2 == 1]