# CallByRef

## Call By Value/Reference

1. Call By Value: 값에 의한 호출
    - 보통 숫자 계열 값을 메소드 호출시 메소드로 전송하는 경우가 해당이 됩니다.
    - 메소드로 한 문자, 상수 문자열, 숫자를 전달하면 전부 값에의한 호출이라고
      하고 Call By Value 라고 합니다.

> Pay1.java

```

package classtest;
class Pay1{
String name="";   //직원 이름
int pay=0;        //급여
int comm=0;       //보너스
int tax=0;        //세금

public Pay1(){ }


public void name(String name){
[this.name](http://this.name/) = name;
}


public void tax(float f){
    tax = (int)(pay * f);
}

public void pay(int pay){
   this.pay= pay;
}

public void comm(int comm){
   this.comm = comm;
}

public int earn(){
    int total = (pay + comm)-tax;
    return total;
}


}

```

> Employee_arg.java
```
public class Employee_arg {

public static void main(String[] args) {
    String name="아로미"; //성명
    int pay=1500000;      //급여
    int comm=200000;      //보너스

    Pay1 p = new Pay1();
    p.pay(pay);
    p.name(name);
    p.tax(0.05f);
    p.comm(comm);

    System.out.println("이름:"+p.name);
    System.out.println("실수령액:"+p.earn());
}


}
```

### Call By Reference: 참조값에 의한 호출(Hash Code)
- 메소드로 참조type을 전송할 수 있습니다.
- 메소드로 클래스의 객체를 전달하면 메모리가 전달되는 것이 아니라
  객체를 가르키고있는 Hash Code가 전달됨으로 Call By Reference 라고 합니다.
- Call By Reference의 경우 참조값(Hash Code)을 전달한 객체는 자신의
  참조값이 전달됨으로 값의 변화가 발생할 수 있고 heap memoey를
  공유하게 됩니다.

### Call By Value/Reference 예제

> Pay.java

```
class Pay{
int ppp;
public void payRefer(Pay p){
p.ppp = p.ppp + 2000;
}
public void payValue(int i){
i = i + 2000;
}
}
```

> PayTest.java

```
public class PayTest {

public static void main(String[] args) {
	Pay p = new Pay();
	p.ppp = 10;

	int i = 10;

	p.payRefer(p);	//call by reference로 전달
	p.payValue(i);	//call by value로 전달

	System.out.println(p.ppp); //객체가 변경되서 2010
	System.out.println(i);//10
}

}
```

> Ref.java, 데이터 클래스

```

public class Ref {
public String area = ""; // 지역
public int oil = 0;      // 평군 기름값
public String sobi = ""; // 전년 동월대비 소비량
}

```

> RefMgr.java, 데이터 조작 클래스


```
public class RefMgr {
/**
* 객체를 받아 출력합니다.
* @param ref 출력할 객체
  */
  public void print(Ref ref){
  System.out.println("지역: " + ref.area);
  System.out.println("평균 기름값: " + ref.oil);
  System.out.println("전년 동월 대비 소비량: " + ref.sobi);
  }

public void calc(Ref ref){
    int add = (int)(ref.oil * 0.2); // 20% 기름값 인상
    int tax = 20;

    ref.oil = ref.oil + add + tax;   // 원 가격 + 인상분 + 세금

}


}

```

> RefUse.java 콤포넌트 이용 클래스
```

public class RefUse {
public static void main(String[] args){
RefMgr m = new RefMgr();

    Ref ref = new Ref();
    ref.area = "서울";
    ref.oil = 2050;
    ref.sobi = "70%";

    // Call By Reference
    // 메소드로 숫자, 문자뿐만 아니라 클래스의 객체도
    // 넘겨 줄 수 있습니다.
    m.print(ref);  // 2050

    // 기름 평균 값 인상 처리 사용
    m.calc(ref);
    System.out.println("1차 변경된 기름값: " + ref.oil);

    m.calc(ref);
    System.out.println("2차 변경된 기름값: " + ref.oil);

}


}
```

###  String객체의 특징

1. 한번생성된 객체는 불변이다.("안녕" ->(X) "안녕하세요")
2. 클래스를 객체화할때 new를 사용하지만
   String은 사용하지 않아도 된다.(String name = "홍길동";)
3. 메모리상에서 같은 문자열은 공유합니다.
   String name = "홍길동";
   String str = "홍길동";
   name hashcode와 str hashcode는 같습니다.
4. 문자열을 변경할때 ("안녕" -> "안녕하세요")
   메모리상에는 "안녕"이라는 객체와 "안녕하세요"라는객체가
   둘다 존재합니다.변경되어지는 객체가 있을때마다 새로운
   객체가 만들어집니다.
5. String 객체의 데이터 전달 유형

> StringTest.java

```

public class StringTest {

public void changeString(String src){
    src = "JSP";
}

public static void main(String[] args) {
    //System.out.println("ABCD".toLowerCase());
    //System.out.println("ABCD".hashCode());

    String step = "JAVA";
    StringTest st = new StringTest();
    System.out.println(step);
    st.changeString(step); //JSP로 변경하기 위해 할당
    System.out.println(step);
}
}

```


