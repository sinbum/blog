

## 함수 리스트 

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

### DATEDIFF()
1) (고객 별로) 유지기간(Retention)은 얼마나 되는가 (보유기간)?
2) (고객 별로) 거래 안한지 얼마나 되었나 (휴면기간)?
3) 평균적 으로 얼마만에 한번씩 우리물건을 구매하는가? (구매빈도/주기)

* 기타 관련 함수: Today, 시간인 텔리전스(Time lntelligence) 함수들
(DatesAdd, DatesBetween, DatesYTD, DateInPeri0d 등)

```text
Duration = DATEDIFF([FirstOrderDate],[LateOrderDate],DAY)
```
### LOOKUPVALUE()

1) 거래(F)테이를에 가격과 거래금액이 없을때 매출은 어떻게 구할까?
2) (엑셀과는 달리) 여러값을 매칭해서 가져을 수는 없을까?

```text
AAA= LOOKUPVALUE ( D-Products(UstPnceL D-Products(ProductKey), (ProductKeyl )
```

기타 관련 함수: Related


### FORMAT()

적용사례 : 데이터 표현형식을 바꾸고 싶을 때 (엑셀의 FORMAT과 동일)

```text
Sales Amt(억원) = FORMAT ( (Sales Amt(KRW) 1 / 100000000. "#0.0억원")
```

1) 카드에 억 단위로 표현말 수는 없을까?
2) 금액 크기에 따라 억원 단위와 만원 단위를 함께 쓸 수는 없을까?
3) 날짜 형식을 연&까지만 나타나게 할 수는 없을까?

기타 관련 함수: IF, SWITCH 함수
