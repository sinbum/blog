# 상수

위키백과에서 정의하는 상수의 개념은 다음과 같습니다. 상수(常數, constant)란 수식에서 변하지 않는 값을 뜻한다.\
이것은 변하는 값 변수와 반대이다. [참고링크](https://ko.wikipedia.org/wiki/%EC%83%81%EC%88%98)

```java
  public static final int 변수명 = 값;
```

* 고정된 같은 값이 반복해서 쓰이는 경우 상수를 이용하면 유지보수 시간을 절약할 수 있습니다.
* public: 누구나 사용할 수 있음
* static: 객체를 만들지 않고도 사용 할 수 있음
* final: 변수의 값을 변경할 수 없음
* int: 정수를 저장함
* 상수의 예: . 1년 365, 1주일 7일등 로직상에서 변하지 않는 고정된 값 또한 상수의 대상이 됩니다. . 상수 사용이 많은 클래스: Calendar Class 등

> Constant.java

```
public class Constant {
public static final int COUNT=1;

public void prn(){
    //COUNT = 5;
    for (int i=0; i<COUNT; i++){
        System.out.print("JAVA ");
    }

    for (int i=0; i<COUNT; i++){
        System.out.print("JSP ");
    }

    for (int i=0; i<COUNT; i++){
        System.out.print("EJB ");
    }

    for (int i=0; i<COUNT; i++){
        System.out.print("CBD Oracle OJT ");
    }
}

public static void main(String[] args) {
    Constant constant = new Constant();
    constant.prn();

    for (int i=0; i<Constant.COUNT; i++){
        System.out.print("Struts ");
    }

}


}
```
