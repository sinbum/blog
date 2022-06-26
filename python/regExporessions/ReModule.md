
# re 모듈

## re 의사용
```python
import re

# pattern P
p = re.comple('ab*')
```

re.compile을 사용해 정규식을 컴파일 합니다. re.compile의 결과로 돌려주는 객체 p(컴파일 패턴 객체)를 사용해 그 이후 작업을 수행 합니다.

- 정규식을 컴파일 할 때 특정 옵션을 주는 것도 가능합니다.
- 패턴은 정규식을 컴파일한 결과입니다.

## 문자열검색 with 정규식
컴파일된 패턴객체를 사용해 문자열 검색을 수행합니다.
컴파일된 패턴 객체는 다음과 같은 4가지의 함수 기능을 제공합니다.

| Method	     | 목적                                            |
|-------------|-----------------------------------------------|
| match()	    | 문자열의 처음부터 정규식과 매치되는지 조사한다.                    |
| search()	   | 문자열 전체를 검색하여 정규식과 매치되는지 조사한다.                 |
| findall()	  | 정규식과 매치되는 모든 문자열(substring)을 리스트로 돌려준다.       |
| finditer()	 | 정규식과 매치되는 모든 문자열(substring)을 반복 가능한 객체로 돌려준다. |

match,search 함수는 정규식과 매치 될때 match 객체를 반환하고, 그렇지 않을때는 'None'을 반환합니다.
아래 예제를 통해 직접 살펴 보겠습니다.

```python
import re
p = re.compile('[a-z]+')
```

## match()
- match 함수는 문자열의 처음부터 정규식과 매치되는지 조사합니다. 위에서 선언한 패턴에서 매치 함수를 사용해 보겠습니다.
  ```python
  m = p.match("python")
  print(m) # <re.Match object; span=(0,6), match='python'>  
  ```
"**python**" 문자열은 '[a-z]+' 패턴 정규식에 매치됨으로 match 객체를 반환합니다.

다음은 "3 python" 이라는 문자열을 매치함수로 적용 시켜보겠습니다.

```python
m = p.match("3 python")
print(m) # None
```

"none"을 반환 하는 것을 확인해 볼 수 있습니다.

매치의 결과로 match 객체 또는 None을 똘려주기 때문에 파이썬 정규식 프로그램은 다음과같이 조건문인 if문을 추가하여 다음과 같은 흐름으로 작성합니다.

```python
p = re.compile({정규표현식})
m = p.match( 'string goes here' )
if m:
    print('Match found: ', m.group())
else:
    print('No match')

```

## search()

컴파일된 패턴 객체 p를 가지고 search 함수를 사용해 보도록 하겠습니다.

```python
m = p.search("python")
print(m) # <re.Match object; span=(0, 6), match='python'>
```

match함수는 None을 반환 했지만 Search함수는 문자열 전체에서 패턴을 검색했기 때문에 match를 반환 하였습니다.

match 함수와 search 함수는 문자열의 청므부터 검색할지 의 여부에 따라 다르게 사용해야 합니다.


## findall()
```python
result = p.findall("I deream code python everyday")
print(result) #['deream', 'code', 'python', 'everyday']
```

"I deream code python everyday" 문자열의 'deream', 'code', 'python', 'everyday' 단어를 p 패턴으로 설정한 '[a-z]+' 정규식과 매치해서 리스트로 반환합니다.
대문자 패턴은 입력하지 않았으므로 "I"는 리스트에 반환 시키지 않았습니다.


## finditer()
이번에는 finditer 함수를 실행시켜 보도록 하겠습니다.
```python
result = p.finditer("life is too short")
print(result) # <callable_iterator object at 0x0000017F83444820>

for r in result: print(r)

# 결과값은 아래와 같습니다.
# <re.Match object; span=(2, 8), match='deream'>
# <re.Match object; span=(9, 13), match='code'>
# <re.Match object; span=(14, 20), match='python'>
# <re.Match object; span=(21, 29), match='everyday'>
```
finditer는 findall과 동이랗지만 그 결과로 반복 가능한 객체를 반환하도록합니다.

반복 가능한 객체가 포함하는 각각의 요소는 match 객체입니다.

## match 객체의 함수.
이제 match함수의 search메서드를 수행한 결과로 돌려준 amtch 객체에 대해서 알아보도록 하겠습니다.
앞에서 정규식을 사용한 문자열 검색을 수행하면서 알아보도록 하겠습니다.

- 어떤 문자열이 매치되었는지.
- 매치된 문자열의 인덱스 위치는 어디서 부터 어디까지 인지.

