# 접근제한자 와 가비지 컬렉션

## 접근 한정자(Access Modifier, 제한자, 수정자)

* 클래스간에 멤버 변수나 멤버 메소드에 접근하는 것을 제한할 수 있습니다.
* 클래스간에 간섭을 줄이기 위해 적용합니다.
* 객체지향에서 캡슐화를 구현하는 핵심 기술입니다.
* 클래스간에 간섭을 막을 수 있음으로 콤포넌트의 독립성을 강화할 수 있습니다.

***

접근 제한자 같은 클래스 같은 패키지 상속관계의 다른 패키지 관련없는 다른 패키지

***

* private ○ X X X (중요)
* friendly ○ ○ X X
* protected ○ ○ ○ X
* public ○ ○ ○ ○ (중요)

### 특성보장

private, 보안성이 향상됨, 콤포넌트의 독립성이 보장됩니다. 독립성이 요구되는 WEB관련 프로그램에서는 private 제한자가 아주 많이 사용됩니다.

* 콤포넌트간 간섭을 최소화하여 독립성을 유지할 수 있습니다.
* private변수는 해당클래스안에서만 접근할 수 있습니다. 따라서 이 변수에 접근하려면 public 형태의 메소드를 이용해야 합니다.
* 데이터 은닉 및 캡슐화에 사용됩니다.

### private 멤버 변수

private 멤버 변수(전역변수, 인스턴스 변수)에 값을 할당하고 가져오기(★)

* 입력되는 값을 검증하여 입력합니다.
* 외부에서 변수의 값을 마음대로 조작할 수 없음으로 안정적인 프로그램을 구현할 수 있습니다.

> Data.java

```
//데이터 클래스
class Data{
//인스턴스 변수, 멤버 변수
private String name=null;
private String season=null;
private int year = 0;

//set으로 시작하는 메소드는 setter라고 부릅니다.
//set은 소문자로, 연결되는 변수명의 첫자는 대문자를 사용합니다.
//private변수에 값을 대입하는 목적을 가지고 있습니다.
//값을 저장함으로 리턴타입은 void를 이용합니다.
public void setName(String name){
    this.name = name;
}

public void setSeason(String season){
    this.season = season;
}

public void setYear(int year){
    if (year >= 20 && year <= 30){
        this.year = year;
    }else{
        System.out.println("입력될 수 있는 나이는 20~30세 사이입니다.");
    }

}

//get으로 시작하는 메소드는 getter라고 부릅니다.
//get은 소문자로, 연결되는 변수명의 첫자는 대문자를 사용합니다.
//private변수에서 값을 가져오는 목적을 가지고 있습니다.
//값을 가져옴으로 값에 따른 다양한 데이터타입을 지정합니다.
public String getName(){
    return name;
}

public String getSeason(){
    return season;
}

public int getYear(){
    return year;
}


}
```

> DataAccess.java

```java
//데이터 이용 클래스
public class DataAccess {


public static void main(String[] args) {
    Data d = new Data();
    //d.name="왕눈이";
    //System.out.println(d.name);
    d.setName("왕눈이");
    d.setSeason("늦가을");
    d.setYear(35);

    System.out.println(d.getName());
    System.out.println(d.getSeason());
    System.out.println(d.getYear());

}

}
```

### private method 응용

```
- private 메소드가 존재하면 반드시 private 메소드를 호출하는 public메소드가
  존재하게되어 있습니다.
- private 메소드는 클래스 외부에서 호출될 수 없습니다.
- 거대한 하나의 메소드를 여러개의 메소드로 분리한후 호출을 하나의 메소드로만
  지정할 경우 사용하며 이때 하나의 메소드만 public으로 지정하고 나머지는
  private으로 지정합니다.(★)
```

> PrivateTest.java

```
class PrivateTest {
public int kuk = 0;
public int eng = 0;
public int sum = 0;

private void sum(){
    sum = kuk+eng;
    if ( sum > 200){
        System.out.println("점수가 200을 초과했습니다.");
        sum = 0;
    }else{
        System.out.println("합계가 정상적으로 처리&#46124;습니다.");
    }
}

//Deligate Method
public void call_sum(){
    sum();
}

}
```

> PrivateTestMain.java

```
public class PrivateTestMain {
public static void main(String[] args) {
PrivateTest pt = new PrivateTest();
pt.kuk = 90;
pt.eng = 95;

    //pt.sum(); //외부에서 호출할 수 없습니다.
    pt.call_sum();
    System.out.println("pt.sum(): " + pt.sum);
}


}
```

## Garbage Collecting

* member 변수와 객체에 할당된 메모리를 회수 합니다.
* 자바 가상 기계가 자동으로 수행 합니다.
* 멤버 메소드등 일반 메소드안에서 생성된 객체는 메소드 종료시 자동으로 메모리 회수됩니다.
* null 값을 가지고 있는 객체변수는 회수의 대상이 됩니다.
* 우선 순위가 낮은 스레드로 수행, 일반적인 경우 모든 스레드가 종료된 후 수행
* gc()를 실행되면 강제로 메모리 회수 작업을 하게되며 finalize()메소드가 호출된다. 그러나 gc()자체는 많은 부하를 동반함으로 JVM이 실행하도록 하는것이 좋습니다.

> Garbage.java

```
class Garbage {

int objNo;

public Garbage(int n) {
    objNo = n;
    System.out.println("Garbage class " + objNo + " 이 만들어 졌습니다.");
}

//객체의 메모리가 회수 될때에 자동으로 호출됩니다.
protected void finalize() throws Throwable {
    System.out.println("Garbage class " + objNo + " 에서 쓰이던 메모리가 수집되었습니다.");
    super.finalize();
}


}
```

> GarbageTest.java

```java
public class GarbageTest {
   public static void main(String[] args) {
   
       Garbage[] ga = new Garbage[10];
   
       //객체 생성
       for (int i=0; i < ga.length; i++) {
           ga[i] = new Garbage(i);
       }
   
       //객체 메모리 해제
       for (int i=0; i < ga.length; i++) {
           ga[i] = null;//메모리 회수의 대상이 됩니다.
       }
   
       //강제로 가베지컬렉션 기능 수행
       System.gc();
   }

}
```
