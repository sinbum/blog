# 쓰레드

---

## Thread 개념

- Process: thread의 집합으로 하나의 exe, com, dll 프로그램을 말합니다.
  - 현재 실행되고 있는 프로그램입니다.
  - Process간 자원(memory)을 공유할 수 없습니다. 따라서 Process를 많이 발생 시키면
  자원이 바닥나게 됩니다.
- Thread:
  - 독립된 작은 실행단위로 프로세스를 구성합니다.
  - 반복적으로 동기화하여 실행되는 프로그램 루틴 입니다.
  - 메소드(함수)단위의 처리 모듈, process의 구성 요소입니다.
  - Thread는 많이 발생해도 자원을 공유함으로 Process에 비해 시스템에 적은 부담이 됩니다.
  - 각각의 Thread는 자신의 일을 하고 있으며, 동시에 실행되지 않습니다.
  - 스레드 스케줄러에 의해서 스레드의 여러상태중 실행상태로 변경할 수 있습니다.
  - 스레드의 상태는 준비상태, 실행상태, 대기상태, 정지상태가 있습니다.
  - 스레드는 자원을 공유하는 특징이 있어 멤버필드와 static 필드를 공유합니다.
- Handle: 메모리 포인터, 함수포인터등의 핸들러, thread의 구성요소입니다.
- run()메소드안에 처리로직을 구현하거나 처리로직을 호출하는 로직이 구현되어 있어야 합니다.
- 네크워크, 게임, 데이터베이스, 웹 관련 프로그램에서 많이 사용
- 자바의 스레드는 많은 Reference 참조로 인해 C언어의 스레드보다 속도 및 안정성이 떨어져
  접속자가 많은 네트워크 관련 프로그램에는 사용을 하지 않습니다.
  - Hash Code 관리 부분에 많은 리소스가 소모됩니다.

### 스레드 콜백 메소드와 기본 메소드
- start():
  . 스레드를 스레드 스케쥴러에 등록하고 실행상태로 변경합니다.
  . 이 메소드를 실행했다고해서 바로 스레드가 실행이 되는 것은 아닙니다.
  . JVM은 스레드를 실행할 수 있는 여유가 생겼을 때 자신이 작성한 스레드 스케쥴러에
  의해서 스레드의 run()메소드를 호출합니다.
- run(): JVM이 호출하는 콜백메소드로 여기서 콜백 메소드는 개발자가 호출을 코드상에
  지시하는 것이 아니라 JVM이 호출하는 메소드를 말하는 것으로 이 run()메소드 안에는
  스레드 상태에서 처리하려고 하는 모든 비즈니스 로직이 구현되어 있어야 합니다.
  가장 중요한 메소드입니다.
- sleep(long milli second): 지정된 시간동안 스레드를 쉬게하고, 그 시간이 지나면 다시
  스레드가 작동됩니다.
  . 1000이 1초입니다.
- wait(): 현재를 스레드 무한정 대기 시킵니다. notify(), notifyall()메소드를
  통해서 재 실행 가능합니다.
- suspend():스레드의 실행을 일시적으로 중단 시킵니다.
  다시 실행은 resume()를 통해서만 가능합니다.
- yield(): 스레드의 실행 권한을 무조건 다른 스레드에게 넘겨 줍니다.(양보)
- stop(): 스레드 실행을 완전히 종료 합니다.
- getName(): 쓰레드의 이름을 알려줍니다.
- Thread.currentThread()는 현재 실행중인 쓰레드를 알려줍니다.
## 단일 스레드
일반적으로 하나의 자바 프로그램을 만들어 실행하면 단일 스레드 상태가 됩니다.  
- **main()메소드가 대표적인 단일 스레드입니다.**
## 멀티 스레드 
멀티 스레드는 하나의 메소드가 처리가 끝나는 것이 아니라 여러 메소드가 계속적으로
   실행상태에 있으면서 자원을 공유하고 이용하는 처리 형태를 말합니다.  
