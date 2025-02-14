# 자바 설치 가이드

## 자바 설치

### 설치시 주의사항

프로그래밍 언어를 설치할 때에 주의 할것은 아래와 같습니다.\
이것은 자바 뿐만아니라, 프레임워크,라이브러리 등 버전에 따라 달라지는 네이밍과 구조 방식 실행환경이 다르가 때문에 버전을 선택하는것은 신중해야 합니다.

* 최신버전이라고 좋은것 만은 아닙니다.
* 가급적 LTS 버전을 설치 (Long Term Support)
* 기존 사용하는 어플리케이션, 및 개발도구, 툴 등이 있을경우 버전별 호환사항에 맞게 다운로드.
* asdfasdfsadfasdfsdaf

### 회원가입 및 로그인

다운로드시에 로그인을 필요로 하므로 회원가입이 되어있지 않다면 가입 후 로그인 및 다운로드를 진행하시기 바랍니다.

### 오라클사이트접속

오라클 사이트에 접속합니다.

각 운영체제에 맞는 자바를 다운로드합니다.

개발자일 경우 > JDK 또는 OpenJDK [(OpenJDK 설명)](https://web-inf.tistory.com/30)

[https://www.oracle.com/java/technologies/downloads/](https://www.oracle.com/java/technologies/downloads/)

### 자바 JDK 다운로드

윈도우 환경에서 다운로드시 exe 파일 패키지로 설치할시에는 환경변수 까지 기본적으로 추가가 되도록 설치 할 수가 있습니다.

그 외에는 64비트와 32비트 운영체제 리눅스 레드햇계열,데비안계열 등에 따라서 수정 설치가 가능합니다.

## 삭제

윈도우에서 설치된 것을 기준으로 프로그램 추가/제거 에서 삭제가 가능합니다.

레지스트리에 등록되어있는 부분까지 삭제를 원하는 경우.

* REGEDIT 레지스트리 편집기를 실행해 "HKEY\_LOCAL\_MACHINE"를 찾아서 "SOFTWARE" --> "JavaSoft"를 삭제합니다.

리눅스계열인 경우는 설치 디렉토리제거 및 환경변수 추가제거하도록 합니다.

## 환경변수 설정

* 내컴퓨터 > 고급 > 환경변수 > 시스템 변수 영역.
* 변수 추가 : 변수명은 JAVA\_HOME, 디렉토리는 자바설치 경로지정.
* Path 변수에 경로추가 : $JAVA\_HOME%\bin (위로이동을 눌러줄 경우 CLI 환경에서 변수탐색시 우선순위를 지정합니다.)

## 자바 프로그램 실행

이클립스,인텔리J 등 다양한 IDE를 사용하여 java 코드파일을 작성 할 수 있지만, CLI를 통해 기초적으로 한 번 시도해 봄으로써 작동원리를 알아 갈 수 있는것이 바람직 하다고 생각합니다.

### JAVA파일 생성

```
//Test.java
class First {
public static void main(String[] args) {
String s = "Hello World";
System.out.println(s);
}
}
```

### CMD 명령찰 실행

1. 윈도우 CLI인 CMD창을 오픈합니다. Test.java 파일이 들어있는 경로로 이동합니다.
2. 다음 명령어를 입력해 컴파일을 실행합니다.

```
javac Test.java
```

1. 컴파일된 자바 클래스 파일을 실행합니다.

```
java Test
```
