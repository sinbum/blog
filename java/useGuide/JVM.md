# JVM 메모리

## System Memory Model

자바에서의 구획별 메모리는 64KB단위로 구분되어 있습니다.

```text
┌───────────┐CS: Code Segment
│[코드 영역]                 │
│Test Class의 Source가 │
│등록되는 영역              │
├───────────┤DS: Data Segment
│[Data 영역]                │
│static변수,                  │
│static 메소드 저장        │
│main()                       │
│객체를 만들지 않아도   │
│이영역의 요소 사용가능│
├──────────-┤SS: Stack Segment
│[Stack 영역]              │
│메소드가 사용하는 영역│
│메소드 안에서 선언되는│
│지역변수가 선언,         │
│메소드 처리가 끝나면   │
│메모리가 자동으로       │
│회수됨                       │
├─────────-─┤HS: Heap Segment
│[Heap 영역]               │
│객체가 생성되면          │
│존재하는 영역,            │
│RAM의 양에 따라 무한대│
│GC의 대상이 되는 영역 │
└───────────┘
```
---

## JVM Memory Model
 - JAVA 소스가 들어가는 영역
 - 객체가 HashCode를 받는 과정
 - HashCode와 Memory Address의 연계과정
 - Heap에 할당되는 인스턴스 변수
 - 객체의 사이즈
 - 메소드안에서 사용하는 Stack Memory
 - Code Area에 저장되는 공유메소드
 - this, super의 존재 이유
 - Call By Value, Call By Reference호출과정
 - Garbage Collecting 과정