# 예외처리(Exception)

- 예외는 프로그램 개발시에 발생하는 에러와 다릅니다.
- 프로그램 개발시에 발생하는 에러는 전부 수정해야 합니다.
- 안정적으로 컴파일된 후 운영중에 발생하는 에러는 대부분 "예외"인 경우가 많습니다.
  예외는 코드상에서 발생하는 에러하고는 다르며 컴파일시에는 에러가 발생하지 않습니다.
  마치 디스켓을 읽어오는 프로그램이 있다면 디스켓이 없는 상태에서 읽기 기능을 작동하여 발생하는 에러와 같은 것입니다.
- 예외 처리를 하면 예외가 발생되서 프로그램이 끝나는 것이 아니라 나머지 루틴이
  정상적으로 실행이 됩니다.
- 자바는 객체지향 언어임으로 예외 메시지도 객체지향적으로 처리합니다.

> 자바 코드 try,catch문 예제코드

```java
try{

   //에러가 발생할 소지가 있는 코드를 개발자가 선별하여 지정해야 하며 "IO, DBMS, NETWORK"관련 코드가 대부분입니다.

}catch(Exception e){

   //예외처리 및 예외처리 원인 출력
   System.out.println(e.toString());

}finally{

   //무조건 실행되는 코드 블럭, 데이터베이스 연결 종료 등

}
```

> Ex1.java - ERROR 발생

```java
class Ex1 {
public static void main(String args[]) {

  int a = 10;
  int b = 0;
  /*
  if (b == 0){
      System.out.println("0으로 나눌수 없습니다.");
      System.exit(0);
  }
   */

  System.out.println(" a = " + a + " b = " + b );
  System.out.println(" a/b = " + (a/b) );
  System.out.println("나눗셈이 수행되었습니다.");


}
}
```

> Ex2.java - 예외를 처리한 경우

```java
class Ex2 {
public static void main(String args[]) {

  System.out.println("매개변수로 받은 두 개의 값");
  int a = 10;    // 문자열 값을 정수로 변환
  int b = 0;

  System.out.println(" a = " + a + " b = " + b );

  try{
      System.out.println(" a를 b로 나눈 몫 = " + (a/b) );
  }catch(Exception e){
      System.out.println("[경고]예외발생:" + e.toString());
  }finally{
      System.out.println("나눗셈 연산이 종료 되었습니다.");
  }

  System.out.println("나머지 루틴을 정상적으로 실행합니다.");

}
}
```
## 예외 선언

 예외의 선언은 처음에는 좁은 범위를 잡고 다음으로 내려갈수록 넓은 범위의 예외를 아래처럼 명시합니다.
 - 예외의 파악이 불분명한경우 Exception 클래스로 받습니다.

```text
   java.lang.Object
   |
   +--java.lang.Throwable
   |
   +--java.lang.Exception                                 <--- 가장 넓은 범위
   |
   +--java.lang.RuntimeException
   |
   +--java.lang.IllegalArgumentException
   |
   +--java.lang.NumberFormatException   <--- 가장 좁은 범위, 여기부터 catch문에 명시
```

> ExceptionError1.java

```java
class ExceptionError1 {
   public static void main(String args[]) {
   
      try {
      System.out.println("매개변수로 받은 두 개의 값");
      int a = Integer.parseInt(args[0]);    // 문자열 값을 정수로 변환
      int b = Integer.parseInt(args[1]);
      System.out.println(" a = " + a + " b = " + b );
      System.out.println(" a를 b로 나눈 몫 = " + (a/b) );
      System.out.println("나눗셈이 원할히 수행되었습니다.");
      }
      catch(ArithmeticException e) {
      System.out.println("==================================");
      System.out.println("ArithmeticException 처리 루틴 : ");
      System.out.println(e + " 예외 발생");
      }
      catch(ArrayIndexOutOfBoundsException e) {
      System.out.println("==================================");
      System.out.println("ArrayIndexOutOfBoundsException 처리 루틴");
      System.out.println(e + " 예외 발생");
      }
      catch(NumberFormatException e) {
      System.out.println("==================================");
      System.out.println("NumberFormatException 처리 루틴");
      System.out.println(e + " 예외 발생");
      }
      catch(Exception e) {
      System.out.println("==================================");
      System.out.println("알수없는 문제가 발생했습니다.");
      System.out.println(e.toString());
      }
      finally {
      System.out.println("==================================");
      System.out.println("예외 처리를 끝내고 finally 블럭을 수행합니다");
      }
   System.out.println("나머지 모듈 정상 작동!!!");
   }
}
```
