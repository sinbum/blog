# 메타문자2
---


## 다른 메타문자
문자열 소비가 없는 메타 문자는 다음과 같습니다.
- |
- ^
- $
- \A
- \Z
- \b
- \B

## 메타문자 |
**|**   는 or와 동일한 의미로 사용된다. 'A|B' 라는 정규식의 경우 A 또는 B 가 됩니다.

```python
import re
p = re.compoile('Crow|Servo')
m = p.match('CrowHello')
print(m) # <re.Match object; span=(0, 4), match='Crow'>
```

## 메타문자 ^
**^** 는 문자열의 맨 처음과 일치함을 의미합니다. re.MULTILINE 옵션을 사용할 경우 여러줄의 문자열중 각각의 첫줄과 일치 하는 내용을 가져오게 됩니다.

```python
import re
print(re.search('^Help', 'Help me now')) # <re.Match object; span=(0, 4), match='Help'>
print(re.search('^Help', 'you Help')) # None
```
^Help 정규식은 Help 문자열이 청므에 온 경우 매치하지만 처음 위치가 아닌 경우 매치되지 않습니다.

## 메타문자 $
**$** 메타 문자는 **^**와 반대 경우이다. $는 문자열의 끝과 매치를 반환합니다.
```python
import re
print(re.search('Help$', 'Help me now')) #None
print(re.search('Help$', 'your Help')) #<re.Match object; span=(5, 9), match='Help'>
```

help$ 정규식은 검색할 문자열이 short으로 끝난 경우 매치되지만 그외 경우에는 매치 되지 않습니다.

## 메타문자 \A
^ 메타 문자와 동일하지만 re.MULTILINE 옵션을 사용할 경우 다르게 해석되빈다.
- re.MULTILINE 옵션을 사용할 경우
  - ^  : 각줄의 문자열의 처음만 매치.
  - \A : 전체 문자열의 처음하고만 매치.

## 메타문자 \Z
**|Z**는 문자열의 끝과 매치됨을 의미합니다.
- re.MULTILINE 옵션을 사용할 경우
  - $ : 각줄의 끝과 매치.
  - \Z :\A 와 동일하게 전체 문자열에서 매치 됩니다.

## 메타문자 \b
**\b**는 단어 구분자(Word Boundary)입니다. 단어를 파싱 하는 기준은 whitespace에 의해 구분됩니다.
```python
import re
p = re.compile(r'\bclass\b')
print(p.search('no class at all')) # <re.Match object; span=(3, 8), match='class'>
```

**\bclass\b** 정규식은 앞뒤가 whiteSpace로 구분된 class라는 단어와 매치됩니다.
```python
print(p.search('the declassified algorithm')) #None 을반환합니다.
```

**주의할점**
\b는 파이썬 맅너럴 규칙에 의해 백스페이스를 의미할 수 있으므로 Raw String의 기호 r을 반드시 붙여 주어야 합니다.

## 메타문자 \B
**\B** 메타문자는 \b 와 반대의 경우입니다.  
whitespace로 구분도니 단어가 아닌 경우에만 매치됩니다.
```pyhton
import re

p = re.compile(r'\Bclass\B')

print(p.search('no class at all')) # None
print(p.search('the declassified algorithm')) # <re.Match object; span=(6, 11), match='class'>
print(p.search('one subclass is')) # None
```

class 단어의 앞뒤에 공백이 있는경우에 매치가 되지 않습니다.




 