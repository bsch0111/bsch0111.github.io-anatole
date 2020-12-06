---
title: "GIT에 대한 궁금증"
date: 2020-12-04T14:05:11+09:00
Description: ""
Tags: []
Categories: ["git"]
DisableComments: false
---

# GIT에 대한 궁금증

- Github와 Git의 차이 & .git 폴더가 어떤 일을 하는지

git의 발전방향
* 로컬 폴더에서 파일 관리 -> 데이터베이스를 이용한 로컬 버전 관리 ( VCS : Version Control System ) -> 중앙집중식 버전관리 ( CVCS : Centered Version Control System) ex. subversion ->  분산 버전 관리 시스템 (DVCS : Distributed Version Control System )
* Git 은 기존에 리눅스에서 사용하던 분산 버전 관리 시스템이 유료화 되면서 리눅스 창시자 리눅스 토발즈가 빠른 속도와 분산을 목표로하는 분산 버전 관리 시스템을 개발

.git 폴더가 어떤 일을 하는지
* git의 핵심 : 로컬 파일시스템에 버전 데이터베이스 정보를 보관함
* 기존의 Subversion과의 차이 : 기존의 Subversibon 은 서버와 작업을 하다보니 비행기를 타고 이동하거나 인터넷이 연결되지 않았을 때 버전 정보에 대한 commit을 지정할 수 가 없었음. 인터넷이 연결된 순간의 결과 정보만 서버에 올릴 수 있음
* 그러나 git은 로컬 시스템서 모든 이력정보가 담긴 데이터베이스가 있으니 비행기를 타고 이동 중이나 인터넷이 연결되지 않았을 때도 개발 작업을 진행하고 그 이력을 저장하고 싶을 때 commit 작업을 수행할 수 있음
* 서버 없이 구동할 수 있다는 점과 빠르다는 점이 크게 다름
* 이러한 git 을 구동하는데 로컬 데이터베이스의 기능을 하는게 .git 폴더이다. 다르게 보면 .git 폴더를 제거하면 해당 폴더에서는 git 과 관련된 기능을 수행할 수 없다 

git과 github의 차이
* git 을 협업 할때 쓰다보면 서버를 구동해야 할때가 많다. 자체적으로 git 저장소(서버)를 만들어서 적용할 수 있지만 이미 잘 구동되고 있는 서버에 프로젝트를 생성해서 작업하면 편하다
* github는 이미 구동되고 있는 git server이다. 여기서 프로젝트를 생성하면 git 호스팅 정보, 이슈 트래킹, 코드 리뷰 등을 추가적으로 제공한다. 물론 git을 기반으로 개인적으로 server를 개발해도 된다.


git add 와 git commit 의 차이
* git add 는 짧막한 이력정보를 남기는 것. 새로운 파일의 이력정보를 추가하거나, 수정된 파일을 스테이지에 올리고 싶을 때 add를 수행
* git commit은 로컬 데이터베이스에 올리는 것. add로 주가된 버전 정보가 로컬데이터베이스에 올라간다. 가장 최근에 변경된 정보가 올라가는 것이 아니다.

git clone을 하면 자동으로 저장소가 등록되나요
* 넵. 자동으로 등록됩니다. git clone 을 하고, git remote -v 를 보시면 clone 한 레파지토리가 등록되어 있음을 확인할 수 있습니다.

- origin 이 뜻하는 것은 무엇일까 
* 원격 저장소의 별칭 입니다.
* 저장소를 clone 하면 origin이라는 이름으로 추가한다.

- git remote 옆에 써있는 fetch의 의미 & git remote 로 여러 개의 저장소 관리하는 방법
```bash
별칭 원격레포지토리주소 (fetch)
별칭 원격레포지토리주소 (push)
```
* cf. fetch : 가져오다
* git fetch [remote-name] : 로컬 저장소에는 없지만 리모트 저장소에 있는 데이터를 모두 가져온다. 그러면 리모트 저장소의 모든 브랜치를 로컬에서 접근할 수 있어서 언제든지 Merge 하거나 내용을 살펴볼 수 있다.
* git fetch 명령은 리모트 저장소의 데이터를 가져오지만 자동으로 merge하지 않는다. 그래서 로컬에서 하던 작업을 정리하고 수동으로 merge해야한다.
 