- 어느 한 메소드가 실행이 종료 되지 않고 다른 메소드와 함께 계속 실행상태에 있게 되는 것
## 스레드의 생성 방법
- Thread 클래스를 상속받는 방법
- Runnable 인터페이스를 구현하는 방법
  - 자바는 다중 상속이 안됨으로 클래스가 특정 클래스를 상속할 필요가 있는 경우는
  반드시 Runnable인터페이스를 구현해야 합니다.

## 스레드 실습

### 스레드를 이용하지 않은 경우

> GenClass
```

class GenClass{
private int num;
private String name;

public GenClass(String a, int b){ //생성자
    name = a;
    num = b;
}

public void start(){
    for(int i=0; i<num; i++)
        System.out.println(name + " : " + i);
}


}
```
> NonThread.java

```
public class NonThread{
public static void main(String args[]) {
  GenClass t1 = new GenClass("first", 5);
  GenClass t2 = new GenClass("second", 5);
  GenClass t3 = new GenClass("third", 5);  
      t1.start();
      t2.start();
      t3.start();
  }
}
```

### Thread 클래스를 상속받은 경우
- start() ---> JVM ---> run()

  - start(): 개발자: 스레드 스케쥴러에 등록
  - run(): JVM이 스레드스케쥴러를 확인후 그 실행 순서에 따라 run()메소드를 호출함, CallBack Method에 해당됨

- CallBack Method: JVM이 자신의 실행 스케쥴러를 만들고 거기에 등록된 순서에 따라 자동으로 호출하는 메소드
```text
  java.lang.Object
  |
  +--java.lang.Thread
  |
  +--MyThread.java
```


> MyThread.java
```

class MyThread extends Thread{
private int num;
private String name;

public MyThread(String a, int b) {
    name = a;
    num = b;
}

public void run() {  //Callback 메소드
    for(int i=0; i<num; i++)
        System.out.println(name + " : " + i);
}

}
```

> ThreadTest1.java


```
public class ThreadTest1{
public static void main(String args[]) {
  MyThread t1 = new MyThread("first", 1000);
  MyThread t2 = new MyThread("second", 1000);
  MyThread t3 = new MyThread("third", 1000);
      t1.start();
      t2.start();
      t3.start();
  }
}
```


### Runnable 인터페이스를 사용한 경우
- 스레드 내용을 가지고 있는 클래스가 추가적인 기능이 필요해 다른 클래스를 상속받는 경우는
  Thread 클래스를 Extend 할 수 없음으로 반드시 Runnable 인터페이스를 상속받아야 합니다.
- 상속을 받으면서 스레드를 구현하고 싶은 경우 사용됩니다.

> ThreadOne.java


```
class ThreadOne implements Runnable {
private int num;
private String name;

  public ThreadOne(String a, int b) {
      name = a;
      num = b;
  }
  
  public void run(){
      for(int i=0; i<num; i++)
          System.out.println(name + " : " + i);
  }


}
```
> ThreadTest2

```
public class ThreadTest2{
  public static void main(String args[]) {
  //Runnable Interface를 구현한 클래스 객체를
  //Thread 클래스의 생성자로 할당합니다.
  Thread t1 = new Thread(new ThreadOne("first", 1000));
  Thread t2 = new Thread(new ThreadOne("second", 1000));
  Thread t3 = new Thread(new ThreadOne("third", 1000));
  
      t1.start();
      t2.start();
      t3.start();
  }
}
```

### 쓰레드 기본메소드와 특징확인
> Myruns.java

```java
package threadtest;
public class  MyRuns implements Runnable{

  public void run(){
    show();
  }

  public void show(){
    for(int i=0;i<100;i++){
      if(((Thread.currentThread()).getName()).equals("a") ){
        System.out.print("a");
        System.out.print("[A"+i+"]");
      }else if(((Thread.currentThread()).getName()).equals("b") ){
        System.out.print("[B"+i+"]");
        System.out.print("b");
      }else if(((Thread.currentThread()).getName()).equals("c") ){
        System.out.print("[C"+i+"]");
        System.out.print("c");
      }else{
        System.out.print("["+Thread.currentThread().getName()+i+"]");
      }
    }
  }
}
```
> MyRunsMain.java
```java
package threadtest;

public class   MyRunsMain {

  public static void main(String[] args) {
    
    MyRuns mr1=new MyRuns();
    
    Thread t1=new Thread(mr1,"a");
    Thread t2=new Thread(mr1,"b");
    Thread t3=new Thread(mr1,"c");
    
    //Thread t3=new Thread(mr1);
    t1.start();
    t2.start();
    t3.start();
  }
}
```
### Thread와 자원 공유 - 멤버필드, static필드
- 같은자원(같은 객체의 멤버필드)을 여러개의 쓰레드가 공유할 수 있습니다.
- 문제점발생: 좌석예약, 계좌입출금 등등
- 문제점은 동기화 처리(synchronized)로 해결할 수 있습니다.

