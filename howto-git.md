
###
```
$ git clone [남의깃주소복사]  //아무것도 안하고 폴더다운됨 .처음만 
$ git fetch -p // 예전에 받았다면 다시 pull해서 동기화

$ git checkout [브런치이름] //해당폴더이동후 이런브렌치로 이동하면 로컬파일 변경
// npm install 해야?  
$ git checkout [다른브런치이름] //다른브런치 내용으로 로컬파일 변경됨.
$ git log 
//선생님이 마스터에 머지안하고 저 브런치에만 올려서. 브런치이동해야함  
$ git pull origin [브런치이름] //새로올렸음 다시받기 
```

```
git pull
git fetch -p
git branch
git checkout [브런치]
```

```
git status //빨간게나타나면 커밋할게 있음. 이러면 체크아웃안됨 
git branch

```

- git 소스트리    
- git blame 

## upstream 사용
남의repofork-> 나의repo에 클론-> 로컬과동기화-> 새브런치-> 내깃에올리고->내깃에서 new pull requeest 
upstream은 remote원격저장소에 이름붙인것.
master이외 브렌치를 만들어서(난안만듬) lacal내용을 변경. 내레포내용은 바뀌고 원본과확인-> pull request
<https://owl423.github.io/2017/05/08/github-upstream/>



## git 사이트에서 repositories 생성 
~~~
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/layna1124/[레포지토리네임].git
git push -u origin master
~~~

<hr>

## vscode에서 커밋후 한번에 올리기  
1. vscode 좌측 깃 init 버튼 ,레포지토리 초기화
2. 커밋 [c]+enter 한번에 add 설정 or 각각 
3. 좌측 소스제어버튼
4. U마크 : 언스테이지상태,  A : U에서 + 누르면 변경 하고 하나씩 커밋해서 변경
5. 설정따라 : 커밋만 누르면 unstaged된 상태를 전부 staged로 바뀜
6. 깃 사이트에서 레파지토리 등록 
7. vscode 터미널에서 git remote add origin 주소 
8. git push origin master 



<hr>

## git 공동작업 

문제1 - 서로 다른부분을 수정해서 push했다면 깃이 알아서 멋지 
같은 부분을 다르게 고쳤다면 깃은 어떻게 병합할지 몰라서 출동
해결1 - merge complete강제로 일으키고 풀기, 비쥬얼스튜디어코드에서 사람이 풀어야 


문제2 - 같은 master브런치에서 a,b가 작업 
커밋하면 푸쉬해서 원본저장소(upstream)저장해야되는데 
같은 master에서 계속 푸쉬하면 생기는 문제 : A가 먼저 푸쉬하면 b가 하면 꼬여, commit hisroty엉망진창

해결2 - branch를 기능별로 따로 만들기 
아무리 push하고 commit해도 괜찮아.
여러명이 push한걸 [pull request]날려서 master 브렌치에 병합시킨다.
프론트/백 이렇게 나누지 말고..
login기능 만들면 - login branch를 따서 - 뿌듯할때commit - push 


<hr>
- 커멘드라인 명령어 다 외워야되고..괜찮아몰라도 
- git 소스트리   
- git blame


## 오리진이름 다르게 하는거?

##
- git remote add pumpkin [포크뜬 원본주소]
- git push pumpkin master 하면 권한없으니까 안되고 
- git pull pumpkin master 를 주기적으로 해야함. 아니면 동료들에게 push했다고 말해야
- 안하면 complete 백개뜸. 들어가서 지워야되  
- compare&pull리퀘 날려 

- 포크뜬 레포는 내가 브렌치 어떻게 말들어쓰던 상관없는데 ,,기록은남아
- 보낼때는 해당브런치로 보내야 좋아 

- 디벨롭브런치에서 개발후 마스터 브런치와 멋지 
- git flow 
- 푸쉬 필요하다고 상태뜰것. 해주면되 


- 브렌치를 원본레포에서 기능별로 나눠놓고 해당기능에 푸쉬하고 주기적으로 풀받는방법


### git flow 
- git flow init 이거치니까 어느 브런치로 릴리즈하냐고 묻는데 
- 저장소 내에서 초기화하는 기능도있어?  브런치가 자동 만들어져?

- 
- git flow feature start


