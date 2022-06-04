
# 생성자(Constructor)

- return Type이 없습니다.
- 클래스 이름과 같아야 합니다.(대소문자 구별)
- new를 이용하여 객체를 메모리에 할당한 후 할당된 메모리를 특정 값으로
  초기화하는 역활을 합니다.

## 기본 생성자가 생략되어 있는 경우

> SchoolMain2.java

```
class School2{
int kuk = 0;
int eng = 0;
int tot = 0;


public int hap(){
    tot = kuk+eng;

    return tot;
}


}

```

> SchoolMain2.java

```java
public class SchoolMain2 {
    public static void main(String[] args) {
        School2 sc2 = new School2();
        sc2.kuk=90;
        sc2.eng=100;
        System.out.println("hap: " + sc2.hap());
    }
}
```

## 기본생성자를 선언한 경우
- 생성자에 초기화하는 변수가 없어도 반드시 생성자를 선언할 것을 권장합니다.
- 상속 관계에 들어가면 이 기본 생성자가 선언되지 않으면 상황에 따라 에러를
  발생합니다.

> School3.java

```java

class School3{
int kuk = 0;
int eng = 0;
int tot = 0;


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

## 기본생성자를 선언해야 하는 경우
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


## 생성자에 대한 개념 부가 설명(중요)

**자바에서의 생성자**

1. 기본생성자를 이용하여 학생을 만들고보니 학생클래스 내부의 성적과 학생정보에 대한 클래스가 존재합니다.
그런데 이 클래스를 활용할 수 없습니다.  
**Student student=new Student( );**


2. 생성자 중 객체를 전달하는 생성자가 있습니다.
그런데 문제는 이 객체를 생성하고 객체전달을 해야 사용이 가능 합니다.  
**Student student=new Student(sungjuk, studentinfo);**


3. 성적과 학생정보 객체를 생성 그리고 학생 객체 생성자함수에 전달을 해주었지만 문제가 발생헀습니다.   
문제는 다음과 같습니다.  
**Sungjuk sungjuk=new Sungjuk( );**  
**StudentInfo studentinfo=new StudentInfo( );**  
**Student student=new Student(sungjuk, studentinfo);**

   - 성적 정보 부재
   - 학생 정보 부재  

4. 성적정보를 입력하는 생성자 함수를 찾았고  
**Sungjuk sungjuk=new Sungjuk(subject);**


5. 학생정보를 입력하는 생성자 함수를 찾았습니다.  
**StudentInfo studentinfo=new StudentInfo(1,"김하나","010-1111-1111");**  
그러나 성적정보는 subject 라는 클래스로 이루어져 있습니다.

6. subject 라는 객체를 생성하고 점수를 전달합니다.
**Subject subject=new Subject(80,80,80);**  
**Sungjuk sungjuk=new Sungjuk(subject);**  

---

해결된 예시는 다음과 같습니다.  
```java
Subject subject=new Subject(80,80,80);  
Sungjuk sungjuk=new Sungjuk(subject);  

StudentInfo studentinfo=new StudentInfo(1,"김하나","010-1111-1111");  
student[0]=new Student(sungjuk, studentinfo);  

System.out.println(student[0].sungjuk.total);  
System.out.println(student[0].sungjuk.avg);  
```

즉 위 사례를 통한 트러블슈팅은 다음과 같습니다.
1. 각 클래스의 값 조회는 가능하나 활용이 불가능했다.
2. 각 클래스를 따로 생성하여 한 로직에서 모든 정보를 대입하고,
3. 대입한 클래스를 하나의 학생객체에 담아 주었습니다. 즉 객체가 객체를 담은 것입니다.
4. 정리하면 생성자를통해 새로운클래스를 생성하였지만 대입한 인자값 또한 생성자로 생성된 객체로 주입을 한 것입니다.
 