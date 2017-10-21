#node설치
#npm(노드패키지관리자) v8에서 노드써도 되지만 관련 라이브러리들을 관리하게 편하도록


# 노드설치
윈도우
<https://github.com/coreybutler/nvm-windows>
Download the latest installer from the releases. 
<https://github.com/coreybutler/nvm-windows/releases>
nvm-setup.zip 다운설치 후 터미널재실행 
```
$ nvm install 8.4
$ nvm use 8.4
$ nvm alias default 8.4 (# nvm-windows는 필요없음)
```
npm install -g로 깔았던게 6.11.x버전으로 종속이됨
지금 8.4로 깔아서 이전꺼못씀.  
원래 깔았던 버전으로 돌아가기 
```
$ nvm ls  설치한목록뜸 (6.11.1)등 
$ nvm use 이전버전 
$ node
> 꺽쇠뒤에 자바스크립트 코드 입력
> .exit 나가기 
```

## 윈도우 포트차지 문제해결 
(특히 윈도우에서) 종료된 Node.js 프로그램이 포트를 차지하고 있는 문제에 대한 해결 
<https://www.npmjs.com/package/cross-port-killer>

<hr>

# npm
Node.js 패키지 관리 도구 + 클라우드 패키지 저장소
- 의존 패키지 관리 / 스크립트 실행 / 패키지 설정
- NPM에 패키지 배포 / Node.js 종합 작업 도구 /
- node package manager : 모듈 관리(설치, 업데이트, 삭제 등)하기위한 매니저 
- npm으로 외부 모듈 설치 : node_modules 디렉토리에 저장, 우리가 설치한 외부 모듈이 의존 모듈까지 같이 설치함
- node_modules는 따로 git 버젼 관리하지않음 : index.js 만 있으면 바로 실행 x, 사용하는 모듈 설치해야함
- 요즘엔 페이스북에서 만든 yarn 이라는 패키지 매니저도 있음 : https://yarnpkg.com/lang/en/


## npm, package.json으로 쉽게 모듈 설치하기
1) npm init : package.json 생성 - 프로젝트 의존 모듈 관리(사용 모듈 네임, 버젼), 프로젝트 정보
2) npm install 모듈명 --save : 모듈설치시 --save 옵션을 주면 package.json에 자동 등록
~~~
$ npm init -y   //pacage.json파일생성  모두yes
$ npm install --save express
$ npm start  //package.json추가 
$ code .        //vs열림 
~~~

## package.json
그냥 install 하면 ./node_modules 디렉터리에 패키지 설치를 하고 끝.   
--save, --save-dev 옵션은 ./package.json 업데이트를 같이해준다.  
 어디에 패키지 정보를 추가하느냐가 다른데, --save 옵션은 dependencies object에 추가하고 --save-dev 옵션은 devDepenencies object에 추가한다.
차이는 npm install을 할 때 나타난다.  
dependencies는 항상 설치되고,     
devDepenencies는 --production 옵션을 붙이면 빠진다. npm install “$package” 명령어로 설치할 때는 --dev 옵션을 붙여야지만 설치된다.


## nodemon
자동서버실행 
윈도우안되 


<hr>


## ejs에서 eslint쓰기 
```
"emmet.showExpandedAbbreviation": "always",
"emmet.includeLanguages": {
	"javascript": "html"
},
"emmet.triggerExpansionOnTab": true,
```

#  --save와 --save-dev차이?

그냥 install 하면 ./node_modules 디렉터리에 패키지 설치를 하고 끝. --save, --save-dev 옵션은 ./package.json 업데이트를 같이해준다. 어디에 패키지 정보를 추가하느냐가 다른데, --save 옵션은 dependencies object에 추가하고 --save-dev 옵션은 devDepenencies object에 추가한다.

dependencies와 devDepenencies 차이는 npm install을 할 때 나타난다. dependencies는 항상 설치되고 devDepenencies는 --production 옵션을 붙이면 빠진다. npm install “$package” 명령어로 설치할 때는 --dev 옵션을 붙여야지만 설치