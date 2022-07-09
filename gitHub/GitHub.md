


# 실무에서 사용하는 Gti 분기 모델.
팀에서 소프트웨어를 지속적으로 제공해야 할때는 간결하고,쉬운 워크플로우를 따르는 것이 좋습니다. 그 이유는 우리가 항상 그래왔든 시작은 심플하지만 점점 많아지는 코드와 구조에 따라서 복잡성을 띄기 때문입니다.
그러므로 항상 주의 해야 합니다.  
프로젝트를 함에 있어서 이점이 되는, 그리고 효율적이지만 최대한 협업을 갖출 수 있는 방법으로써 현업에서도 자주 사용하는 워크플로우에 대한 설명을 해볼까 합니다.  
아마 실무에서는 아주 많이 사용되고 있는 방식이지만, 주니어 개발자, 취업준비중인 개발자를 위해서 유용한 정보를 제공하고자 합니다.  


![Vincent Driessen](https://nvie.com/img/git-model@2x.png)
[Vincent Driessen 의 성공적인 Git 분기 모델](https://nvie.com/posts/a-successful-git-branching-model/)

## 중앙집중형 관리 방식
대부분 개발자들은 origin 에서 가져오고 푸시 합니다.
중앙 집중형은 다음 사진과 같습니다.

![centralrized Git Flow](https://nvie.com/img/centr-decentr@2x.png)

origin을 중심으로 각 팀은 맡은일을 분리하여 업무를 담당 할 수 있습니다. 각 개발자나 팀은 서로의 변경사항을 가져와서 하위 팀을 따로 구성 할 수도 있습니다. 
만약 alice라는 사람이 origin 의 코드가 아닌 david의 코드를 함께 사용하여 개발을 해 나갈 수 도 있죠. origin에는 영향을 미치지 않으면서 협업이 자유롭다는 부분입니다.

## master 브랜치 와 develop

- master(현재는 main)
- develop

![main & develop](https://nvie.com/img/main-branches@2x.png)

master 브랜치는 배포 버전의 브런치 입니다. 
실제 배포되는 최종사항의 내용만 커밋하지만 dvelop에서는 자주 변경 적용되고 최신사항을 반영 합니다. 
이곳에서 모든 개발자의 push 와 merge 현상이 일어납니다. 
베타 버전을 체크하거나 테스트를 하는경우 등등 혹은 배포를 시작하기전 대기상태 에 이르는 반영 사항이 바로 devleop 브런치 인 것입니다.


## develop 분기
앞서 설명한대로 develop 브런치에서의 활동은 수없이 많이 일어 납니다. master는 배포 상태에 있는 분기 이지만 develop 에서는 다음 기능들을 포함합니다.

- Feature (기능에 따라 분류)
- Release (배포를 위한 분류)
- Hotfix (긴급 수정)

### feature 분기
feature 분기는 develop 에서 다시 feature 로 분리됩니다. 이 워크 플로우는 지라 일감을 생성하여 각 기업에서 지정한 규칙을 가지고 업무를 배정할 수 있습니다.
이는 훨씬 효율적이며 단위적이므로 일을 효율적으로 할 수 있습니다. feature분기는 develop 분기로 병합되며 새로운 업무를 배정받거나, 단위적으로 기능을 추가할때에는 devleop 에서 새로운 feature브랜치를 생성합니다.
기능 분기는 일반적으로 개발자 저장소에만 존재합니다. 

기능브런 치 생성.

```shell
git checkout -b feaure_{projectName}_{일감번호} develop
```

로컬 환경에서 개발 후 적용되어 다음 완성된 기능을 통합하는 경우는 다음과 같이 진행합니다.

```shell
git checkout
 # development 'develop' {브랜치로 전환} 
git merge --no-ff myfeature ea1b82a..05e9557
  
git branch -d myfeature myfeature
 # 브랜치 삭제(기존 05e9557). 
git push origin develop
```


--no-ff 은 병합으로 항상 새 커밋 개체를 생성하도록합니다. 이렇게 하는 경우에는 기능 분기의 과거 정보가 손실되는것을 방지 합니다.  
[--ff,--no-ff 의 차이점 - 작성자 : koreabigname](https://koreabigname.tistory.com/65)

### 배포 분기
develop 에서 분기가 가능합니다. 그리고 master로 병합 합니다.
배포 시에는 {release}_{배포명} 등으로 규칙을 생성하여 배포 에 대한 명명을 확실하게 지켜주도록 합니다.

릴리즈(배포)분기는 새로운 버전의 준비를 합니다. 또 버그 수정 과 배포에 대한 메타 데이터를 사용함으로써 배포가 완료되기 전의 모든 준비를 끝마칩니다.
전투기가 이륙하기전 기름을 채우고 모든 검토를 마친것과 마찬가지인 상태입니다.

새 릴리즈 분기를 하는 때에 develop 브랜치는 모든 develop 브랜치가 가지고있는 모든 새로운 기술이 반영된 상태 입니다.   
향후에 새로운 기술은 또 다음의 release 버전에 포함될 수 있도록 해야합니다.

**릴리즈 브랜치 생성**
버전 1.1.5가 현재 제공 상태이고 큰 배포버전이 있고, 현재 develop의상태는 다음 배포에 대한 준비가 되어있다면 그리고 그 버전을 1.2.0 으로 지정 했다면 브런치는 다음과 같이 생성 하도록 합니다.

```shell
$ git checkout -b release-1.2
 development 새 분기 "release-1.2"로 전환 
$ ./bump-version.sh 1.2
 파일이 성공적으로 수정되었으며 버전이 1.2로 변경되었습니다. 
$ git commit -a -m "Bumped version number to 1.2" 
[release-1.2 74d9424] Bumped version number to 1.2 
1 파일 변경, 1 삽입(+), 1 삭제(-)
```

새 분기를 만들고 전환 후 버전 번호를 변경합니다.
다음 bump-version.sh 은 작업 복사본의 일부 파일을 새 버전으로 반영하도록 하는 쉘 스크립트 입니다.

**배포 분기 완료 명령**
```shell
$ git checkout master
 'master' 브랜치로 전환 
$ git merge --no-ff release-1.2
$ git tag -a 1.2
```
병합을 통해 배포를 완료하고 태그도 지정합니다.

**개발 브런치 또한 병합** 시켜줍니다.
```shell
$ git checkout
 development 'develop' 브랜치로 전환 
$ git merge --no-ff release-1.2
```

develop 분기 에서는 병합 충돌 이슈 가능성이 있기 때문에 이전 버전의 브런치를 삭제하도록합니다.
```shell
$ git branch -d release-1.2
```

### 핫픽스 분기
아주 중요한 부분입니다.  
먼저 다음 사진의 플로우를 확인하고 진행하도록 하겠습니다.

![HotFix 분기](https://nvie.com/img/hotfix-branches@2x.png)

예를 들어 실제 배포환경에서 치명적인 결함이나 버그가 발생했을때 '롤백'이나'핫픽스'라는 단어를 보통 게임의 업데이트 패치내용에서 한번쯤은 들어 보았을법 합니다.
마찬가지로 핫픽스 분기는 위 사진처럼 플로우로 해결하며 이는 마스터 브랜치에서 핫픽스로 직접적으로 단계를 수정하거나, 치명적이지 않지만 우선순위로 해결해야 하는 경우 develop 환경에서 수정하도록 할 수 있습니다.
핫픽스 브랜치 생성은 다음과 같이 진행합니다.

```shell
$ git checkout -b hotfix-1.2.1 master
 새 분기 "hotfix-1.2.1"로 전환 
$ ./bump-version.sh 1.2.1
 파일이 성공적으로 수정되었으며 버전이 1.2.1로 변경되었습니다. 
$ git commit -a -m "Bumped version number to 1.2.1" 
[hotfix-1.2.1 41e61bb] Bumped version number to 1.2.1 
1 파일 변경, 1 삽입(+), 1 삭제(-)
```
분기 후 에 버전 번호를 꼭 올려 수정하도록합니다.
그 다음 버그를 수정했다고 가정하고 하나 이생의 개별 커밋에서 수정사항을 커밋합니다.

```shell
$ git commit -m "심각한 프로덕션 문제 수정" 
[hotfix-1.2.1 abbe5d6] 심각한 프로덕션 문제 수정 
5개 파일 변경, 32개 삽입(+), 17개 삭제(-)
```

**핫픽스 분기 완료**

버그 이슈를 개선하고 master 브랜치로 병합 해야 하지만 develop(1.2.0)에도 적용 시켜 주어야 합니다. 그래야 develop 브랜치가 후에 배포환경에 있어서도 마찬가지로 버그가 수정이 된 상태로 이루어 져야 하기 때문이죠.

```shell
$ git checkout master
 'master' 브랜치로 전환 
$ git merge --no-ff hotfix-1.2.1
 재귀로 병합. 
(변경사항 요약) 
$ git tag -a 1.2.1
```

```shell
$ git checkout develop
 development 'develop' 브랜치로 전환 
$ git merge --no-ff hotfix-1.2.1
 재귀로 병합. 
(변경 사항 요약)
```

다음 릴리즈 분기가 존재하는 경우에는 변경사항을 적용 시켜야 하기떄문에 다음 대기 릴리즈 에 핫픽스를 적용시키기 위해 병합을 시킬수도 있습니다. 
또는 핫픽스 이전의 릴리즈 버전을 삭제하고 재 생성을 할 수도 있습니다.


