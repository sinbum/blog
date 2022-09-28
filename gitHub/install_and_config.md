---
description : 깃허브 설치 및 초기 세팅 안내.
---

# github 설치 (linux)
- 리눅스 설치시
- 윈도우 설치시

## 리눅스 설치

- OS에 따른 설치.  
  - 우분투 : sudo apt install git
  - 록키   : sudo dnf install git
  - 기타 레드햇 계열 : sudo yum install git
- 버전확인  
  - git --version
- 초기 이름,메일 설정
  - git config --global user.name {이름}
  - git config --global user.mail {메일 주소}
- 깃허브 레포지토리 클론
  - git clone {git repository address}

## 윈도우 설치

![git-scm.com](images/git_scm_web.png)  

하위 링크로 접속 후 위와 같은 화면에서 윈도우 에따른 버전 설치를 진행합니다.  
윈도우내 설치시 패키지로 들어있어 git-bash 도 함께 있어 깃을 위한 몇가지 ui와 기능을 제공합니다.    
때문에 사용측면에서 현재 브런치나 커밋정보 텍스트 색상으로 구분하기 쉽게 표현되어 편리하게 이용 할 수 있습니다.

[깃허브 다운로드 링크 : git-scm.com](https://git-scm.com/downloads)


## SSH로 접속.
깃허브에서는 다음과 같이 3가지 방법으로 깃을 접근 할 수 있습니다.
- 깃허브 HTTPS 로 접속
- ssh 인증서를 발급 후 접속 및 사용
- git client를 이용해 접근(소스트리,깃 데스크탑 등 형상관리 프로그램)
ssh 접근을 설정하면, username과 비밀번호를 입력하지 않고도 깃허브와 함께 접근 할 수 있습니다.

다음은 **ssh 를 생성하고 사용하는 순서** 입니다.
1. SSH key 생성 여부 확인.
2. SSH key 생성
3. SSH key-agent 에 키 등록하기
4. 깃허브 내 ssh 개인키 추가


1. SSH key 생성 여부 확인.
   - 아래 명령으로 이미 생성된 ssh 키가 존재하는지 확인 할 수 있습니다.   
   - ls -al ~/.ssh
2. SSH key 생성
   - ssh key를 생성하는 'ssh-keygen'으로 github에 등록된 자신의 메일 계정을 추가한 ssh key를 생성합니다. 
   - 또한 -t 옵션을 통해 rsa,dsa,등 옵션으로 암호화 키를 생성 할 수있습니다. 아래 예제는 ed25519키 암호화 방식을 이용합니다.
   - ssh-keygen -t ed25519 -C "your_email@example.com"
   - ed25519는 최신 암호화 방식으로 rsa를 대체 할 수도있습니다.
     - ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
3. SSH key-agent 에 키 등록하기
  - ssh-agent를 실행 함으로써 pid 번호를 부여받은것을 확인 할 수 있습니다.
  - ```shell
    eval "$(ssh-agent -s)"
    Agent pid 62393
    ```
  - config 파일 설정하기
    - vi ~/.ssh/config 파일에 다음과 같은 내용을 추가합니다.
    - ```text
    Host *
    AddKeysToAgent yes
    UseKeychain yes
    IdentityFile ~/.ssh/id_ed25519
    ```
  - ssh-agent 에 ssh 개인키 추가하기    
    ```shell
    ssh-add -K ~/.ssh/id_ed25519
    Identity added: /Users/sinbum/.ssh/id_ed25519 (sinbum@kakao.com)
    ```
5. 깃허브 내 ssh 개인키 추가


# 참고링크
[DEVOCEAN](https://devocean.sk.com/blog/techBoardDetail.do?ID=163311)  
[LainyZine: 프로그래머 가이드](https://www.lainyzine.com/ko/article/creating-ssh-key-for-github/)