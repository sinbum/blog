문자열은 문자나 문자들을 합쳐서 나열한 것입니다. 값을 변경할 수 없고 순서를 가지고 있습니다.
또한 타입선언시에는 큰따옴표나 작은따옴표로 구분하여 작성합니다.
문자형에 대한 설명 [String](type.md)

# 포맷팅

포멧팅은 일정한 틀이나 정형화된 규칙을 선언하는 것을 말합니다. 
문자열에서의 포멧팅은 %d , %f ,%s 이라고 쓰며 다음과 같이 작성합니다.

- %d : 정수형 숫자 대입.
- %f : 실수형 숫자 대입.
- %s : 문자열 대입.

```python
print('My name is %s' % '최') # My name is 최
print('x = %d, y = %d' % (3, 2)) # x = 3, y = 2
print('%d x %d = %d' % (4, 5, 4+5)) # 2 x 3 = 6
```

# 포맷 함수.

포멧팅을 사용하는 것처럼 중괄호를 대입하고 **'{}'.fromat()** 함수를 사용함으로써 더욱 편리하게 이용 할 수있습니다.  
%d,%s,%f 등의 사용은 c언어서 많이 쓰이며 더 직관적이고 편리한 방법을 추구하는 파이썬에 가까운 방식입니다.  
또한 괄호에 숫자를 넣어 순서 지정 또한 가능합니다.

```python
print('My name is %s' % '최') # My name is 최
print('My name is {}'.format('최')) # My name is 최
print('{} x {} ={}'.format(5, 4, 5 * 4)) # 5 x 4 = 20
print('{1} x {0} ={2}'.format(1, 2, 1 * 2))  # 괄호 안의 숫자는 순서를 지정 2 x 1 = 2
```

# 인덱싱
인덱싱은 문자가 위치한 인덱스를 말합ㄴ지다.
- 인덱싱을 위용하여 문자열 내 각문자의 위치에 접근할 수 있습니다.
- 일부 sql에서는 인덱싱이 1부터 시작하는 경우도 있지만 코드 언어는 대부분 인덱스 위치가 0에서 시작됩니다.

```python
alphabet = 'abcd'
print(alphabet[0]) # a
print(alphabet[3]) # d
```

# 슬라이싱
- 문자열에서 인덱싱을 이용해 원하는 위치의 글을 잘라서 가져올 수 있습니다.
- 콜론을 이용합니다.

```python
str = 'Hello Python!'

print(str[0:1]) # H
print(str[0:2]) # He
print(str[3:7]) # lo P

# 앞 뒤 생략고 가능합니다.
print(str[:2]) # He
print(str[7:]) # ython!
```

# 메서드
함수라고도 하며 특정한 기능을 수행하기 위한 규칙입니다.
내가 만든 함수도 있고 남들이 만든 함수를 사용할 수도있습니다.

```python

def python_hello():
    return "hello python!"

def python_print(str):
    print(str)    
    
    python_print(python_hello()) # hello python! 

```
# end

- end: print() 함수에서 출력 끝을 주는 옵션입니다.
- 줄바꿈은 기본값입니다.
- 특정한 기능을 수행하기 위해 미리 정해둔 문자 조합을 이스케이프 코드라 합니다. [해당링크 참조](https://wikidocs.net/11524)

```python
print('python is fun', end=', well.. actually it is not')
```