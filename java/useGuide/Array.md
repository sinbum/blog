# 배열

## 배열 사용하기

- 배열의 장점:
  . 통일된 하나의 변수명으로 다량의 데이터를 처리할수 있습니다.
  . 각각의 데이터에 공통된 연산작업을 적용할 수 있습니다.
  . 변수 사용을 줄임으로 코드를 간결하게 할 수 있습니다.
- 배열의 단점:
  . 배열의 요소를 선언하고 전부 이용하지 않으면 심각한 메모리 낭비가 발생합니다.
  . 자바는 이 문제를 개선한 여러형태의 Collection Class들이 존재합니다.
  . 배열의 사이즈는 필요에 따라 증가시키거나 감소할수가 없습니다.
- 배열의 사용예:
  . 사이즈가 변경되지 않는 데이터 배열인 경우
  . 1월 ~12월, 월요일~일요일, 각종 지정된 공휴일
  . 각 학교의 학년(1~6, 1~3, 1~4)
- index를 통한 배열 요소의 구분: 배열명[인덱스]=값
- 배열의 요소가 일정한 경우만 사용하고 요소의 갯수를 알수 없는 경우는 Collection Class를 사용해야 합니다.
### 배열의 선언
- int[] weight = new int[7]; (접근 범위: weight[0]~weight[6])
- int weight[] = new int[7]; 4 * 7 = 28 바이트 할당
- int weight[]={100, 200}; 자동으로 배열 요소가 결정이 되고 값이 할당됩니다.
### 배열요소에 값 저장
   - weight[0] = 3  
   - weight[1] = 6
### 1차원 배열 이용
```
public class DevEnvironment {
    public static void main(String[] args) {
        String[] lang = new String[3];
        String[] script = new String[3];
        String[] dbms = {"Oracle","ms-sql","my-sql"};
    
        lang[0] = "JAVA"; 
        lang[1] = "C#"; 
        lang[2] = "C";
        
        script[0]="JSP";
        script[1]="ASP.NET";
        script[2]="PHP";
    
        for(int i=0; i<=2; i++){
            System.out.println(lang[i] + "-"+script[i]+"-"+dbms[i]);
        }
    
    }

}
```


## 다차원 배열의 이해 및 활용

- 2차원 배열은 일반적으로 for문을 2개이상 동반합니다.
- 1차원(열), 2차원(행, 열), 3차원(면, 행, 열) 배열의 구조

> Two_Array.java
 
```
class Two_Array {
    public static void main (String args[]) {
    int[][] m = {{10,20},  //1행
    {30,40},  //2행
    {50,60}}; //3행
    >
    
      /*
        int[][] m2 = new int[3][2];
    
        0,0(10)   0,1(20)
        1,0(30)   1,1(40)
        2,0(50)   2,1(60)
    
        m2[0][0] = 10;
        m2[0][1] = 20;
        m2[1][0] = 30;
        m2[1][1] = 40;
        m2[2][0] = 50;
        m2[2][1] = 60;
    
       */
    
      for(int i=0; i<3; i++) {     //행
         for(int j=0; j<2;j++) {   //열
            System.out.println("m[" + i + "]n[" + j + "]=" + m[i][j]);
         }
      }
    
    
    }
}
```

> MultiArrayTest.java

- length 속성은 for문의 반복횟수를 결정하는데 사용됩니다.
- 3차원 배열은 [면][행][열]로 이루어져 있으며 프로그래밍분야에서 사용되지 않습니다.


```
class MultiArrayTest{
    public static void main(String args[]){
    //1차원 배열
    int[ ] arr1 = new int[3];
        //2차원 배열
        int[ ][ ] arr2;
        arr2 = new int[2][3];
    
        //1차원 배열은 컬럼의수를 리턴합니다.
        System.out.println("arr1배열의 열의 수 : " + arr1.length + "\\n");
    
        //2차원 배열은 행의수를 리턴합니다.
        System.out.println("arr2배열의 행의 수 : " + arr2.length + "\\n");
    
        //각행의 열의수를 리턴합니다.
        System.out.println("arr2배열의 1행의 열의 수 : " + arr2[0].length + "\\n");
        System.out.println("arr2배열의 2행의 열의 수 : " + arr2[1].length + "\\n");
    
    }

}

```
