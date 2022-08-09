---
description: system daemon 을 관리하는 systemctl 사용.
---

# Systemd
systemd는 unix 시스템이 부팅 후 프로세스를 실행하는 역할을 합니다.

![Systemd Utilities](https://en.wikipedia.org/wiki/Systemd#/media/File:Systemd_components.svg)
[출처링크 : 위키피디아](https://en.wikipedia.org/wiki/Systemd#/media/File:Systemd_components.svg)


# Systemctl 사용


## 서비스 확인
- 서비스의 상태를 확인하려면 다음과 같이 BASH 명령을 합니다.
    ```shell
    systemctl status 서비스이름
    ``` 
- nginx 서비스의 상태를 출력 하는 예제
    ```shell
    systemctl status nginx
    ```

## 서비스 구동
- 서비스를 구동하려면 start 명령을 사용합니다.
    ```shell
    systemctl start mongodb
    ```

## 서비스 자동 시작
- enable 의 명령으로 부팅시 자동시작이 되도록 설정이 가능합니다.
    ```shell
    systemctl enable mongodb
    ```

## 서비스 목록 출력
- list-units 명령으로 서비스의 목록을 출력 할 수 있습니다.
    ```shell
    sudo systemctl list-units
    ```
- 설치된 모든 unit 파일을 보기위해서 list-unit-files를 사용합니다.
    ```shell
    sudo systemctl list-unit-files
    ```
## 서비스 마스킹
동일한 용도로 사용하는 서비스가 동시 설치된 경우 충돌을 방지하기 위해서 mask 명령어를 사용합니다.

- 예)
    ```shell
    sudo systemctl mask ntpd
    ```
- 실수로 ntpd 를 실행하는 경우에는 마스킹이 되어 실행이 되지 않습니다.
    ```shell
    sudo systemctl start ntpd
    # Failed to start ntpd.service: Unit is masked.
    ```
  
- 마스킹된 서비스를 해제하려면 systemctl unmask 명령어를 실행합니다.
    ```shell
    sudo systemctl unmask ntpd
    # Removed symlink /etc/systemd/system/ntpd.service
    ```
## 그 외 기능
- enabled 된 모든 서비스 확인
    ```shell
    sudo systemctl list-units --state=enabled
    ```
- 구동에 실패한 서비스 확인
    ```shell
    sudo systemctl list-units --state=failed
    ```
- 현재 실행중인 active 목록
    ```shell
    sudo systemctl list-units --state=active
    ```
- 상태가 inactive 인 목록
    ```shell
    sudo systemctl list-units --state=inactive
    ```
- 상태가 running 인 목록
    ```shell
    sudo systemctl list-units --type=service --state=running
    ```
- 특성서비스가 active 상태인지 조회할 경우
    ```shell
    sudo systemctl is-active connector
    ```
- 특정서비스가 enabled 상태인지 조회할 경우
    ```shell
    sudo systemctl is-enabled connector
    ```