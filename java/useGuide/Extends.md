# 상속

## 상속(Inheritance)의 개념

- 상속의 경우 속성을 상속하는 경우 보다는 메소드를 상속하기위해 많이 사용되며,
  부모 클래스의 기능을 확장하는데 부모클래스를 수정하지 않고,
  부모에 구현된 로직을 사용하면서 안정적으로 클래스의 기능을 확장 할 수 있는
  기법을 제공합니다.
- 상속을 계속적으로 하게 될 경우 가장 아래의 클래스는 부모로부터 많은 메소드를
  상속 받음으로 매우 많은 기능을 사용할 수 있게 됩니다.
- 무분별한 상속은 모바일 프로그램의 경우 심각한 속도 저하를 가져올 수 있습니다.
  또한 유지보수시에 Application 분석을 어렵게 할 수 있습니다.
- 상속은 한번에 하나의 클래스에서만 가능, C++의 경우는 2개이상의 클래스를
  상속하는것이 가능합니다.
- 형식: class 자식 Class(Sub Class) extends 부모 Class(parent Class, Super Class)

  public class TestChild extends TestParent{ }

- 자식 클래스 객체를 생성시 부모 클래스의 객체가 먼저 생성 됩니다.
- Default Constructor(기본 생성자) 선언을 반드시 명시적으로 해야 잠재적인
  에러를 예방할 수 있습니다.
- Object 클래스는 묵시적으로 상속이 선언되기 때문에 상속을 선언하지 않습니다.
- 자식클래스는 부모의 위치를 알지만 부모는 자식의 위치를 알지 못합니다.

### 멤버 변수의 상속

> MovieTest.java

```java

class Movie{
String prat="영화";
}

class Korea extends Movie{  //part변수 상속
String m1 = "가문의위기";
}

class Foreign extends Movie{
String m1 = "박물관이 살아있다.";
}

public class MovieTest {
public static void main(String[] args) {
Korea k = new Korea();
System.out.println("장르:" + k.prat);
System.out.println("제목:" + k.m1);
Foreign f = new Foreign();
System.out.println("장르:" + f.prat);
System.out.println("제목:" + f.m1);
}

}
```

### 메소드의 상속

> Car.java

```java

class Car{
public void gear(){
System.out.println("수동 기어를 사용합니다.");
}
}

class ChildCar extends Car{
public void auto_gear(){
System.out.println("자동 기어를 사용합니다.");
}
}

class ChildCar2 extends ChildCar{
public void auto_gear2(){
System.out.println("수동/자동 기어를 혼합하여 사용합니다.");
}
}
```

> CarTest.java

```
public class CarTest {

  public static void main(String[] args) {
      ChildCar2 cc2 = new ChildCar2();
      cc2.gear();
      cc2.auto_gear();
      cc2.auto_gear2();
  }


}
```

## 상속관계 UML로의 표현

```
  Car Class
  
  △
  │
  │상속(Inheritance), Generalization, 실선
  │
 
  ChildCar Class
  
  △
  │
  │상속(Inheritance), Generalization, 실선
  │
  
  ChildCar2 Class  <─────────── CarTest Class
  
  Instantiate, Import
  
```

### 객체 설계 툴의 설치 - Rational Rose의 설치


## Method Overriding

- 상속관계의 클래스에서 상위 클래스에 선언된 메소드를 자식 클래스에서 다시 선언하는
  경우를 말합니다. 이런 경우 기본적으로 부모클래스의 메소드는 무시됩니다.
- 같은 메소드가 부모와 자식에게 모두 선언되어 있으나 메소드의 내용은 다릅니다.
- 부모와 자식 Class간에 메소드의 원형이 같아야 합니다.
  . 원형(Stub): 메소드명, 인수의 갯수, 인수의 데이터 타입, return 타입
- 부모클래스가 메소드를 상속해주나 자식 클래스는 자신이 구현한 메소드를 우선하여
  이용합니다. 따라서 상속이 무시됩니다.
- 부모클래스의 메소드 기능을 유지하면서 상황에 따라 자식클래스의 변형된 기능을
  사용하고 싶은 경우 사용하며 다형성 구현의 핵심 원리입니다.
