# 추상클래스_인터페이스

## 추상 클래스(abstract class)

- 추상 메소드
  . 기능이 구현되지 않고 stub, 원형만 선언되어 있는 메소드 입니다.
  . 중괄호 "{, }"가 생략되어 있습니다.
```text
  예)
  public int add(int i, int j);

  public abstract int sub(int i, int j);
```

- 추상 클래스는 추상 메소드가 1개이상 선언되어 있습니다.
- 추상 클래스는 객체를 생성할 수 없습니다.
- 추상클래스가 객체를 생성하려면 추상 메소드를 Overriding(구현) 해야 합니다.
- 추상클래스를 구현한 클래스는 추상클래스를 상속받아 구현함으로 추상클래스 타입에
  포함됩니다.(형변환)

### 추상 클래스의 실습


> Sum.java

```java
abstract class Sum {
//추상메소드 입니다.
public abstract String toString();

    public String sum(int i, int k){
        int sum = i+k;
        return ""+ sum;
    }


}

```

> Sum_s1.java

```java
class Sum_s1 extends Sum{
    //추상 메소드 Overriding(구현)
    public String toString(){
    return "class Sum_s1 extends Sum";
    }
}
```

> Sum_s2.java

```java
class Sum_s2 extends Sum{
    //추상 메소드 Overriding(구현)
    public String toString(){
    return "class Sum_s2 extends Sum";
    }
}
```

> SumMain.java

```java
public class SumMain {

    public static void main(String[] args) {
        Sum_s1 s1 = new Sum_s1();
        System.out.println(s1.sum(10, 20));
        System.out.println(s1.toString());
    
        Sum_s2 s2 = new Sum_s2();
        System.out.println(s2.sum(100, 200));
        System.out.println(s2.toString());
    
    }

}
```

## final

### final 클래스
final클래스는 상속될 수 없습니다.

```java
public final class String extends Object implements Serializable, Comparable, CharSequence

    public class FinalTest extends String{  //ERROR
    
    }
    
```

### final 메소드
자식 클래스가 Overriding 할 수 없습니다.

```java
    public final String prn() {
    
    }
```

## 인터페이스 (Interface)

- 추상 메소드로만 이루어져 있습니다."{}"가 없습니다.
- 아래처럼 중괄호가 없고 메소드의 프로토타입만 선언되어 있으면 추상 메소드입니다.
  예) public abstract void speedDown(int speed);
- 추상메소드를 사용하는 이유는 앞으로 추가되거나 구현되어야하는 기능의 설계 역활을 하며
  실제 기능은 구현하지 않고 메소드 프로토타입만 구현하는 것을 말합니다.
- 추상 메소드는 건축물에서 구조를 이루는 철근과도 같고 설계도와 같은 역활을 합니다.
- 외부에 공개할 메소드를 등록하는 목적으로도 사용됩니다.
- 하나의 콤포넌트가 다양한 형태로 구현되어야 할 경우 인터페이스를 이용하면 콤포넌트의
  사용법이 상당히 단순해 집니다.
- 인터페이스를 구현한 클래스는 인터페이스상에 있는 추상 메소드를 전부 구현해야 합니다.
- 인터페이스상에 있는 메소드를 하나라도 구현하지 않으면 인터페이스를 상속받은 클래스는
  추상클래스가 됩니다.
- A a_obj = new A(); 인터페이스는 객체를 만들 수 없습니다. 따라서 반드시 그 인터페이스를
  구현한 클래스의 객체를 받아 사용하게 되어 있습니다.
    ```java
        A memo;            // A인터페이스형 참조 변수 memo 선언  
      memo = new C1();   // C1은 A라는 인터페이스를 전부 구현한 클래스입니다.
    ```

    

- 인터페이스에 선언된 메소드를 호출하면 그 인터페이스를 구현한 클래스의 메소드가
  자동으로 호출됩니다.
