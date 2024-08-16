# Greedy 와 Non-Greedy

정규식에서 Greedy는 어떤 느낌으로 이해해야하는지 코드를 살펴보겠습니다.

## Greddy

```python
s = '<html><head><title>Title</title>'

len(s) # 길이 : 32

print(re.match('<.*>', s).span()) # (0, 32)
print(re.match('<.*>', s).group()) # <html><head><title>Title</title>
```

태그가 들어간 '<.\*>' 패턴은 변수로 선언된 s 내에서 두가지 구믄을 가지고 있습니다.

* case1:Title
* case2:

## Non-Greddy

case2의 만 가져오고 싶을경우 non-greedy 를 표현하는 '?'를 사용하면 \*에서 전체로 가져오는것을 방지 할 수 있습니다.

```python
print(re.match('<.*?>', s).group()) # <html>
```

non-greedy 문자인 ? 는 \*? , +? , ??, {m,n}? 와 같이 사용 할 수 있습니다. 가능한 최소한의 반복만을 하여 결과값을 나타냅니다.
