# CollectionFramework
- 배열의 단점을 개선한 클래스로 객체만 저장할 수 있습니다.
- 배열의 단점인 메모리 낭비를 피할수 있는 구조입니다.
- 동적인 크기 변경이 가능합니다.
- 자료를 효율적으로 정리하는것을 자료구조(Data structure)라 합니다.
- 자료구조 방법에는 Set계열, List계열, Map계열이 있습니다.
- java는 java.util 패키지의 자바 컬렉션(JCF)에서 자료구조 방법을 제공합니다.


## *Set*
    - 순서가 없고 중복안됨
    - HashSet, TreeSet

> SetTest

```java
package collectiontest;
import java.util.*;
public class SetTest {

public static void main(String[] args) {
	HashSet list=new HashSet();
	list.add("lee");//0
	list.clear();//모두 제거
	list.add("cho");//1
	list.add("kim");//2
	list.add("chung");//3
	list.add("min");//4
	list.add("chung");//3과 동일
	System.out.println("set 사이즈:"+list.size());//size()
	System.out.println(list.contains("chung"));
	list.remove("kim");//2제거
	System.out.println("kim 제거후 set 사이즈:"+list.size());
	System.out.println("Iterator객체 이용해서 set출력");
	print(list);
	System.out.println("배열을 이용해서 set출력");
	print(list.toArray());
}
public static void print(Set set){
	Iterator iter=set.iterator();
	while(iter.hasNext()){
		String str=(String)iter.next();
		System.out.println(str);
	}
}//
public static void print(Object [] obj){
	int count=obj.length;
	for(int i=0;i<count;i++){
		System.out.println(obj[i]);
	}
}//

```

}

## List
- 순서가 있고 중복이 가능합니다.
- ArrayList, LinkedList, Vector

> ListTest1


```java
package collectiontest;
import java.util.*;
public class ListTest1 {

public static void main(String[] args) {
	ArrayList list=new ArrayList();
	list.add("lee");//0
	list.clear();//모두 제거
	list.add("cho");//1
	list.add("kim");//2
	list.add("chung");//3
	list.add("min");//4
	list.add("chung");//3과 동일
	System.out.println("ArrayList 사이즈:"+list.size());//size()
	System.out.println(list.contains("chung"));
	list.remove("kim");//2제거
	list.remove(3);//cung제거
	System.out.println("ArrayList 사이즈:"+list.size());
	System.out.println("min이 있는 위치값:"+list.indexOf("min"));

	System.out.println("Iterator를 이용해서 출력");
	print(list);
	System.out.println("배열를 이용해서 출력");
	print(list.toArray());
	//ArrayList 에서 0에서 1까지의 데이타 추출
	List sublist=list.subList(0,2);//0~2-1까지
	System.out.println("추출된 데이타만 출력");
	print(sublist);
	System.out.println("for문을 이용해서 출력");
	printGet(list);
}
public static void print(List list){
	Iterator iter=list.iterator();
	while(iter.hasNext()){
		String str=(String)iter.next();
		System.out.println(str);
	}

}//
public static void print(Object [] obj){
	int count=obj.length;
	for(int i=0;i<count;i++){
		System.out.println(obj[i]);
	}
}//
public static void printGet(List set){
	int count=set.size();
	for(int i=0;i<count;i++){
		System.out.println(set.get(i));
		//String str=(String)set.get(i)
	}
}//


}
```

### Vector의 정의 및 요소 검색, 크기 조절

```text
   java.lang.Object
   |
   +--java.util.AbstractCollection
   |
   +--java.util.AbstractList
   |
   +--java.util.Vector
```

- 모든 구현 인터페이스
  - Cloneable 
  - Collection 
  - List 
  - RandomAccess 
  - Serializable

- 직계의 기존의 서브 클래스
  - Stack

> SearchDelete.java


