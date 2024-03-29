# 메소드

## 멤버 메소드

* C언어의 함수와 비슷합니다.
* 데이터 처리 기능을 구현합니다.
* 리턴값이 없는 메소드는 void 형을 지정합니다.
* 메소드가 받는 인수의 데이터 타입은 메소드를 호출하는 쪽과 일치해야 합니다.
* Method Overloading(중복 정의), Overriding(재정의)기술로 확장 됩니다.
* 메소드가 리턴하는 값과 리턴되는 값의 데이터 타입은 일치해야 합니다.

### 메소드를 사용하지 않은 경우

> PayCalc2.java

```
public class Pay2 {
    //멤버 변수, 인스턴스 변수, 필드
    String name;
    int    bonbong;
    int    tax;
    int    silsu;
}
```

```
public class PayCalc2 {
    public static void main(String[] args) {
      //┌ Class
      //↓
        Pay2 p1 = new Pay2();
        Pay2 p2 = new Pay2();
      //       ↑
      //       └ 객체, 객체 변수
    
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

### 메소드를 사용한 경우

> Pay.java

```
package classtest;

/**

- 데이터 클래스
  */
  class Pay {
  //멤버 변수, 인스턴스 변수, 필드
  private String name; //성명, 문자열 저장
  private int bonbong; //본봉, 숫자
  private int tax; //세금, 숫자
  private int silsu; //실수령액 본봉 - 세금, 숫자

  /**
    - 기초 데이타를 멤버변수에 저장한다
    - @param name
    - @param bonbong
      */
      public void setData(String name,int bonbong){
      this.name = name;
      this.bonbong = bonbong;
      }

  /**
    - 세금계산
      */
      public void calcTax(){
      tax = (int)(bonbong * 0.045 + 0.5);
      }

  /**

    - 실수령액 계산
      */
      public void calcSilsu(){
      silsu = bonbong - tax;
      }

  public void printPay(){
  System.out.println("--------------------");
  System.out.println("--- 8월 급여 내역 ---");
  System.out.println("--------------------");
  System.out.println("성명: " + name);
  System.out.println("본봉: " + bonbong);
  System.out.println("세금: " + tax);
  System.out.println("실수령액: " + silsu);

  }
  }
```

> PayCalc.java

```
/**

- 데이터 이용 클래스, 시작 클래스
  */
  public class PayCalc {

  /**

    - 시작 메소드
    - @param args
      */
      public static void main(String[] args) {

      Pay p1 = new Pay();
      Pay p2 = new Pay();
      Pay p3 = new Pay();

      p1.setData("왕눈이", 2000000);
      p1.calcTax();
      p1.calcSilsu();
      p1.printPay();

      p2.setData("아로미", 2500000);
      p2.calcTax();
      p2.calcSilsu();
      p2.printPay();

      p3.setData("투투", 3000000);
      p3.calcTax();
      p3.calcSilsu();
      p3.printPay();


    }
    }
```

### 리턴값이 있는 메소드의 사용

> PayCalc.java

```


/**

- 데이터 이용 클래스, 시작 클래스
  */
  public class PayCalc {

  /**

    - 시작 메소드
    - @param args
      */
      public static void main(String[] args) {

      Pay p1 = new Pay();
      Pay p2 = new Pay();
      Pay p3 = new Pay();

      p1.setData("왕눈이", 2000000);
      p1.calcTax();
      p1.calcSilsu();
      p1.printPay();

      p2.setData("아로미", 2500000);
      p2.calcTax();
      p2.calcSilsu();
      p2.printPay();

      p3.setData("투투", 3000000);
      p3.calcTax();
      p3.calcSilsu();
      p3.printPay();


    }
    }
```

> Pay.java

```
package classtest;

/**

- 데이터 클래스
  */
  class Pay {
  //멤버 변수, 인스턴스 변수, 필드
  private String name; //성명, 문자열 저장
  private int bonbong; //본봉, 숫자

  /**

    - 기초 데이타를 멤버변수에 저장한다
    - @param name
    - @param bonbong
      */
      public void setData(String name,int bonbong){
      this.name = name;
      this.bonbong = bonbong;
      }

  /**

    - 세금계산
      */
      public int calcTax(){
      int tax = (int)(bonbong * 0.045 + 0.5);
      return tax;
      }

  /**

    - 실수령액 계산
      */
      public int calcSilsu(){
      int silsu = bonbong - calcTax();
      return silsu;
      }

  public void printPay(){
  System.out.println("--------------------");
  System.out.println("--- 8월 급여 내역 ---");
  System.out.println("--------------------");
  System.out.println("성명: " + name);
  System.out.println("본봉: " + bonbong);
  System.out.println("세금: " + calcTax());
  System.out.println("실수령액: " + calcSilsu());

  }
  }
```

### 클래스의 분리

> Pay.java

```
package classtest;

