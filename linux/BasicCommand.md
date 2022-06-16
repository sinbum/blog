# 리눅스 기본 명령어
---

## 리눅스 관련 웹 정보 사이트 링크
> - JSLinux : https://bellard.org/jslinux/  : 리눅스를 웹사이트에서 간단하게 연습해 볼 수 사이트.
>  

## 목차

1. ls
2. cd
3. pwd
4. rm
5. cp
6. touch
7. mv
8. mkdir
9. rmdir
10. cat
11. head,tail
12. more
13. less
14. file
15. clear


## 명령어 설명
### ls
    List 의 약자로 디렉터리폴더에 있는 파일을 나열합니다.

- ls
  - 현재 디렉터리의 파일 목록을 표현
- ls /etc/sysconfig
  - 지정한 디렉터리의 목록을 표현합니다.
- ls -a
  - 숨김파일을 포함한 디렉터리의 목록을 표현합니다
- ls -l
  - 현재 디렉터리의 목록을 자세히 보여줍니다.
- ls *.cfg
  - cfg 확장자의 파일을 보여줍니다.
- ls -l /etc/sysconfig/a*
  - 지정한 디렉토리에 목록을 자세히 보여줍니다.

### cd
    Change Directory의 약자로, 디렉터리를 이동하는 명령어 입니다.
    
- cd
  - 사용자의 홈 디렉터리로 이동합니다. 
  - 현재 사용자가 'root' 라면 '/root' 경로로 이동합니다.
- cd ~centos
  - centos 사용자의 홈 디렉터리로 이동합니다.
- cd .. 
  - 상위 경로로 이동합니다.
- cd /etc/sysconfig
  - 절대경로로 이동합니다. /etc/sysconfig
- cd ../etc/sysconfig
  - 상대 경로로 이동합니다.
  - 만약 현재 나의 디렉터리 경로가 /home 이라면 현재 경로의 home/etc/sysconfig 으로 이동합니다
  - 
### pwd
    Print Working Directory 의 약자로, 현재 디렉터리의 전체 경로를 화면에 보여줍니다.

### rm
    ReMove의 약자로, 파일이나 디렉터리를 삭제합니다. 삭제시에는 권한이 필요합니다. 'root'권한은 제약이 없습니다.

- rm abc.txt
  - abc.txt 파일을 삭제합니다.
  - 이 기본명령어는 rm -i 옵션과 같은 명령어 입니다.
- rm -i abc.txt
  - 삭제시에 정말로 삭제할 것인지 확인하는 메세지가 나옵니다.
- rm -f abc.txt
- rm -r abc
- rm -rf abc

### cp
    Copy 의 약자로, 파일이나 디렉터리를 복사합니다. 복사 할 파일의 읽기 권한이 필요합니다.

- cp abc.txt bbb.txt 
  - abc.txt를 bbb.txt라는 이름으로 바꿔서 복사합니다.
- cp -r abc cba
  - 디렉터리를 복사합니다.


### touch
    크기가0인 새 파일을 생성하거나, 이미 파일이 존재한다면 파일의 최정 수정 시간을 변경합니다.

- touch abc.txt
  - 파일이 없을 경우 abc.txt 빈파일을 생성하고, 있을경우는 수정시간을 현재 시각으로 변경합니다.

### mv
    Move의 약자로, 파일이나 디렉터리의 이름을 변경하거나 다른 디렉터리로 옮길 때 사용합니다.
- mv abc.txt /etc/sysyconfig
  - abc.txt 파일을 지정한 경로에 위치를 변경합니다.  
- mv abc.txt www.txt abc.txt의 이름을 www.txt로 변경해서 이동 시킵니다.

### mkdir
**Make Directory의 약자로, 새로운 디렉터리를 생성합니다.**


- mkdir abc
  - 현재 디렉토리에 abc 폴더를 생성합니다.
  - mkdir -p /def/fgp 
    - /def/fgh 디렉터리를 생성하는데, 만약에 /fgh 디렉터리의 부모 디렉터리인 '/def' 디렉터리가 없다면 자동으로 생성합니다
    - 옵션 -p 는 Parent를 뜻합니다.


### rmdir
**ReMove Directory의 약자로 , 디렉터리를 삭제합니다.**
- rmdir abc
  - 해당 디렉터리의 삭제 권한이 있어야 합니다


### cat
**conCATenate 의 약자로, 파일내용을 화면에 보여줍니다.**

- cat a.txt
  - a.txt 의 텍스트를 콘솔창에서 미리보기 할 수 있습니다.

### head,tail
**텍스트 형식으로 작성된 파일의 앞 또는 마지막의 라인을 미리보기합니다.**
- head anaconda-ks.cfg
  - 해당 파일의 앞 10행을 화면에 출력합니다.
  - 파일 내용이 너무긴 경우 cat 명령어 보다 head 명령어를 이용한다면 내가 원하는 부분 까지 미리보기 할 수 있습니다.
- tail -5 anaconda-ks.cfg
  - 마지막 5행만 화면에 출력합니다.

### more
**텍스트 형식으로 작성된 파일을 페이지 단위로 화면에 출력합니다.**

- more anaconda-ks.cfg
  - '스페이스바'를 누를경우 다음페이지로 이동하고 'B' 를 누르면 앞 페이지로 이동합니다.  'Q' 는 종료입니다.
- more +100 anaconda-ks.cfg 
  - 100부터 출력합니다.
  
### less
**more 명령과 용도가 비슷하지만 기능이 더 확장되어 있습니다.**

- less ananconda-ks.cfg
- less +100 anaconda-ks.cfg
  - 100행부터 출력
  

### file
**해당하는 파일이 어떤종류의 파일인지 표시합니다.**
- file anaconda-ks.cfg
  - 해당 파일은 텍스트 파일이므로 아스키 파일로 표시됩니다.
- file /dev/sr0
  - sr0은 DVD 장치이므로 block special로 표시됩니다.

### clear
**현재 사용중인 터미널 화면을 깨끗하게 지워줍니다.**

- clear