## 메소드 오버로딩(Method Overloading)

- 같은 클래스 내에서 같은 이름의 메소드를 여러개 선언하는 것을 말합니다.
- JVM은 같은 이름의 메소드가 있으면 메소드가 받는 인수의 갯수와 데이터
  타입을 비교하여 다르면 각각 다른 메소드로 인식을 합니다.
  단 return 타입은 메소드를 구분하는 조건으로 사용하지 않습니다.
### method overloading 의 대표적인 경우
- System.out.println(1);
- System.out.println(1.5);
- System.out.println("우리는 한국인입니다.");
- System.out.println("IT 기술을 " + " 다양한 분야로 적용해야 합니다.");
  
### method overloading 을 사용하지 않는 경우
- public void printInt(int x){ }
- public void printFloat(float x){ }
- public void printString(String x){ }

### 메소드 오버로딩을 적용한 경우

- public void println(int x){ }
- public void println(float x){ }
- public void println(String x){ }

- PrintStream 클래스의 메소드 오버로딩 예)

    - void print(char c){ }   //print('C')
    - void print(double d){ } //print(10.5)
    - void print(float f){ }  //print(10.5f)
    - void print(int i){ }    //print(10)
    - 메소드가 호출되는 경우 메소드의 인수의 데이터 타입과 갯수가 일치하는 메소드가 호출됩니다.
    - println()메소드 및 생성자는 대표적인 메소드 오버로딩의 예입니다.
    - 개발시에는 좀더 많은 시간이 소요되나 개발된 클래스를 이용시에는 많은 속도
      향상을 가져옵니다.
  
## 메소드 오버로딩 실습

> AvgTest.java


```
public class AvgTest {

public int getAvg(){
    System.out.println("값을 2개이상 입력해 주세요.");
    return 0;
}

public int getAvg(int a, int b){
    return (a + b) / 2;
}

public int getAvg(float a, float b){
    return ((int)a+(int)b)/2;
}

public int getAvg(int a, int b, int c){
    return (a + b + c) / 3;
}

public int getAvg(int a, int b, int c, int d){
    return (a + b + c + d) / 4;
}



//    리턴 타입은 메소드 구분을 할 수 없습니다.
//    public float getAvg(){
//        return 0.0f;
//    }


public static void main(String[] args) {
    AvgTest st = new AvgTest();
    System.out.println(st.getAvg());
    System.out.println(st.getAvg(10,20));
    System.out.println(st.getAvg(10.5f,20.5f));
    System.out.println(st.getAvg(10,20,30));
    System.out.println(st.getAvg(10,20,30,40));

}


}

```

## 생성자(Constructor)

- return Type이 없습니다.
- 클래스 이름과 같아야 합니다.(대소문자 구별)
- new를 이용하여 객체를 메모리에 할당한 후 할당된 메모리를 특정 값으로
  초기화하는 역활을 합니다.
### 기본 생성자가 생략되어 있는 경우

> SchoolMain2.java

```
class School2{
int kuk = 0;
int eng = 0;
int tot = 0;
>

public int hap(){
    tot = kuk+eng;

    return tot;
}


}

```

public class SchoolMain2 {

```
public static void main(String[] args) {
    School2 sc2 = new School2();
    sc2.kuk=90;
    sc2.eng=100;
    System.out.println("hap: " + sc2.hap());
}


}
```

### 기본생성자를 선언한 경우
- 생성자에 초기화하는 변수가 없어도 반드시 생성자를 선언할 것을 권장합니다.
- 상속 관계에 들어가면 이 기본 생성자가 선언되지 않으면 상황에 따라 에러를
  발생합니다.

> School3.java

```

class School3{
int kuk = 0;
int eng = 0;
int tot = 0;
>

public School3(){

}

public int hap(){
    tot = kuk+eng;

    return tot;
}


}

```

> SchoolMain3.java

```
public class SchoolMain3 {

public static void main(String[] args) {
    School3 sc3 = new School3();
    sc3.kuk=90;
    sc3.eng=100;
    System.out.println("hap: " + sc3.hap());
}


}

```

### 기본생성자를 선언해야 하는 경우
- 인수를 받는 생성자가 존재하게되면 반드시 기본 생성자를 선언해야 합니다.
- 기본 생성자는 하는 일이 없어도 반드시 선언을 적극 권장합니다.

> School4.java

```

class School4{
int kuk = 0;
int eng = 0;
int tot = 0;

//기본 생성자
public School4(){ }

//아래처럼 인수를 받는 생성자가 존재하면
//반드시 기본 생성자를 명시적으로 선언해야 합니다.
public School4(int kuk, int eng){
    this.kuk = kuk;
    this.eng = eng;
}

public int hap(){
    tot = kuk+eng;

    return tot;
}


}

```
> SchoolMain4.java

```
public class SchoolMain4 {

public static void main(String[] args) {
    School4 sc4 = new School4();
    sc4.kuk=90;
    sc4.eng=100;
    System.out.println("hap: " + sc4.hap());

    School4 sc = new School4(90, 100);
    System.out.println("hap: " + sc.hap());
}


}
```