```java
package collectiontest;
import java.util.*;

public class SearchDelete{
public static void main(String args[]){
String name[]={"기획자","설계자","개발자"};

    Vector v = new Vector();

    //Vector에 배열 요소 저장
    for(int i =0;i<name.length; i++){
        v.addElement(name[i]);
    }

    //"개발자"가 있는지 검사
    if(v.contains("개발자")){
        int i = v.indexOf("개발자");
        System.out.println("해당 객체의 인덱스 " + (i+1) + "번째에 있습니다.");
    }
    else{
        System.out.println("해당 객체가 없습니다.");
    }

    //첫 번째 요소 삭제
    v.removeElementAt(0);

    System.out.println("===== 지우고 난 후에는 === ");

    String s="";
    for(int j=0;j<v.size();j++){
        s = (String)v.elementAt(j);
        System.out.println("Vector " + j + "번째 요소는 " + s);
    }

    System.out.println("\\n초기상태 크기........................");
    System.out.println("엘러먼트의 수는 " + v.size()); //실제 저장된 객체의 수
    System.out.println("벡터의 크기는 " + v.capacity()); //객체를 저장할 수 있는 초기 사이즈

    System.out.println("\\nv.trimToSize()후.....................");
    v.trimToSize();  //값이 할당되지 않았으면 메모리 삭제
    System.out.println("엘러먼트의 수는 " + v.size());
    System.out.println("벡터의 크기는 " + v.capacity());

    System.out.println("\\n디자이너 요소 추가후..................");
    v.addElement("디자이너");
    System.out.println("엘러먼트의 수는 " + v.size());
    System.out.println("벡터의 크기는 " + v.capacity());

    System.out.println("\\nCoder 요소 추가후..................");
    v.addElement("Coder");
    System.out.println("엘러먼트의 수는 " + v.size());
    System.out.println("벡터의 크기는 " + v.capacity());

    System.out.println("\\nPM 요소 추가후..................");

    v.addElement("PM");
    System.out.println("엘러먼트의 수는 " + v.size());
    System.out.println("벡터의 크기는 " + v.capacity());
}


}
```

### Vector의 이용 예

> Sungjuk.java


```java
import java.util.Vector;

class Sungjuk{
//멤버 변수
String name="";
int kuk = 0;
int eng = 0;
int tot = 0;
int avg = 0;

//생성자
public Sungjuk(){}
public Sungjuk(String name,int kuk,int eng){
    this.name = name;
    this.kuk = kuk;
    this.eng = eng;
    this.tot = kuk+eng;
    this.avg = (kuk+eng) / 2;
}


}
```

> VectorTest2.java

```java
public class VectorTest2 {
public static void main(String args[]){
int i=0;

    //sungjuk 객체 생성
    Sungjuk s = null;
    Sungjuk s1 = new Sungjuk("기획자",100, 80);
    Sungjuk s2 = new Sungjuk("설계자",80, 90);
    Sungjuk s3 = new Sungjuk("개발자",90, 80);

    //Vector에 요소 저장
    Vector v = new Vector();

    /*
    public void addElement(Object obj)
    ↓
    Object obj = s1;
    ↓
    Vector에 (Object)s1 타입으로 저장됩니다.

     Object <-- 외부에서 요소 추출시 Object가 리턴
    ┌-------┐
    │Sungjuk│
    │  s1   │
    └-------┘

     Client ---> Object Interface <---> Sungjuk 객체

    */

    v.addElement(s1);
    v.addElement(s2);
    v.addElement(s3);

    //vector에 저장된 sungjuk객체 추출하여 출력
    for(i=0; i<v.size(); i++){
        s = (Sungjuk)v.get(i);
        System.out.print(s.name + "\\t");
        System.out.print(s.kuk + "\\t");
        System.out.print(s.eng + "\\t");
        System.out.print(s.tot + "\\t");
        System.out.print(s.avg + "\\t\\n");
    }
}

}
```


###  java.util.ArrayList

- Vector와 같은 목적을 가지고 있으며 기능이 비슷합니다.
- Vector와의 차이점은 네트워크를 통한 객체 공유시 동기화 처리가 되어
  있지 않습니다.
- 속도는 Vector보다 빠른 속도를 가지고 있습니다. 굳이 객체를 스레드를
  이용해 공유할 경우가 아니면 ArrayList 사용을 권장합니다.

```text
java.lang.Object
|
+--java.util.AbstractCollection
|
+--java.util.AbstractList
|
+--java.util.ArrayList
```

- 모든 구현 인터페이스
  - Cloneable 
  - Collection 
  - List 
  - RandomAccess 
  - Serializable


> ArrayListTest.java

```java
import java.util.ArrayList;

class Jumsu{
//멤버 변수
String name="";
int kuk = 0;
int eng = 0;
int tot = 0;
int avg = 0;

//생성자
public Jumsu(){}
public Jumsu(String name,int kuk,int eng){
    this.name = name;
    this.kuk = kuk;
    this.eng = eng;
    this.tot = kuk+eng;
    this.avg = (kuk+eng) / 2;
}


}
```
> ArrayListTest.java

