
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