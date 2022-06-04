# 클래스

## OOP(Object Oriented Programming, 객체지향 프로그래밍)

### 프로그래밍 환경 발전 순서

- 순차적 프로그래밍 ---> 구조적 프로그래밍 ---> 객체지향 프로그래밍   
- 수직 순차 처리 함수(Function) 클래스(Class: 메소드+멤버변수)  
- GOTO(유지보수 어려움) 함수 존재, main() 로직을 콤포넌트화해 재사용성 향상  
- 재사용성 없음 포인터를 이용해 고속처리 유지보수시 편리함 제공  
- line번호 존재 메모리 안정성이 떨어짐 메모리가 매우 안정적으로 관리됨  
- Reference 사용으로 속도가 느림

```
GW-BASIC, Fortran         C - Game, Network         WEB - JAVA, C#
Embeded, Graphic          Window Application - VC++
```


### 데이터의 구조 발전 순서  

```
Primitive Data Type------------------> 구조체 -----------------------> 클래스  

(char, int, float...)         (기본 데이터 타입의 집합체)         (데이터 타입, 메소드, OOP)

C 언어

사용자 정의 추상 데이터 타입       사용자 정의 추상 데이터 타입

급여: 성명, 본봉, 세금, 실수령액   객체 지향 개념 추가
```

### 객체 지향의 개념

- 재사용 가능하기 쉽게 제작됨   
- 한번 개발된 자바코드를 또 다른 프로젝트에 아주 적은 수정을 하면서 적용시킬수 있는 특징  
- Copy & Paste와는 전혀 다른 개념입니다.  
- 예) A 급여 프로그램 --> Module 재사용 --> B 급여 프로그램
- 콤포넌트가 다른 콤포넌트와 독립적인 부품을 이루어 하나의 거대한 프로그램을 형성합니다.
  ```
  A 프로그램 --> 모듈 --> 출력 --> 처리 종류
  B 프로그램 --> 모듈 --> 출력 --> 처리 종류  
  │  
  ↓
  (공통모듈)
  
  B 프로그램 --> 콤포넌트 <-- A 프로그램
  워드 패드 --> 파일 열기 <-- 메모장
  ```
- 실생활에서의 객체 지향의 예(콤포넌트 지향 설계)
  - 컴퓨터 조립: onBoard(VGA, LAN, SOUND 합체) --> 교체가 어려움
  - 오디오 콤포넌트: Component- Speaker, Radio, CD, DVD, 카세트 분리
  - 윈도우 파일 열기 창
  - 자동차 조립: 타이어 교체
### 객체 지향 프로그램의 개발 순서
- 객체 모델링(설계)
  - 작성하려는 클래스의 속성과 메소드를 미리 문서상으로 나열 정리한다.
  - 팀원간에 로직에 대한 이해를 빨리 할 수 있습니다.
  - 메소드 Stub(원형, 구조)을 생성합니다.
  - 클래스라는 형태로(멤버 변수의 선언, 메서드의 선언) 선언한다.
  - Rational Rose 2000, 2003, OMONDO Eclipse plugin
- 클래스 정의
  - 멤버 변수 정의, 메소드 기능을 정의
- 객체 생성과 사용
  - 정의된 클래스를 이용해서, 메모리상에 객체를 만들고, 객체를 이용한 프로그래밍을 한다.
  - 클래스 객체의 생성 - new를 통한 메모리 할당, 생성자를 호출

## 클래스 선언, 객체 생성, 멤버 변수

### 클래스의 선언