**멤버필드**

> MemberPrint.java
```java
package threadtest;

public class  MemberPrint implements Runnable{
  
  private  int i=0; //
  
  public void run(){
   show();
  }
  
  public void show(){
  
    for(  ;i<100;i++){
      if(((Thread.currentThread()).getName()).equals("a") ){
       System.out.print("[A"+i+"]");
      }else if(((Thread.currentThread()).getName()).equals("b") ){
        System.out.print("[B"+i+"]");
      }else if(((Thread.currentThread()).getName()).equals("c") ){
        System.out.print("[C"+i+"]");
      }
    }
    
  }
}
```
> MemberPrintMain.java

```java
package threadtest;

public class   MemberPrintMain{
 
  public static void main(String[] args) {
  
    MemberPrint mr1=new MemberPrint();
    Thread t1=new Thread(mr1,"a");
    Thread t2=new Thread(mr1,"b");
    Thread t3=new Thread(mr1,"c");
    
    t1.start();  t2.start();  t3.start();
    
  }
}
```

**static필드**

> StaticPrint.java
> 
```java
package threadtest;

public class  StaticPrint implements Runnable{

private static int i=0; //

  public void run(){
    show();
  }
  public void show(){
    for(  ;i<100;i++){
      if(((Thread.currentThread()).getName()).equals("a") ){
        System.out.print("[A"+i+"]");
      }else if(((Thread.currentThread()).getName()).equals("b") ){
        System.out.print("[B"+i+"]");
      }else if(((Thread.currentThread()).getName()).equals("c") ){
        System.out.print("[C"+i+"]");
      }
    }
  }
}
```
>StaticprintMain.java

```
package threadtest;

public class   StaticPrintMain{
  
  public static void main(String[] args) {
    
    StaticPrint mr1=new StaticPrint();
    StaticPrint mr2=new StaticPrint();
    StaticPrint mr3=new StaticPrint();
    
    Thread t1=new Thread(mr1,"a");
    Thread t2=new Thread(mr2,"b");
    Thread t3=new Thread(mr3,"c");
    
    t1.start();  t2.start();  t3.start();
  }
}
```
### 스레드자원의 동기화
> StaticLockPrint.java

```java
package threadtest;
public class  StaticLockPrint implements Runnable{

private static int i; //static { i=5;}
  
  public void run(){
    show();
  }
  
  public void show(){
    synchronized(StaticLockPrint.class){
      for(  ;i<100;i++){
        if(((Thread.currentThread()).getName()).equals("a") ){
        System.out.print("[A"+i+"]");
        }else if(((Thread.currentThread()).getName()).equals("b") ){
        System.out.print("[B"+i+"]");
        }else if(((Thread.currentThread()).getName()).equals("c") ){
        System.out.print("[C"+i+"]");
        }
      }
    }
  }
}

  /*
  synchronized(StaticLockPrint.class){
    for(  ;i<100;i++){
      if(((Thread.currentThread()).getName()).equals("a") ){
       System.out.print("[A"+i+"]");
      }else if(((Thread.currentThread()).getName()).equals("b") ){
       System.out.print("[B"+i+"]");
      }else if(((Thread.currentThread()).getName()).equals("c") ){
       System.out.print("[C"+i+"]");
      }
    }
  }
  */
```

> StaticLockPrintMain.java

