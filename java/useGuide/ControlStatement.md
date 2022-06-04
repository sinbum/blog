# 제어문

## 제어문 - 분기문 (if)

- 조건에 따라 분기를 할 수 있습니다.
- if (조건식){
  참일 경우 실행
  }else{
  거짓일 경우 실행
  }
- 제어문에 따른 실행 문장이 한 문장이면 중괄호를 생략해도 됩니다.(권장아님)
- 참거짓 상황에서 실행할 문장이 2문장 이상이면 중괄호 블럭을 반드시
  추가해야합니다.
- 처리할 문장이 한 문장이더라도 쉬운 식별을 위해 "{,}"을 추가합니다.
- 중괄호 블럭안은 경계를 쉽게 알아볼수 있도록 반드시 들여쓰기를 합니다.

### 실습 예제

> Pay.java

```
public class Pay {

public static void main(String[] args) {
    int year = 5;         //근무(경력) 년수
    int child = 0;        //자녀수
    int pay = 1500000;    //초봉 기본급

    if (year == 0){
        System.out.println("신입사원입니다.");
    }else if (year == 1) {
        pay = pay + 200000;
        System.out.println("경력 1년 입니다.");
    }else if(year == 2) {
        pay = pay + 400000;
    }else if(year == 3) {
        pay = pay + 600000;
    }else if(year == 4) {
        pay = pay + 800000;
    }else{
        pay = pay + 1500000;
    }

    //자녀수당을 계산합니다.
    if ( year >=1){
        if (child > 1){
            pay = pay + (child * 200000);
        }
    }

    System.out.println("기본급: " + pay);
    System.out.println("연  봉: " + (pay * 13));
    System.out.println("월급여: " + ((pay * 13)/12));
}

```

}

## 제어문 - 분기문 (Switch)

- 수식의 결과가 일정한 수치 형태로 나열되어 있는 값과 비교하는 경우 사용합니다.
- case문에 올수 있는 데이터 타입은 byte, char, short, int, long처럼 정수 형태만
  올 수 있습니다.

> SwitchTest.java
>

