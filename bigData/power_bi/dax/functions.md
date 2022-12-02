

# 함수 리스트 


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