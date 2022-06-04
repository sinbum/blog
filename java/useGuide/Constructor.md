
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