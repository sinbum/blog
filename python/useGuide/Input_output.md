# 입력,출력

## 입력하기

파이썬을 런타임 환경에서 실행할 경우 사용자가 글자를 입력하면 글자를 문자열로 받습니다. 또한 이 글자는 프로그램에 인자값으로 전달 할 수 있습니다. 괄호 안에 문자열을 넣으면 명령창에 글을 남길수 있습니다.

예제를 살펴 보도록 하겠습니다.

```python
word = input("hello there, input your message")
# hello there, input your message
```

## 출력하기

print()는 값을 출력해 주는 함수 입니다. 입력한 메세지나 값을 출력 할 수 있습니다. 프린트 함수 안에 값을 출력합니다.

```python
print("hello world") # 문자형 # hello world
print(1) # 숫자형 1
print(['a','b','c']) # 자료형  ['a','b','c']
```

## 입력과 출력

파이썬으로 입력하기 와 출력하기 를 함께 사용해 보도록 하겠습니다.

```python
word = input("hello there, input your message")
# hello there, input your message
print(word) # 입력한 값을 인자값으로 받아 출력합니다.
```