```java
package threadtest;

public class   StaticLockPrintMain{
  public static void main(String[] args) {
  
  StaticLockPrint mr1=new StaticLockPrint();
  StaticLockPrint mr2=new StaticLockPrint();
  StaticLockPrint mr3=new StaticLockPrint();
  
  Thread t1=new Thread(mr1,"a");
  Thread t2=new Thread(mr2,"b");
  Thread t3=new Thread(mr3,"c");
  
  t1.start();  t2.start();  t3.start();
 
  }
}
```
### 스레드와 sleep 메서드

> SleepThread.java

```java
package threadtest;
public class  SleepThread extends Thread{
  public SleepThread(String name){
    setName(name);
  }
  
  public void run(){
    show();
  }
  
  public void show(){
    for(int i=0 ;i<50;i++){
      print();
      
      try{
      Thread.sleep(50);//50/1000 초
      }
      catch(InterruptedException ite){
      
      }
    }
  }
  
  public void print(){
    System.out.print(getName());//Thread에서
  }
}
```

> SleepThreadMain.java

```
package threadtest;
public class  SleepThreadMain{
  public static void main(String[] args) {
    SleepThread t1=new SleepThread("a");
    SleepThread t2=new SleepThread("b");
    SleepThread t3=new SleepThread("c");
  
    t2.setPriority(7);//1~10 클수록 우서순의
    t1.start();//t2가 t1보다 우선이지만
    
    try{
        t1.join();//t1을 끝낸후 t2, t3를 실행한다.
    }catch(InterruptedException ite){
    
    }
    
    t2.start();
    t3.start();
  }
}
```

## 우선순위

- java.lang.MIN_PRIORITY, java.lang.NORM_PRIORITY, java.lang.MAX_PRIORITY
- setPriority(int p): 현재 스레드의 우선순위를 인자 p로 설정하기 위한 메소드
- getPriority(): 현재 스레드의 우선순위를 반환하는 메소드

### sleep()를 적용한 경우
- 특정 스레드에 CPU의 자원이 집중하는 것을 막을 수 있습니다.
- 불규칙적인 동기화는 지원합니다.

> RunThread2.java

```
class RunThread2 extends Thread {
public RunThread2(String name) {
super(name);
}

public void run() {
    for ( int i = 1; i <= 30000000 ; i++ ) {
        if ( i % 50 == 0 ){
            System.out.println("Thread [" + getName() + "] : " + i);
            try{
               //sleep(1); //0.001초
               System.out.print("");
            }catch(Exception e){ }
        }
    }
}


}
```

> SchedulingTest2.java

```
public class SchedulingTest2 {
  public static void main(String args[]) {
  Thread[] t = new RunThread2[5];
  
      t[0] = new RunThread2("☆");
      t[1] = new RunThread2("★");
      t[2] = new RunThread2("◆");
      t[3] = new RunThread2("◇");
      t[4] = new RunThread2("○");
  
      t[0].start();
      t[1].start();
      t[2].start();
      t[3].start();
      t[4].start();
  }
}
```

### 우선순위를 적용한 예
- Thread.MAX_PRIORITY 10
- Thread.NORM_PRIORITY 5
- Thread.MIN_PRIORITY 1
- sleep()의 이용, 우선순위가 적용은 되나 다른 스레드에게 제어권이 자주 넘어감

> RunThread4.java

```
class RunThread4 extends Thread {
  public RunThread4(String name) {
    super(name);
  }

public void run() {
    for ( int i = 1; i <= 10000 ; i++ ) {
        if ( i % 50 == 0 )
            System.out.println("Thread [" + getName() + "] : " + i);

        try{
            sleep(1); //0.001초
        }catch(InterruptedException e){ }

    }
}


}
```

> SchedulingTest4.java
 
```java
public class SchedulingTest4 {

public static void main(String args[]) {
    Thread[] t = new RunThread4[3];

    t[0] = new RunThread4("☆");
    t[1] = new RunThread4("◑");
    t[2] = new RunThread4("○");

    t[0].start();
    t[0].setPriority(1);

    t[1].start();
    t[1].setPriority(5);

    t[2].start();
    t[2].setPriority(10);
    /*
    System.out.println("t[0]" + t[0].getPriority());
    System.out.println("t[1]" + t[1].getPriority());
    System.out.println("t[2]" + t[2].getPriority());
    */
}


}
```
