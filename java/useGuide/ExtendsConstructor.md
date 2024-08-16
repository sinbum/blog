# 상속생성자

## 상속 관계에서의 생성자

부모클래스는 생성자의 쓰임과 관련 없이 디폴트 생성자를 선언할 것을 절대 권장 합니다.

* 자식 클래스 객체 생성시 기본 생성자를 호출하면 부모클래스도 기본생성자가 호출됩니다.
* 부모클래스에 파라미터가 있는 생성자가 존재하면 부모클래스의 기본생성자는 자동으로 생성되지 않음으로 명시적으로 생성자를 선언해야 합니다.
* 자식 클래스 객체 생성시 부모클래스의 생성자가 먼저 호출되고 자식 클래스의 생성자가 호출됨

```
  public Parent(){ }
```

### 부모 클래스의 기본 생성자 호출

* 부모 클래스의 생성자는 생략 가능하나 권장사항이 아닙니다.
* 기본 생성자가 명시되지 않은 경우 자동으로 기본 생성자가 생성되어 객체가 만들어 집니다.

**클래스 별로 생성해야하지만 코드가 길어져 함축 하였습니다.**

> MovieTest.java

```java
//TV클래스
class TV{
}

//TV에서 상속받은 Movie클래스
class Movie extends TV{
   String part="한국 영화";
}

//Movie에서 상속받은 Action클래스
class Action extends Movie{
   String name="";
}

//MovieClass
public class MovieTest {
   //기본 생성자는 자동으로 생성되어 사용됩니다.
   
   public static void main(String[] args) {
   
   //Action클래스 생성
   Action act = new Action();
   
   act.name="우리들의 블루스"; //이병헌   
   
   System.out.println(act.name);
   
   }
}
```

### 부모클래스 선 생성 여부

상속관계에서는 부모클래스의 생성자가 먼저 실행됩니다.

> MovieTest2.java

```java
//TV2 클래스
class TV2{
   public TV2(){
   System.out.println("TV2");
   }
}

//TV2를 상속받은 Movie2 클래스
class Movie2 extends TV2{
   
   String part="한국 영화";
      
   ublic Movie2(){
      System.out.println("Movie2");
      }
}

//Moive2를 상속받은 Action2 클래스
class Action2 extends Movie2{

String name="";
   
   public Action2(){
   System.out.println("Action2");
   }
}

//MoiveTest2 클래스
public class MovieTest2 {
   //기본 생성자는 자동으로 생성되어 사용됩니다.
   public static void main(String[] args) {

   Action2 act = new Action2();

   act.name="우리들의 블루스";
   System.out.println(act.name);
   }

}
```

### 부모 클래스의 생성자가 반드시 필요한 경우

부모 클래스의 생성자가 반드시 필요한 경우 는 에러요소가 잠재적으로 존재할 때 부모클래스를 사용합니다.\
예제 설명은 다음과 같습니다.

> Movie3.java

```java
class Movie3{
String part="";

   public Movie3(){ }  //기본 생성자
   
   public Movie3(String part){
       this.part = part;
       System.out.println("Movie3");
   }
   
}
```

> Comedy3.java

```java
class Comedy3 extends Movie3{
String time="";
String name="";

   //public Comedy3() { } //기본 생성자
   
   public Comedy3(String time, String name){
       this.time = time;
       this.name = name;
       System.out.println("Comedy");
   }

}
```

> MovieTest3.java

```
public class MovieTest3 {
   public static void main(String[] args) {
   //파라미터가 있는 생성자만 호출합니다.
   Comedy3 com = new Comedy3("21:00", "닥터스트레인지2");
   
   //기본 생성자는 기존에 생성자가 없는 경우만
   //자동으로 만들어 집니다.
   //Comedy3 com2 = new Comedy3();
   
   System.out.println(com.time);
   System.out.println(com.name);
   }


}
```

## 메소드 내부 객체 변수, 생성자 호출 메소드

### 메소드 내부 객체 변수

* this : 메소드안에서 객체를 나타내는 객체 변수\
  메소드안에서 메소드를 호출한 객체의 주소(Hash Code)를 가지고 있습니다.
* super : 메소드안에서 상위 클래스 객체를 나타내는 객체 변수

### 생성자 호출 메소드

* 생성자안에서 다른형태의 생성자를 호출 할 수 있습니다.
* this() : 현재 클래스의 생성자를 호출합니다.
* super() : 부모 클래스의 생성자를 호출합니다.
* 생성자 : new를 이용하여 메모리 할당이 끝난 후 메모리를 초기화하는 역활을 합니다. 멤버 변수에 초기값을 할당합니다.