- 클래스명은 첫자는 대문자로 시작하고 파일명은 클래스명과 대소문자도 일치 해야 합니다.
  - public class DosInput3 { ---> DosInput3.java 로 저장
- 하나의 클래스는 하나의 파일로 생성됩니다. Test.java --> Test.class
- java 파일 하나 안에는 여러개의 클래스를 넣어둘수 있는데 이런경우 컴파일을하면 자바 소스 파일은 하나이나 컴파일의 결과로 만들어지는 클래스는 2개이상이 됩니다.
- 하나의 파일안에 클래스가 2개이상 있게되면 반드시 public 키워드로 진입(메인, 시작)클래스를 명시해야합니다. 이 클래스안에는 main()메소드가 있습니다.
- 클래스가 2개이상 있는 경우의 파일명은 public이 명시된 클래스명으로 저장합니다.
- 하나의 파일안에 public 클래스는 하나만 있을 수 있습니다.

> PayCalc.java, 유지보수가 어려운 경우의 예
```
// 데이터 클래스
  
  class Pay {
  //멤버 변수, 인스턴스 변수, 필드
  String name; //성명, 문자열 저장
  int bonbong; //본봉, 숫자
  int tax; //세금, 숫자
  int silsu; //실수령액 본봉 - 세금, 숫자
  }

/**

- 데이터 이용 클래스, 시작 클래스
  */
  public class PayCalc {

  /**

    - 시작 메소드
    - @param args
      */
      public static void main(String[] args) {
      //┌ Class ┌ 메모리 할당(heap memory)
      //│ │
      //│ │
      //↓ ↓
      Pay p1 = new Pay();
      Pay p2 = new Pay();
      Pay p3 = new Pay();
      // ↑
      // └ 객체, 객체 변수

      p1.bonbong = 2000000; //200만원
      [p1.name](http://p1.name/) = "왕눈이";
      p1.tax = (int)(p1.bonbong * 0.045 + 0.5);
      p1.silsu = p1.bonbong - p1.tax;

      p2.bonbong = 2500000; //250만원
      [p2.name](http://p2.name/) = "아로미";
      p2.tax = (int)(p2.bonbong * 0.045 + 0.5);
      p2.silsu = p2.bonbong - p2.tax;

      p3.bonbong = 1500000; //150만원
      [p3.name](http://p3.name/) = "투투";
      p3.tax = (int)(p3.bonbong * 0.005 + 0.5);
      p3.silsu = p3.bonbong - p3.tax;

      System.out.println("--------------------");
      System.out.println("---12월 급여 내역---");
      System.out.println("--------------------");
      System.out.println("성명: " + [p1.name](http://p1.name/));
      System.out.println("본봉: " + p1.bonbong);
      System.out.println("세금: " + p1.tax);
      System.out.println("실수령액: " + p1.silsu);

      System.out.println("--------------------");
      System.out.println("---12월 급여 내역---");
      System.out.println("--------------------");
      System.out.println("성명: " + [p2.name](http://p2.name/));
      System.out.println("본봉: " + p2.bonbong);
      System.out.println("세금: " + p2.tax);
      System.out.println("실수령액: " + p2.silsu);

      System.out.println("--------------------");
      System.out.println("---12월 급여 내역---");
      System.out.println("--------------------");
      System.out.println("성명: " + [p3.name](http://p3.name/));
      System.out.println("본봉: " + p3.bonbong);
      System.out.println("세금: " + p3.tax);
      System.out.println("실수령액: " + p3.silsu);
      }
      }

```

### 데이터 클래스의 분리

> Pay2.java
```

//부속 클래스(콤포넌트 CLASS)는 main 메소드가 없습니다.
public class Pay2 {
//멤버 변수, 인스턴스 변수, 필드
String name;
int    bonbong;
int    tax;
int    silsu;
}

```

> PayCalc2.java

```
public class PayCalc2 {

public static void main(String[] args) {
  //┌ Class
  //↓
    Pay2 p1 = new Pay2();
    Pay2 p2 = new Pay2();
  //    ↑
  //    └ 객체, 객체 변수

    p1.bonbong = 2000000;
    p1.name = "왕눈이";
    p1.tax = (int)(p1.bonbong * 0.05 + 0.5);
    p1.silsu = p1.bonbong - p1.tax;

    p2.bonbong = 2500000;
    p2.name = "아로미";
    p2.tax = (int)(p2.bonbong * 0.05 + 0.5);
    p2.silsu = p2.bonbong - p2.tax;

    System.out.println("성명: " + p1.name);
    System.out.println("본봉: " + p1.bonbong);
    System.out.println("세금: " + p1.tax);
    System.out.println("실수령액: " + p1.silsu);

    System.out.println("성명: " + p2.name);
    System.out.println("본봉: " + p2.bonbong);
    System.out.println("세금: " + p2.tax);
    System.out.println("실수령액: " + p2.silsu);
}


}
```