match 객체의 메서드를 사용하면 다음과 같은 데이터의 정보를 얻을 수 있습니다.

| method	 | 목적                               |
|---------|----------------------------------|
| group() | 	매치된 문자열을 돌려준다.                  |
| start() | 	매치된 문자열의 시작 위치를 돌려준다.           |
| end()	  | 매치된 문자열의 끝 위치를 돌려준다.             |
| span()	 | 매치된 문자열의 (시작, 끝)에 해당하는 튜플을 돌려준다. |

```python

 m = p.match("python")
 m.group() # 'python' 
 m.start() # 0
 m.end() # 6
 m.span() # (0, 6)
```
예상한 대로 결과 값이 출력되는 것을 확인 할 수 있습니다. search 함수를 이용했다면 start() 값은 다르게 나올 수있습니다.

```python
m = p.search("3 python")
m.group() # 'python'
m.start() # 2
m.end() # 8
m.span() # (2, 8) 
```

# 모듈 단위로 수행해보기

```python
p = re.compile('[a-z]+') # 문자열의 패턴을 가진 패턴을 지정합니다.
m = p.match("python")
```
**코드**를 축약 하면 **다음**과 같습니다.
```python
m=re.match('[a-z]+',"python")
```
위에서 처럼 사용하면 컴파일과 함수를 한 번에 수행 할 수 있습니다. 보통 한번 만든 패턴 객체를 여러번 사용해야 할 떄는 이방법보다 컴파일을 지정해 주는 것이 훨씬 바람직 합니다.

## 컴파일 옵션
정규식을 컴파일 선언시에 다음의 옵션을 사용할 수있습니다.
- DOTALL(S) = .이 줄바꿈 문자를 포함해 모든 문자와 매치 할 수 있도록 합니다.
- IGNORECASE(I) - 대소문자에 관계없이 매치할 수 있도록합니다.
- MULTILINE(M) - 여러줄과 매치할 수 있도록 합니다. (^,$메타문자의 사용과 관계가 있는 옵션입니다.)
- VERBOSE(X) -VERbose 모드를 사용할 수 있도록 합니다.(정규식을 보기 편하게 만들수도 있고, 주석등을 사용할 수 있습니다.)

옵션을 사용할때는 're.DOTALL' 로 전체 옵션에 이름을 써도되고 're.s' 약어를 써도 가능합니다.

## DOTALL, S
'.'메타 문자는 줄바꿈 문자 '\n' 을 제외한 모든 문자와 매치되는 규칙이 있습니다.   
만약에 '\n' 문자도 포함해 매치하고 싶다면 're.DOTALL' 또는 're.s' 옵션을 사용해 정규식을 컴파일 하면 됩니다.

예제 코드를 살펴보도록 하겠습니다.

```python
import re
p = re.compile('a.b')
m = p.match('a\nb')
print(m) # None
```
\n 문자와도 매치되게 하려면 다음과 같이 re.DOTALL 옵션을 사용해야 합니다.

```python
p = re.compile('a.b', re.DOTALL)
m = p.match('a\nb')
print(m) <re.Match object; span=(0, 3), match='a\nb'>
```
보통 're.DOTALL' 옵션은 여러 줄로 이루어진 문자열에서 줄바꿈처리가 상관없이 검색할 때 많이 사용합니다.

## GINORECASE, I
're.IGNORECASE' 또는 're.I' 옵션은 대소문자 구별 없이 매치를 수행할 때 사용하는 옵션입니다.

```python
p = re.compile('[a-z]+', re.I)
p.match('python') # <re.Match object; span=(0, 6), match='python'>
p.match('Python') # <re.Match object; span=(0, 6), match='Python'>
p.match('PYTHON') # <re.Match object; span=(0, 6), match='PYTHON'>
```
'[a-z]+' 정규식은 소문자만을 의미하지만 re.I 옵션으로 대소문자를 구별없이 매치 할 수 있습니다.


## MULTILINE, M

re.MULTILINE 또는 re.M 옵션은 '^','$'와 연관된 옵션입니다.
- '^' 메타 문자는 문자열의 처음을 의미합니다.
- '$' 메타 문자는 문자열의 마지막을 의미합니다.
- '^python' 인경우 문자열의 처음은 python으로 시작해야 매치가 됩니다.
- 'python$' 인경우 문자열의  끝 은 python으로 끝이나야 매치가 됩니다.

```python
import re
p = re.compile("^python\s\w+")

data = """
python one
I dream code python everyday
python two
you need python
python three
"""

print(p.findall(data))
```