- 메신저는 버젼별로 기능이 틀리나 버전이 틀리다고해서 대화를 할 수 없는
  것은 아닌것과 같이 overriding 기술은 부모클래스의 구기능을 없애는것이
  아니라 유지하면서 자식의 새로운 기능으로 교체하는 목적으로 사용됩니다.

### 단순상속

메소드 원형이 다름으로 오버라이딩이 아닙니다. **단순 상속**입니다.

> OverrideExam1.java

```java

class OverA {
void show(String str) {
System.out.println("상위클래스의 메소드 show(String str) 수행 " + str);
}
}

class SubOverA extends OverA {
void show() {
System.out.println("하위클래스의 메소드 show() 수행");
}
}

public class OverrideExam1 {
public static void main(String args[]) {
SubOverA over = new SubOverA();
over.show("IT KOREA");
over.show();
}
}
```

### Method Overriding

상위 클래스와 하위 클래스의 메소드 원형이 같음으로 Method Overriding이라고 합니다.




> OverB.java

```
class OverB {
  void show() {
  System.out.println("부모클래스의 메소드 show()");
  }
  
  void parent() {
      System.out.println("부모클래스에만 있는 메소드 parent()");
  }
}

```

> SubOverB.java

``` java
class SubOverB extends OverB {
  //Overriding
  void show() {
  System.out.println("자식클래스의 메소드 show()");
  }  
}
```

> OverrideExam2.java

```java
public class OverrideExam2 {
  public static void main(String args[]) {
  //부모 클래스 객체 생성
  OverB ob = new OverB();
  ob.show(); //부모클래스의 메소드 show()
  ob.parent();
  
  //자식 클래스 객체 생성
  //상속이 무시되면서 자식 클래스의 메소드가 수행됩니다.
  SubOverB over = new SubOverB();
  over.show();  //자식클래스의 메소드 show()
  over.parent();
  
  }
}
```

### return 타입이 다른 경우

- 메소드의 원형은 같으면서 return type만 다르게 지정할 수 없습니다. 그 이유는 오버라이딩할 것이라고
  소스를 Eclipse가 판단하기 때문에 편집시에 에러를 발생합니다.


## 객체 형변환

- 상속 관계에서는 부모자식간에 형변환이 가능합니다.
- 상속관계에서는 좌측에 부모클래스가 오고 우측에 자식 클래스가 올수 있습니다.
- 실제로 메모리상에 생성되는 객체는 자식 클래스 객체가 생성되고 타입만
  부모클래스가 됩니다.
- 자식 클래스에 등록된 메소드는 호출할 수 없습니다. 따라서 기본적으로
  부모클래스에 있는 메소드만 호출 가능합니다.(타입에 우선합니다.)
- 부모 클래스 타입을 자식클래스로 강제 형변환하면 자식 클래스의 메소드를
  호출 할 수 있습니다.
- 일반적으로 부모클래스의 메소드를 호출하려면 부모클래스 타입으로,
  자식클래스의 메소드를 호출하려면 자식 클래스 타입으로 형변환하여야
  합니다.(★)
  . 예외: 오버라이딩시에는 부모클래스 타입이더라도 자식클래스의 메소드가
  호출됩니다.
- 모든 클래스는 Object 클래스를 기본적으로 상속 받습니다.

> TypeConvertTest.java



```
public class TypeConvertTest {

public static void main(String[] args) {
    TypeConvert tc = new TypeConvert();
    Object obj = tc; //Object 클래스의 메소드만 호출가능
    //System.out.println(obj.getUrl());
    System.out.println(tc.getUrl());

    System.out.println(obj.hashCode());
    System.out.println(tc.hashCode());

    TypeConvert tc2 = (TypeConvert)obj;
    System.out.println("tc2: " + tc2.getUrl());
    System.out.println("tc2: " + tc2.hashCode());
}


}
```

> TypeConvert.java

```
class TypeConvert{
String url = "[http://www.kma.go.kr](http://www.kma.go.kr/)";

public void setUrl(String url){ this.url = url; }
public String getUrl(){ return this.url; }


}
```