```java
public class ArrayListTest {
public static void main(String args[]){
int i=0;

    //sungjuk 객체 생성
    Jumsu s = null;
    Jumsu s1 = new Jumsu("왕눈이",100, 80);
    Jumsu s2 = new Jumsu("아로미",80, 90);
    Jumsu s3 = new Jumsu("투투",90, 80);

    //Vector에 요소 저장
    ArrayList v = new ArrayList();

    /*
    public void addElement(Object obj)
    ↓
    Object obj = s1;
    ↓
    ArrayList에 (Object)s1 타입으로 저장됩니다.

     Object <-- 외부에서 요소 추출시 Object가 리턴
    ┌-------┐
    │Sungjuk│
    │  s1   │
    └-------┘

     Client ---> Object Interface <---> Sungjuk 객체

    */

    v.add(s1);
    v.add(s2);
    v.add(s3);

    //ArrayList에 저장된 sungjuk객체 추출하여 출력
    for(i=0; i<v.size(); i++){
        //Client ---> Object Interface <---> Sungjuk 객체
        //Client ---> Sungjuk Interface <---> Sungjuk 객체
        s = (Jumsu)v.get(i);
        System.out.print(s.name + "\\t");
        System.out.print(s.kuk + "\\t");
        System.out.print(s.eng + "\\t");
        System.out.print(s.tot + "\\t");
        System.out.print(s.avg + "\\t\\n");
    }
}


}
```

## Map
- Key, value 한쌍
- HashMap, Hashtable
- put 메서드로 입력합니다.
- 중복된 키 값을 허용하지 않습니다. 만약 사용하게되면 기존의 값이 삭제됩니다.
- 검색 결과가 없으면 null을 리턴합니다.

> MapTest


```java
import java.util.*;
public class MapTest {

public static void main(String[] args) {
	HashMap list=new HashMap();
	list.put("0","lee");//0
	list.clear();//모두 제거
	list.put("1","cho");//1
	list.put("2","kim");//2
	list.put("3","chung");//3
	list.put("4","min");//4
	list.put("3","jung");//3과 동일 에러
	System.out.println(list.size());//size()
	System.out.println(list.containsKey("3"));
	list.remove("2");//2제거 key를 이용
	System.out.println(list.size());

	print(list);//Set 만들기
}
public static void print(Map sets){
	Set set=sets.keySet();//key값을 Set으로
	Iterator iter=set.iterator();
	while(iter.hasNext()){
		String key=(String)iter.next();
		System.out.println(key+"  "+sets.get(key));//value
	}
}//


}
```

### java.lang.Object

```text
    java.lang.Object
    |
    +--java.util.Dictionary
    |
    +--java.util.Hashtable
```

- 모든 구현 인터페이스
  - Cloneable 
  - Map 
  - Serializable

- 직계의 기존의 서브 클래스
  - Properties 
  - UIDefaults


> TestHashTable.java


```java
import java.util.Hashtable;

public class TestHashTable {

    public static void main(String[] args) {
        Hashtable ht = new Hashtable();
    
        ht.put("AREA01", "대한민국");
        ht.put("AREA02", "러시아");
        ht.put("AREA03", "중국");
        ht.put("AREA04", "일본");
    
        String area = (String)ht.get("AREA01");
        //String area = (String)ht.get("AREA05");
    
        if ( area != null){
            System.out.println(area);
        }else{
            System.out.println("검색 지역이 없습니다.");
        }
    }
}
```

###  Properties
- 속성값 부여를 목적으로 합니다.

```text
    java.lang.Object
    |
    +--java.util.Dictionary
    |
    +--java.util.Hashtable
    |
    +--java.util.Properties
```



- 특정 객체 생성시 생성자에 초기값으로 속성값을 주는 역활을 합니다.

```java
  java.util.Properties p = new java.util.Properties();
  p.put(Context.INITIAL_CONTEXT_FACTORY, "weblogic.jndi.WLInitialContextFactory");
  p.put(Context.PROVIDER_URL, "t3://192.168.0.1:7001");
  ctx=new InitialContext(p);// 부분으로 변경할 것
```

> ProTest.java

```java
//import java.util.Properties;

public class ProTest {

public static void main(String[] args) {

    //Properties p = new Properties();
    java.util.Properties p = new java.util.Properties();
    p.put("step1", "JAVA + SCJP");
    p.put("step2", "JSP + Oracle + SCWCD");
    p.put("step3", "EJB + SCBCD");
    p.put("step4", "OJT + MVC2, Framework + 개발");

    System.out.println("STEP1:" + p.getProperty("step1"));
    System.out.println("STEP2:" + p.getProperty("step2"));
    System.out.println("STEP3:" + p.getProperty("step3"));
    System.out.println("STEP4:" + p.getProperty("step4"));
}


}
```