- Pull Requests 란
* pull 명령은 리모트 저장소 브랜치를 가져올 뿐만 아니라 자동으로 로컬 브랜치와 Merge 시킬 수 있다.

- 그럼 가져오는게 clone, fetch, pull 세 가지인데, 이 세가지의 차이는 무엇인가?
* git clone 명령은 자동으로 로컬의 master 브랜치가 리모트 저장소의 master 브랜치를 추적하도록 한다.
* git pull 명령은 clone 한 서버에서 데이터를 가져오고 그 데이터를 자동으로 현재 작업하는 코드와 merge 시킨다.
* git clone은 초기에 빈 프로젝트에 셋팅을 할때, git pull은 현재 디렉토리에서 업데이트 된 부분을 다운로드하려고 할때 만이 사용함
* 참고 : git에서 clone과 pull의 차이점 https://meaownworld.tistory.com/157


- git remote 를 한다는 것은 현재 폴더와 원격 레포지토리를 동기화 시키는건가 ?
* 등록만하는 것이다. git clone 같은 경우 자동으로 remote 초기 동기화 이후 remote 등록을 해주고, git pull 은 연결된 remote 레포에서 데이터를 가져오는 부분만 수행한다.


- Branch 과정의 이해 & checkout 과 init, remote 연결의 차이 & Fork 와 Clone 의 차이
* branch는 포인터이다.
* git branch <branch명> : 해당 레포의 master 브런치의 가장 최신본을 가르키는 브런치를 생성한다. 하지만, 단지 가져오기만 할뿐 git이 해당 브런치를 가리키진 않는다.
* git checkout <branch명> : 다른 브런치로 이동하는 기능, 브런치로 이동하면 워킹 디렉토리의 파일이 해당 브런치의 파일로 변경된다는 것을 기억 ! 만약에 충돌이 일어난다면 branch가 바뀌지 않는다.
* git merge <합칠 branch명> : 현재 브런치와 다른 브런치를 합치는 방법
* git pull 명령 은 두가지 명령을 합친 것이다.
    * git fetch <리모트명>
    * git merge <브런치명>

- git push 명령어
* git push <remote> <branch> : ex git push origin master


- colab에서 레포지토리를 포크하는 방법
- 스테이징 개념 : 3가지 스테이지
- git submodule 



공부하다보니 궁금 
- git의 되돌리기 기능 : 수강생의 파일을 되돌릴 필요가 있을 듯함
* 스테이지 되어 있는 파일을 스테이지에서 내릴 때 : git reset <파일명> 
- git log 와 관련된 사용 : 공부하기보단 실습하면서 배워야 할거같다. 
- git merge 충돌
- git rebase 와 git merge 의 차이


주니어로써 도움 드릴 수 있을 일

- 세션 1,2 의 colab의 git 사용과 , 세션 3의 git 사용의 차이를 알려주면 좋을거 같음
- 세션 1,2는 쉽게 사용하는 방법을 알려주고
- 세션 3에는 git의 이해와 깊은 사용에 대해서 안다고 보면 될거같음
- 왜냐하면 취업시장에서 git의 사용 및 이해에 대해 물어보는 사람들도 있음, 그러나 실제 프로젝트에서는 colab의 쉬운 방식을 이용하기도 하고 지금부터 배우는 방식을 사용하기도함 ..
-  엔지니어링에 가깝다면 git을 커맨드라인으로 많이 이용함
- 어떤걸 강의를 들어야하고, 어떤건 공부를 해야하는지 구분할 수 있게 된거같다. 