위 정규식을 잘 해석 해보면 정규식 '^python\s\w+'는
- 'python'이라는 문자열로 시작한다. '^python'
- 다음에는 공백이온다 '^python\s'
- 그뒤에 단어가 와야한다 '^python\s\w+'

**'^'** 문자를 각라인의 처음으로 인식시키고 싶은 경우에 사용할 수 있는 옵션이 're.MULTILINE' 또는 're.M' 입니다.  
코드는 다음과 같습니다.
```python
import re
p = re.compile("^python\s\w+", re.MULTILINE)

data = """python one
I dream code python everyday
python two
you need python
python three"""

print(p.findall(data))
# ['python one', 'python two', 'python three']
```

> 코드의 세계는 신비롭지 않나요.
처음에 정규식을 잘 사용할 줄 몰랐을때에는 포기하고 string을 기교를 부리며 하드코딩 한적이 많았습니다.   
그럴때마다 한계에 부딪히고는 했습니다. 그러나 정규식을 잘사용한다면 많은 에너지 소모를 줄일 수 있지 않나 생각해봅니다.


## VERBOSE, X
정규식 전문가들이 만든 정규식을 보면 거의 암호 수준입니다.    
정규식을 이해하려면 하나하나 뜯어보아야합니다.  
여기에 주석을 추가 할 수있다면 가독성이 추가됨으로 훨씬 빠른 이해를 도울 수있습니다.

이떄 바로 필요한것이 **re.VERBOSE** 입니다.

```python
charref = re.compile(r'&[#](0[0-7]+|[0-9]+|x[0-9a-fA-F]+);')
```

위와같은 코드의 정규식은 실제로 이해하기 어렵습니다. 따라서 다음과 같은 예제로 풀어보도록 하겠습니다.

```python
charref = re.compile(r"""
 &[#]                # Start of a numeric entity reference
 (
     0[0-7]+         # Octal form
   | [0-9]+          # Decimal form
   | x[0-9a-fA-F]+   # Hexadecimal form
 )
 ;                   # Trailing semicolon
""", re.VERBOSE)
```
- re.VERBOSE 옵션을 사요하면 문자열에 사용된 whitespace는 컴파일 할때 제거됩니다.('[]' 안에서 사용한 whitespace는 제외 입니다.)
-  줄단위로 '#'을 사용해 주석을 작성 할 수있습니다.

## 백슬러시 문제
정규 표현식을 파이썬에서 사용할 때 혼란을 주는 요소가 한 가지 있는데, 바로 백 슬러시(\) 입니다.  
예를 들어 어떤 파일 안에 있는 "\section" 문자열을 찾기 위한 정규식을 만든다고 가정해 봅시다.

**\section**

이 정규식은 '\s'문자가 whitespace로 해석되어 의도한 대로 매치가 이루어지지 않습니다.
위 표현은 다음과 같이 동일한 이ㅡ미가 됩니다.
'[ \t\n\r\f\v]'ection

의도한 대로 매치하고 싶다면 다음과 같이 변경해야 합니다.
**\\section**

정규식에서 사용한 \문자가 문자열 자체임을 알려 주기 위해서 백슬래시 2개를 사용해 escape 탈출 처리 해야합니다.
따라서 위 정규식을 컴파일 하려면 다음과 같이 작성 하도록합니다.

```python
p = re.compile('\\section') # 문제발생 >> '\\\\section'으로 사용해야 \\section을 인식.
```
- 그러나 여기에서 또하나의 문제가 발견됩니다.
- 위처럼 정규식을 만들어서  컴파일 하게된다면 실제로 문제가 발생합니다.
- 파이썬 정규식 엔진에는 파이썬 문자열 리터럴 규칙에 따라서 \\이 \로 변경되어 '\section'이 전달됩니다.
- 결국 '\\\\section' 으로 백슬러시를 4개나 사용해야 합니다.
>※ 이 문제는 위와 같은 정규식을 파이썬에서 사용할 때만 발생한다(파이썬의 리터럴 규칙). 유닉스의 grep, vi 등에서는 이러한 문제가 없습니다.


위와 같은 문제로 파이썬 정규식에는 Raw String 규칙이 생겨나게 되었습니다. 컴파일 해야하는 정규식이 RawString임을 알려 줄 수있도록 문법을 만든것입니다. 그 방법은 다음과 같습니다.
```python
p = re.compile(r'\\section')
```

위와 같이 정규식 문자열 앞에 r문자를 삽입시 Raw String 규칙에 의해 백슬래시 2개 대신 1개만 써도 2개를 쓴 것과 동일한 의미를 갖게 됩니다.
