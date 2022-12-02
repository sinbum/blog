

# 함수 리스트 

강의 저자 : 어니언 비아이
강의 제목 : POWER BI DAX 사용법
강의 url : [https://www.youtube.com/@user-bs8qs5fs3k](https://www.youtube.com/watch?v=0Wh7PoDwASI&list=PLXTZTI9YjEQ172Ek4eT7TJGK4WAEZ2YV5)


### COUNTBLANK()

값이 비어 있는 것을 count 하는 함수

예제)
```text
#Product_단종 = COUNTBLANK(D_Products[Status])
```
### DISTINCTCOUNT()

고유한 것들만 카운트 하는 함수

예제)
```text
#Order = DISTINCTCOUNT(F_Sales[SalesOrderNumber])
```

### MIN,MAX()

적용 사례 : 고객별 최초/ 최종거래일, 데이터기간 등

1) 고객별 마지막으로 우리 물건을 산 시점은 언제인가?
2) 데이터가 보여주는 기간은 언제부터 언제까지 인가?

기타 관련 함수 : FirstDate(), LastDate()

```text
Order_FirstDate = MIN (F_Sales [OrderDate])
```