- 인터페이스를 이용하면 인터페이스를 구현하는 클래스들은 메소드의 형태가 같기 때문에
  같은 메소드명을 이용하면서 다양한 구현을 할 수 있습니다.
  이것은 마치 My-SQL용으로 개발된 프로그램을 Oracle 용으로 변경시에 JDBC 드라이버만
  변경하면 프로그램이 작동하는 것과 같은 이치입니다.

### Interface의 구현

> Inter.java


```
public interface Inter {
    public abstract int add(int i, int j);    
    public int sub(int i, int j);
}
```


> InterImpl.java

```
public class InterImpl implements Inter{
    public int add(int i, int j){
        return i+j;
    }
    public int sub(int i, int j){
        return i-j;
    }

    public static void main(String[] args) {
        InterImpl interImpl = new InterImpl();
        System.out.println(interImpl.add(10, 5));
        System.out.println(interImpl.sub(10, 5));
    
        //인터페이스는 기능이 구현되어 있지않음으로
        //객체를 생성할 수 없습니다.
        //----------------------------------------
        //Inter inter = new Inter();
    
        //인터페이스는 구현 클래스를 할당 받을 수 있습니다.
        //인터페이스 = 구현 클래스
        //----------------------------------------
         Inter inter2 = new InterImpl();
         System.out.println(inter2.add(100, 50));
         System.out.println(inter2.sub(100, 50));
    }

```

}

### 인터페이스의 참조
- 인터페이스를 이용하여 메소드만 호출하는 경우는 인터페이스 타입을 그대로 사용합니다.
- 각 클래스의 멤버 변수에 접근하는 경우는 그 클래스 타입으로 형변환을 해주어야 합니다.
- 인터페이스에 변수를 선언한다면 주로 상수를 선언합니다.
- 메소만 선언되는 경우가 대부분입니다.
- 인터페이스 타입 객체 = new 인터페이스 구현 클래스

> IR2.java

```java
interface B {
    void display(String s);
}
```

> D1.java
 
```java
class D1 implements B {
    String str = "";
    public void display(String s) {
    str=s;
    System.out.println("☆☆☆☆☆☆☆☆☆ " + s);
    }
}

```


> D2.java

```java
class D2 implements B {
    String str = "";
    public void display(String s) {
    str=s;
    System.out.println("★★★★★★★★★ " + s);
    }
}
```
> IR2.java

```java
class IR2 {
    public static void main(String args[]) {
    //인터페이스 객체변수는 할당되는 객체에 따라 기능을 변경할 수 있습니다.
    
    B b = new D1();
    b.display("석모도 - 보문사 - 벤뎅이 회무침"); // 클래스 D1의 객체를 생성하여 memo에 할당

    b = new D2();
    b.display("대부도 - 방아머리 - 바지락 칼국수");
    
    //인터페이스 타입은 구현 클래스의 변수에
    //접근할 수 없습니다.
    //-------------------------------------
    //System.out.println(b.str);
    
    //구현 객체의 멤버변수에 접근하려면
    //인터페이스의 구현 클래스 타입으로 형변환을 합니다.
    //-------------------------------------
    D2 d2 = (D2)b;
    System.out.println(d2.str);
  
    }
}

```
> Myinfo.java

```
package day10;

interface Myinfointer {
public String getName();
public String getPhone();

}

```

> Myinfointer.java

```java
class Myinfo implements Myinfointer {
private String name ;
private String phone;
private String address;
private int age;

Myinfo(){}
Myinfo(String name,String phone, String address, int age){
this.name= name;
this.phone = phone;
this.address = address;
this.age = age;
}

public String getName(){
return name;
}

public String getPhone(){
return phone;
}

public String getAddress(){
return address;
}
public int getAge(){
return age;
}
}
```

> Myinfouse.java

```
public class Myinfouse {

  /**
   * @param args
   */
  public static void main(String[] args) {
      Myinfointer info = new Myinfo("개똥이","010-1111-2222","서울시 성북구",33);
      System.out.println("이름:"+info.getName());
      System.out.println("전화:"+info.getPhone());
      //System.out.println("주소:"+info.getAddress());
      //System.out.println("나이:"+info.getAge());
}


}
```