public class SwitchTest{
public static void main(String args[]){
int k = 1;

```
    switch(k){
        case 1:
            System.out.println("1 입니다.");
            break;
        case 2:
            System.out.println("2 입니다.");
            break;
        case 3:
            System.out.println("3 입니다.");
            break;
        case 4:
            System.out.println("4 입니다.");
            break;
        default:
            System.out.println("1부터 4까지 입력해야 합니다.");
            break;
    }
}


}

```


> SwitchTest2.java


```
public class SwitchTest2{
public static void main(String args[]){
char c = 'C';
String str = "C";
    switch(c){  //정수 계열만 가능
        case 'A':  //65
            System.out.println("입력된 코드는 A 입니다.");
            break;
        case 'B':  //66
            System.out.println("입력된 코드는 B 입니다.");
            break;
        case 'C':
            System.out.println("입력된 코드는 C 입니다.");
            break;
        case 'D':
            System.out.println("입력된 코드는 D 입니다.");
            break;
        default:
            System.out.println("코드는 A부터 D까지 입력해야 합니다.");
            break;
    }
}


}
```



## 논리 연산자를 이용한 제어 조건의 이용

- Short Circuit
  . ||: 좌측의 연산식의 결과가 참이면 우측의 연산을
  검사하지 않고 참 처리합니다.

  int a = 10;
  int b = 5;

  a > b || c < d (a가 b보다 크거나 c가 d보다 클 때 )  

  . &&: 좌측의 연산식의 결과가 거짓이면 우측의 연산을
  검사하지 않고 거짓 처리합니다.

  int a = 5;
  int b = 10;

  a > b && c < d

- 입력받은 값이 3의 배수이거나 5의 배수인 수를 판단하는 IF문의 사용
    ```
    public class IfApp1{
    public static void main(String args[]){
    int k=101;
        //논리 연산자 or의 사용
        if((k % 3 == 0) || (k % 5 == 0)){
            System.out.println("k의 값은:" + k + ": 3의 배수이거나 5의 배수입니다.");
        }
        else{
            System.out.println("K의 값은 3의 배수이거나 5의 배수가 아닙니다.");
        }
    }
    
    }
    ```




- 입력받은 값이 3의 배수이면서 5의 배수인 수를 판단하는 IF문의 사용

    ```
    public class IfApp2{
    public static void main(String args[]){
    int k=90;
        //논리 and 연산자
        if(k % 3 == 0 && k % 5 == 0){
            System.out.println("k의 값은:" + k + ": 3의 배수이면서 5의 배수입니다.");
        }
        else{
            System.out.println("K의 값은 3의 배수이면서 5의 배수가 아닙니다.");
        }
    }
    
    }
    ```


## 제어문 - 반복문 While, do-While, for 문

### While 문
- 참일동안 실행합니다.
- 조건을 만족하지 않으면 한번도 실행을 안 합니다.
- 순환 횟수를 정확히 지정할 수 없을 경우 사용합니다.

> While.java
```
public class While{
public static void main(String args[]){

    int j = -5;

    //j가 0보다 작을 동안 실행합니다.
    while(j <= 0){
        System.out.println("번호 : " + j);//-5, -4
        j++;
        if(j==-3) break;
    }

    System.out.println("--------- END ---------");
    System.out.println("While 종료후 j의 값:" + j);
}

};

```

> Unlimit.java



```
public class Unlimit {
public static void main(String[] args) {
    int i=0;

    while(true){
        i = i + 1;
        //2,3,4의 배수가 발견되면 while문을 벗어납니다.
        if((i % 2 == 0) && (i % 3 == 0) && ( i % 4 == 0)){
            break;
        }
    }
    System.out.println("2,3,4의 배수는 " + i + " 입니다.");

}


}
```

### do-While 문
- 조건에 관계 없이 무조건 1회는 실행합니다.

> DoWhile.java
```
public class DoWhile{
public static void main(String args[]){
    int j=1;

    do{
        System.out.println("번호 : " + j); //1
        j++;  //2
        if(j == 5) break;
    //j가 0보다 작을 동안 실행
    }while(j < 0);

    System.out.println("--------- END ---------");
    System.out.println("do-while문 종료후의 j의 값:" + j);
}
};

```




### for 문
- 반복 횟수가 지정되어 있는 경우
- for문은 내부에 초기화 코드를 가지고 있다.
- 조건식이 참이면 계속 실행한다.

```
    for (int i=1; i<=5;   i++) {
    
    for(초기화;  조건식;  재초기화){
    ⓐ -------> ⓑ <-------- ⓔ   시계 반대 방향으로 회전
    │            ↗
    │          ／
    ⓒ │        ／ ⓓ
    │     ／
    │  ／
    System.out.println("★");
    
    }
    
    // 최초 처리순서
    //   ⓐ --> ⓑ --> ⓒ --> ⓓ --> ⓔ --> ⓑ --> ⓒ
    // 반복 처리순서
    //   ⓑ --> ⓒ --> ⓓ --> ⓔ --> ⓑ --> ⓒ
```


> Array.java

```
public class Array {
    public static void main(String[] args){
    int[] pay = {1800, 2200, 2600, 3000, 3400, 3800};
    
    //        System.out.println(pay[0]); //pay 배열 index 0의 값
    //        System.out.println(pay[1]);
    //        System.out.println(pay[2]);
    //        System.out.println(pay[3]);
    //        System.out.println(pay[4]);
    //        System.out.println(pay[5]);
        int i=0;
    
        //i는 5보다 작거나 같을 경우 실행
        for (i=0; i<=5; ++i){ //0,1,2,3,4,5,6
            System.out.println(i + "년차 연봉: " + pay[i]);
        }
        System.out.println(i);
    }
}
```

> EvenSum.java(1부터 100까지 짝수의 합 구하기 (답 : 2550))

```
public class EvenSum {
public static void main(String[] args) {

    int sum = 0;

    for (int i=1; i<=100; i++) {
        if ((i%2)==0){
            sum += i;
        }
    }

    System.out.println("1부터 100까지 짝수의 합: " + sum);
}


}

```

▷ 홀수의 합을 구해 보세요. (2500 이 정답)

## break, continue

### for문의 break

> Break.java

```
public class Break {
public static void main(String[] args) {
for (int i=0; i<=2; i++) {     //3

        //---------------------------------------
        for (int j=2; j>=0; j--) { //3
            // 출력하고 줄을 변경하지 않습니다.
            System.out.print("i=" + i + " j=" + j);
            System.out.print("     ");
            // 출력하고 줄 변경
            System.out.println("X-MAS");
            if (j == 1){
                System.out.println("j==1 break");
                break;
            }
        }// END 안쪽 for문
        //---------------------------------------

        if ( i == 1){
            System.out.println("i==1 break");
            break;
        }
    }// END 바깥쪽 for문
}


}
```


### continue
- 루틴을 벗어나지않고 특정 조건에서만 로직을 수행하지 않는 경우에 사용합니다.

> Continue.java


```
public class Continue {
public static void main(String[] args) {

    for (int i=0; i<=2; i++) {
                         //  ┌ continue시 이동되는 곳
                         //  ↓
        for (int j=0; j<=2; j++) {
            if (i==j){
                continue;
            }else{
                System.out.println("i==" + i + " j==" + j);
            }
        }
    }
}


}

```

## 구구단 출력 (문자열 + 숫자 = 문자열, 연산의 우선순의 주의)

> GuguDan.java

```
public class GuguDan{
    public static void main(String args[]){
        //1, 4, 7
        for (int i = 1; i <= 9; i += 3) {
        System.out.println("   " + i + "단\t\t   " + (i+1) + "단\t\t   " + (i+2) + "단");
        //                                1                   2                    3
        //                                4                   5                    6
        //                                7                   8                    9
        System.out.println("------------------------------------------");
        //1,2,3,4,5,6,7,8,9
        for (int j = 1; j <= 9; j++) {
        System.out.print(i + " * " + j + " = " + i*j + "\t");
        //               1 * 1 = 1
        //               1 * 2 = 2
        //               1 * 3 = 3
    
        System.out.print((i+1) + " * " + j + " = " + (i+1)*j + "\\t");
        //                2 * 1 = 2
        //                2 * 2 = 4
        //                2 * 3 = 6
    
        System.out.print((i+2) + " * " + j + " = " + (i+2)*j);
        //                3 * 1 = 3
        //                3 * 2 = 6
        //                3 * 3 = 9
    
        //줄 바꾸기 목적으로 사용됩니다.
        System.out.println("");
        }
        System.out.println("");
        }
    }
}

```

> 콘솔 결과 

```

### 1단 2단 3단

1 * 1 = 1	2 * 1 = 2	3 * 1 = 3
1 * 2 = 2	2 * 2 = 4	3 * 2 = 6
1 * 3 = 3	2 * 3 = 6	3 * 3 = 9
1 * 4 = 4	2 * 4 = 8	3 * 4 = 12
1 * 5 = 5	2 * 5 = 10	3 * 5 = 15
1 * 6 = 6	2 * 6 = 12	3 * 6 = 18
1 * 7 = 7	2 * 7 = 14	3 * 7 = 21
1 * 8 = 8	2 * 8 = 16	3 * 8 = 24
1 * 9 = 9	2 * 9 = 18	3 * 9 = 27

### 4단 5단 6단

4 * 1 = 4	5 * 1 = 5	6 * 1 = 6
4 * 2 = 8	5 * 2 = 10	6 * 2 = 12
4 * 3 = 12	5 * 3 = 15	6 * 3 = 18
4 * 4 = 16	5 * 4 = 20	6 * 4 = 24
4 * 5 = 20	5 * 5 = 25	6 * 5 = 30
4 * 6 = 24	5 * 6 = 30	6 * 6 = 36
4 * 7 = 28	5 * 7 = 35	6 * 7 = 42
4 * 8 = 32	5 * 8 = 40	6 * 8 = 48
4 * 9 = 36	5 * 9 = 45	6 * 9 = 54

 7단 8단 9단

7 * 1 = 7	8 * 1 = 8	9 * 1 = 9
7 * 2 = 14	8 * 2 = 16	9 * 2 = 18
7 * 3 = 21	8 * 3 = 24	9 * 3 = 27
7 * 4 = 28	8 * 4 = 32	9 * 4 = 36
7 * 5 = 35	8 * 5 = 40	9 * 5 = 45
7 * 6 = 42	8 * 6 = 48	9 * 6 = 54
7 * 7 = 49	8 * 7 = 56	9 * 7 = 63
7 * 8 = 56	8 * 8 = 64	9 * 8 = 72
7 * 9 = 63	8 * 9 = 72	9 * 9 = 81

```

