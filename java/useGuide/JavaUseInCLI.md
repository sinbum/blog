
# 명령 프롬프트(콘솔)상에서의 입력처리

## 도스상에서의 문자열 데이터 입력 처리
OS -----------------> JVM ----------------------> main()
입력된 데이터 main(String[] args)

> DosInput.java

```

public class DosInput {

public static void main(String[] args) {
    String s1 = args[0]; //1번째 문자열 입력
    String s2 = args[1]; //2번째 문자열 입력

    System.out.println("args.length:" + args.length);
    System.out.println("s1:" + s1);
    System.out.println("s2:" + s2);
}


}

```

- 실행
  ```
  C:
  CD\
  CD C:\java_sunday\eclipse\workspace\february\classes
  java DosInput 봄 여름.
  ```

## 숫자를 입력받는 경우

> DosInput2.java


```
public class DosInput2 {

public static void main(String[] args) {
    int i1 = Integer.parseInt(args[0]); //1번째 수
    int i2 = Integer.parseInt(args[1]); //2번째 수

    System.out.println("args.length:" + args.length);
    System.out.println("i1:" + i1);
    System.out.println("i2:" + i2);
    System.out.println("i1+i2:" + (i1+i2));
}


}
```

실행:
C:
CD\
CD C:\java_sunday\eclipse\workspace\february\classes
java DosInput2 10 200

### 문자와 숫자의 입력

> DosInput3.java


```
import java.text.DecimalFormat;

public class DosInput3 {

  public static void main(String[] args) {
      DecimalFormat comma = new DecimalFormat("###,##0");
      String cs1;
      String cs2;
  
      String s1 = args[0];        //성명
  
      int i1 = Integer.parseInt(args[1]); //급여
      cs1 = comma.format(i1);
  
      int i2 = Integer.parseInt(args[2]); //세금
      cs2 = comma.format(i2);
  
      System.out.println("args.length:" + args.length);
      System.out.println("성명(name):" + s1);
      System.out.println("급여(pay):" + cs1);
      System.out.println("세금(tax):" + cs2);
      System.out.println("실수령액(income):" + comma.format(i1-i2));
  
  }
}

```
- 실행
  ```
  C:
  CD\
  CD C:\java_sunday\eclipse\workspace\february\classes
  java DosInput3 왕눈이 2000000 120000
  ```