## 메소드 내부 객체 변수, 생성자 호출 메소드 실습

### this

* 멤버 변수를 호출한 객체의 주소를 가지고 있습니다.
* 멤버 메소드는 메소드를 호출한 객체의 주소를 알아야 메소드의 결과를 리턴하기 때문에 호출한 객체의 주소를 저장하기위해 this 객체 변수를 사용합니다.

> This.java

```
class This{
String area="";

   public void prn(){
       System.out.println("이 메소드를 호출한 객체의 HashCode: " + this);
       System.out.println(this.area);
   }


}
```

> ThisTest.java

```
public class ThisTest {

   public static void main(String[] args) {
       This obj1 = new This();
       obj1.area = "인천시";
       obj1.prn(); //객체의 Hashcode가 prn()메소드로 호출됩니다.
       System.out.println("obj1.hashCode(): " + obj1.hashCode());
   }


}
```

### super

super는 부모클래스의 객체의 Hashcode를 가지고 있습니다.

> School.java

```java
class School{
   int year=0;
   public School(){
   this.year = 0;
   }
}
```

> MiddleSchool.java

```java
class MiddleSchool extends School{
int year=0;
   public MiddleSchool(){
   this.year = 3;
   }

   public void prn(){
       System.out.println("year: " + year);
       System.out.println("this.year: " + this.year);
       System.out.println("super.year: " + super.year); //부모클래스
   }
}
```

> SuperTest.java (상위 부모 객체를 비교.)

```
public class SuperTest {
   public static void main(String[] args) {
       MiddleSchool middleSchool = new MiddleSchool();
       middleSchool.prn();
   }
}
```

### this()생성자의 실습

파라미터가 계속 증가해도 기존의 생성자를 이용 활 수 있습니다.

> ThisData.java

```
class ThisData{
int i;
int j;
int k;

//ⓐ
public ThisData(){
    this.i=0;
    this.j=0;
    this.k=0;
}

//ⓑ
public ThisData(int i){
    this.i=i;
}

//ⓒ
public ThisData(int i, int j){
    this(i);  //ⓑ 호출되어 초기화됩니다.
    this.j=j;
}


}
```

> ThisExam.java

```
public class ThisExam {
   public static void main(String[] args) {
   ThisData od = new ThisData(100, 90);
       System.out.println("od.i: " + od.i);
       System.out.println("od.j: " + od.j);
       System.out.println("od.k: " + od.k);
   }
}
```

### super() 생성자 메소드

* 초기화 하려는 변수가 부모클래스와 자식 클래스간에 나누어져 있는 경우 부모와 자식의 생성자에서 그 변수들을 나누어 초기화 합니다.
* 자식 클래스() 시작 ---> 부모 클래스 생성자() 시작/완료 --> 자식 클래스() 완료
* 자식 클래스는 자신이 가지고 있는 멤버 변수만 초기화하고 나머지는 부모클래스의 생성자를 호출해서 부모클래스의 멤버로 초기화 합니다.
* 부모클래스의 생성자를 호출할 경우는 반드시 자식 클래스의 생성자안에서 가장먼저 선언해야 합니다.\
  이유는 자식 클래스의 모듈이 실행되기전에 부모클래스의 생성자가 먼저 실행이 되어야 하는 우선순위의 규칙 때문에 그렇습니다.

> OverC.java

```java
class OverC {
int i, j;

   //생성자
   public OverC(int i, int j) {
       this.i = i; //10
       this.j = j; //20
   }
   
   void show() {
       System.out.println("상위클래스의 메소드 show() 수행");
   }

}
```

> SubOverC.java

```java
class SubOverC extends OverC {
int k;

   //int i: 부모 클래스
   //int j: 부모 클래스
   //int k: 자식 클래스
   public SubOverC(int i, int j, int k ) {
       super(i, j); //상위 클래스의 생성자를 호출
       this.k = k;  //k만 10으로 초기화를 합니다.
   }

   void show() {
       System.out.println("하위 클래스의 메소드 show() 수행");
       System.out.println("===super를 이용한 상위 클래스 메소드 호출===");
       super.show();
   }

}
```

> SuperExam.java

```java
class SuperExam {
   public static void main(String args[]) {
   SubOverC over1 = new SubOverC(10, 20, 30);   
   System.out.println("i, j, k의 값 : " + over1.i + " " + over1.j + " " + over1.k);
   over1.show();
   }
}
```
