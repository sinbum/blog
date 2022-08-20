
## LED 깜박임 예제를 통해 디지털 출력
LED를 아두이노 보드에 다이렉트에 연결할 수 있는 이유는 LED에 이미 저항이 연결되어 있어서 저항 없이 회로를 구성해도 문제가 되지 않습니다.
- LED 설명
    - LED는 다리가 긴 쪽이 (+)
    - 다리가 짧은 쪽은 (-)
- LED 연결
    - LED 다리가 긴 쪽을 우노보드 13에 연결 합니다.
    - LED 다리가 짧은쪽을 우노보드 GND에 연결 합니다.
    - LED 다리가 짧은쪽을 우노보드 GND에 연결 합니다.

```c
void setup() {
  // put your setup code here, to run once:
  // SETUP 함수는 보드에 전원 공급 또는 리셋 버튼을 눌렀을때 한번 실행됩니다.
  
  pinMode(13,OUTPUT); // 13번 디지털 핀을 출력으로 설정
}

void loop() {
  // put your main code here, to run repeatedly:
  // loop 함수는 전원이 켜저 있는 동안 무한 반복휴ㅐ서 실행됩니다.

  
  digitalWrite(13,HIGH); //번 핀에 high 설정 . LED
  delay(100); // ms 단위. 대기시간지연  
  
  digitalWrite(13,LOW);
  delay(1500); // 딜레이 함수를 한번 더 적용합니다.  
}
```
