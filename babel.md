
# babel 설치 
<http://poiemaweb.com/es6-babel>

충돌안나게 로컬로 
~~~
$ mkdir babel-project && cd babel-project
$ npm init -y
$ npm install babel-cli --save-dev
~~~

packge.json 내용변경 
~~~
{
  "name": "babel-project",
  "version": "1.0.0",
  "devDependencies": {
    "babel-cli": "^6.26.0"
  }
}
~~~


명령어를 실행
~~~
$ npm install babel-preset-env --save-dev
~~~ 

.babelrc 파일을 생성하고 아래내용 입력
~~~
{
  "presets": ["env"]
}
~~~

다시 package.json파일을 아래처럼 수정   
npm scripts를 사용하여 트랜스파일링 하는법       
Babel CLI 명령어도 있음 <https://babeljs.io/docs/usage/cli/>
~~~
{
  "name": "babel-project",
  "version": "1.0.0",
  "scripts": {
    "build": "babel src/js -w -d dist/js"  
  },
  "devDependencies": {
    "babel-cli": "^6.26.0",
    "babel-preset-env": "^1.6.0"
  }
}
~~~ 
바벨폴더안에 src/js 폴더만들면  dist/js폴더는 자동생성되어서 결과물을 담는다   
w 감시하겠다  d 자동변경실행   

src/js 폴더를 생성한 후  main.js와 lib.js를 추가한다.[es6문법]  
~~~
$ npm run build
~~~
스크립트 이름이 build
실행하면 dist폴더에 es5문법으로 변환된 js파일들을 확인한다. 


문제없이 실행된것처럼 보이지만 node.js에서 실행된것뿐 
브라우저에서 쓰려면 webpack를 써야한다. 

<br>

# webpack
브라우저에서 모듈을 불러올수있는기능  
번들러(여러파일을 하나로 묶음)  
es6뿐 아니라 sass처럼 css로 컴파일 해야하는것도 webpack에서 한번에 자동화 
설정이 약간 어려움

작업폴더 
~~~
npm install webpack --save-dev
~~~

--save-dev는 개발환경용으로 설치라는 의미 
package.json파일에 "devDependencies": {내용}에 webpack이 추가.
배포할때는 필요없는 부분

~~~
$ npm install babel-loader --save-dev
~~~

package.json script변경 
~~~
{
  "name": "babel-project",
  "version": "1.0.0",
  "scripts": {
    "build": "webpack -w"
  },
  "devDependencies": {
    "babel-cli": "^6.26.0",
    "babel-loader": "^7.1.2",
    "babel-preset-env": "^1.6.0",
    "webpack": "^3.5.5"
  }
}
~~~

설정파일 webpack.config.js를 생성하고 아래내용 입력 
~~~
var path = require('path');

module.exports = {
  entry: {
    entry: './src/js/entry.js'   //실제 동작파일  
  },
  output: {
    filename: 'bundle.js',       //bundle.js 로 최종결과물 만들것, html에서 이것만 링크  
    path: path.resolve(__dirname, 'dist/js')
  },
  module: {
    rules: [{
      test: /\.js$/,   //모든 js파일을 
      include: [
        path.resolve(__dirname, 'src/js')  //src의 js안에 있는 파일 
      ],
      exclude: /node_modules/,
      use: {                       
        loader: 'babel-loader',   //바벨로더로 바벨을 call
        options: {
          presets: ['env']
        }
      }
    }]
  },
  devtool: 'source-map'
};
~~~

webpack을 사용하여 번들링을 실행한다. 이때 Babel 또한 실행
~~~
npm run build
~~~

브라우저는 require못읽어 

src의 js파일들이 dist js폴더에(바벨), 파일들이 합쳐서 bundle.js만들어짐(웹팩) 
html에서 스크립트 경로 bundle.js만 연결하면 실행