/**

- 데이터 클래스
  */
  class Pay {
  //멤버 변수, 인스턴스 변수, 필드
  private String name; //성명, 문자열 저장
  private int bonbong; //본봉, 숫자

  /**

    - 기초 데이타를 멤버변수에 저장한다
    - @param name
    - @param bonbong
      */
      public void setData(String name,int bonbong){
      this.name = name;
      this.bonbong = bonbong;
      }

  /**

    - 세금계산
      */
      public int calcTax(){
      int tax = (int)(bonbong * 0.045 + 0.5);
      return tax;
      }

  /**

    - 실수령액 계산
      */
      public int calcSilsu(){
      int silsu = bonbong - calcTax();
      return silsu;
      }

  public void printPay(){
  System.out.println("--------------------");
  System.out.println("--- 8월 급여 내역 ---");
  System.out.println("--------------------");
  System.out.println("성명: " + name);
  System.out.println("본봉: " + bonbong);
  System.out.println("세금: " + calcTax());
  System.out.println("실수령액: " + calcSilsu());

  }
  }
```

> PayCalc.java

```
package classtest;

/**

- 데이터 이용 클래스, 시작 클래스
  */
  public class PayCalc {

  /**

    - 시작 메소드
    - @param args
      */
      public static void main(String[] args) {

      Pay p1 = new Pay();
      Pay p2 = new Pay();
      Pay p3 = new Pay();

      p1.setData("왕눈이", 2000000);
      p1.calcTax();
      p1.calcSilsu();
      p1.printPay();

      p2.setData("아로미", 2500000);
      p2.calcTax();
      p2.calcSilsu();
      p2.printPay();

      p3.setData("투투", 3000000);
      p3.calcTax();
      p3.calcSilsu();
      p3.printPay();


    }
    }
```

### 메소드를 이용해 성적프로그램 만들기. Sungjuk, SungjukUse

> Sungjuk.java

```
class Sungjuk{
String name = "";
int kuk = 0;
int eng = 0;
int tot = 0;
int math = 0;
int avg = 0;
}
```

> SungjukMgr.java

```
public class SungjukMgr {

// ⓐ 값 초기화
public void setValue(){

}

// ⓑ 총점
public void calcTot(){

}

// ⓒ 평균
public void calcAvg(){

}

// ⓓ 출력
public void print(){

}


}
```

> SungjukUse.java

```
public class SungjukUse {

public static void main(String[] args) {
    SungjukMgr mgr = new SungjukMgr();

    Sungjuk sungjuk = new Sungjuk();
    mgr.setValue(sungjuk); // 값 초기화
    mgr.calcTot(sungjuk);  // 총점 계산
    mgr.calcAvg(sungjuk);  // 평균
    mgr.print(sungjuk);

}


}
```

## 변수의 유효 범위(scope)

### 멤버 변수(Instance 변수)

* 변수가 메소드 밖에 선언되는 변수를 말합니다.
* 멤버변수, 인스턴스 변수, 필드라고 합니다.
* 멤버 변수는 모든 메소드가 사용할 수 있습니다.
* 메모리 모델에서 Heap 메모리를 이용합니다.
* 변수의 사용이 끝나도 클래스의 객체 자체가 GC에 의해 회수 되기 전에는 할당받은 메모리를 계속 유지하게 됩니다. 따라서 불필요한 멤버 변수를 최대한 사용하지 않아야 메모리를 낭비없이 효율적으로 이용할 수 있습니다.
* 변수 선언시 값을 주지 않아도 특정 값으로 초기화 됩니다.

### 지역 변수, Local Variable

* 변수가 메소드안에 선언되는 것을 말합니다.
* Stack 메모리를 이용합니다.
* 메소드의 이용이 끝나면 자동으로 메모리가 회수됩니다.
* 초기화를 해야 사용할 수 있습니다.
* 블럭안에 선언: '{ }'안에서만 생명력을 가집니다.
  * Stack 메모리를 이용합니다.

> Variable.java

```
public class Variable {
//멤버 변수, 인스턴스 변수, 필드, Heap
String movie = "트로이";

//지역변수가 없음으로 전역변수가 출력
public void show(){
    System.out.println("show 메소드 영역:" + movie);//트로이
}

//지역변수가 우선으로 출력됩니다. Stack
public void title(){
    String movie = "아마겟돈";
    System.out.println("title 메소드 영역:" + movie);
    System.out.println("title this.movie:" + this.movie);
}

public static void main(String[] args) {

    Variable v = new Variable();
    v.show();
    v.title();
}


}
```

> Block.java

```
public class Block {
String Block="재미있는 영화";

public static void main(String[] args) {
    String b1="트로이";
    System.out.println("Movie:" + b1);//트로이

    {
       String b2="우주 전쟁";
       System.out.println("Movie:" + b2);
       int i=0;

       for(int j=0; j<5; j++){
         //j는 이 블럭 안에서만 유지됩니다.
       }
       //System.out.println("j:" + j);

       for(i=0; i<5; i++){
         //i는 외부에 선언되어 있어야 합니다.
       }
       System.out.println("i:" + i);

    }
    System.out.println("Movie:" + b1);
    //ERROR
    //System.out.println("Movie:" + b2);
}
```
