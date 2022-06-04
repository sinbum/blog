# 다중 구현(다중 상속) 실습

- 자바는 다중 상속을 할 수 없습니다. 한번에 하나의 클래스만 상속할 수 있습니다.
- 상속을 연속해서 받는 경우 다중 상속과 비슷한 기능은 구현할 수 있습니다.
- 인터페이스는 다중상속을 지원합니다. 하지만 이 다중상속은 구현이 이루어진 기능을
  상속하는것이 아니라 추상 메소드를 상속받는 것에 불과함으로 최하의 클래스는 상속받은
  모든 클래스를 직접 구현해야 합니다. 따라서 상속의 개념 보다는 다중 구현의 개념에
  가깝습니다.
  하지만 C++은 실제로 기능이 구현된 클래스를 다중상속 받을 수 있습니다. 이로인해 부모
  클래스가 중복되거나 메소드의 소속이 불분명해져 추가적인 코드가 필요하며 유지보수시
  소스 분석이 매우 어렵습니다.


> Green.java 

```java
interface Green {
  //추상 메소드
  public String greenColor();
}
```

> GreenImpl.java 

```java
  class GreenImpl implements Green{
    public String greenColor(){
    return "초록색입니다.★";
    }
  }
```

> Red.java
```java
interface Red {
  //추상 메소드
  public String redColor();
}
```
> RedImpl.java

```java
class RedImpl implements Red{
  public String redColor(){
  return "빨간색입니다.★";
  }
}
```
> ColorImpl.java

```java
class ColorImpl implements Green, Red{
  
  public String greenColor(){
  return "초록색입니다.";
  }
  
  public String redColor(){
      return "빨간색입니다.";
  }  
}
```

> ColorMain.java

```java
public class ColorMain{

  public static void main(String[] args) {
    Green g = new GreenImpl();
    System.out.println(g.greenColor());
        Red r = new RedImpl();
        System.out.println(r.redColor());
        ColorImpl c = new ColorImpl();
        System.out.println(c.greenColor());
        System.out.println(c.redColor());
  }
}
```