다가오는 배포(release)를 위한 새 기능(feature)을 개발
새 기능의 개발은 'develop' 브랜치에서 시작

git flow feature start MYFEATURE
이것은 'develop'에 기반한 새 기능(feature) 브랜치를 생성하고 
그 브랜치로 전환
기능 완료. 기능 개발을 완료

MYFEATURE 브랜치를 'develop'에 병합(merge)합니다.
기능 브랜치를 삭제합니다.
'develop' 브랜치로 전환합니다.
git flow feature finish MYFEATURE

릴리스를 시작하려면 git flow의 release 명령을 사용합니다.

'develop' 브랜치로부터 'release' 브랜치를 생성합니다.
git flow release start RELEASE [BASE]

피처스타트, 릴리즈 
깃풀펌킨마스터.
내컴퓨터가 origin 이 되는

---
## 혼자작업 upstream
<http://meetup.toast.com/posts/116>
- upstream : 메인 repository이다. 
- origin : repo를 자기 계정으로 fork한 repo이다. 
- clone : fork된 repo를 로컬로 clone한다. git clone [주소]
- git remote add upstream [주소] 하면 origin과 upstream 두개가 생긴다. 
- 최신내용을 로컬로 :  git pull --rebase upstream develop
- 저희는 Git Flow 전략에 따라, 기존 develop 브랜치로부터 새로운 개발 이슈에 해당하는 feature 브랜치를 만들어 작업하고 있습니다




---
## 깃용어
1. remote : 저장소 "http://github.com/username/000.git"
: 관련명령어 

---
# 0908

1. repo만들거나 쿨론해서 끌고오기

2. git flow
- 아래 브런치들 생김 
* develope : 다음릴리즈 개발중인 최신버전
: 여기병합, origin/develop`에서 관리, 최종 master`로 \'병합
* feature/ : 특정기능개발 
: 배포하려고 하는 기능을 개발하는 브랜치 feature/{branch-name} 형식
* release/ : 릴리즈 점검
* hotfix/ : 긴급버그픽스
* support/ : 버전호환성문제처리

* master

```
$ git flow init  // init 안되면 윈도우용 <>설치
//git flow init -d 엔터귀찮을때 
Which branch should be used for bringing forth production releases?
   - master
Branch name for production releases: [master]
Branch name for "next release" development: [develop]

How to name your supporting branch prefixes?
Feature branches? [feature/]
Bugfix branches? [bugfix/]
Release branches? [release/]
Hotfix branches? [hotfix/]
Support branches? [support/]
Version tag prefix? []
Hooks and filters directory? [C:/Users/Layna/documents/dev/gittest/.git/hooks]
```
> 2개만써도되 <https://ujuc.github.io/2015/12/16/git-flow-github-flow-gitlab-flow/>


3.push하면 사이트에도 branch:master가 생김  
```
Layna@LaynaPC MINGW64 ~/documents/dev/gittest (develop)
$ git push origin develop

```

4. 기능브런치 만들기 
```
$ git flow feature start <브런치이름>
Switched to a new branch 'feature/login'
...
~/documents/dev/gittest (feature/login)

```
이렇게 하면 새로운 기능 개발을 위한 branch가 “feature/기능명”이라는 이름으로 만들어지고, 해당 branch로 자동으로 checkout 된다.

4-2. 내용을 푸쉬해아한다.
사이트에 feature/기능명 으로  브런치 생성되있음.


5. 기능브런치 머지시키고 삭제
```
$ git flow feature finish  <branch name>
```
- git flow는 develop branch로 checkout 한 후,
feature branch의 변경 내용을 자동으로 develop branch에 merge하고,
작업이 끝난 feature branch를 삭제한다.

- 멋지안되는데?
같은거 고쳐서 충돌인가. 상위 브런치로 가서...병합해야하나봄

```
Layna@LaynaPC MINGW64 ~/documents/dev/gittest (develop|MERGING)
// 아래거 치면 
$ git merge --abort
// 돌아옴 
Layna@LaynaPC MINGW64 ~/documents/dev/gittest (develop)

```
6. 같은거고쳤을때 멋지 다시시도 




# 쉬운설명 git flow
<http://huns.me/development/1131>


<hr>

# git clone 일반 