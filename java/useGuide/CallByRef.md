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



