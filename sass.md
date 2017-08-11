#SASS

- js아니고 루비로 만들어짐 : ruby sass  
- Node.js 환경에서 사용가능 컴버전 된것 : node sass (업데이트 시간차 있을수있음)
- css의 한계극복, 유지보수 변수.함수.확장,상속 등의 기능추가  
- Sass의 표기법은 SASS(.sass)와 SCSS(.scss 기본)가 있다. 
- 브라우저는 css문법 밖에 모르므로 sass를 css로 변환해야 한다.

> less : js로 구동 , 브라우저단에서 고장 
> scss : css동일한 문법으로 기능추가


> ## npm설치
~~~
 $ npm install -g node-sass 
 $ node-sass -v 
~~~ 

- my-project 폴더 > src > sass 폴더 생성  
- vscode의 해당 프로젝트 파일열기
- vscode안의 터미널 [c]+~ 열기 
~~~
$ cd my-project 
$ node-sass src/sass --output dist/css 
~~~
- 프로젝트폴더 > dist > css 폴더가 생성)
- ※ dist : 배포용

~~~
//파일단위
$ node-sass --watch src/sass/main.scss --output dist/css
//폴더
$ node-sass --watch src/sass --output dist/css
~~~
- scss 파일의 변경을 감지하여 컴파일 css 파일을 자동 업데이트 
- webpack 쓰면 더 간단하다 


## 문법  

- 프로퍼티값으로 사용할 수 있는 값

1. 숫자형
2. 문자열 : "", 사용하지 안는문자열 
3. 컬러   : e.g. true, false
4. boolean : e.g. true, false
5. null
6. list : 공백 또는 콤마 구분된 값
7. map  : JSON과 유사방식 map-get 함수로 원하는 값 추출

- 변수명 $ 
- scope 존재 , 코드블럭
~~~
// 지역변수 전역변수 전환방법  
#main {
  $color: #333 !global; // global variable
  width: $width;
  ...
~~~


- 동일단위 연산만 가능
~~~
$width: 100px;
#foo {
  width: 5% + 10%; // 15%
  width: $width + 10em; // NG
}
~~~

- CSS3의 calc 함수(IE9이상)를 사용하면 가능  
~~~
#foo {
  width: calc(25% - 5px);
}
~~~

### 여러가지 예
~~~
p {
  // 타원형 둥근 모서리
  border-radius: 10px 20px / 20px;
  
  // 나누기연산 
  $width: 1000px;
  width: $width / 2;

  //함께사용 
  $font-size: 12px;
  $line-height: 30px;
  font: #{$font-size} / #{$line-height};  // 12px/30px

  ...
  }
~~~

> 컬러연산 
~~~
p {
  color: rgba(255, 0, 0, 0.75) + rgba(0, 255, 0, 0.75);
  // alpha 값은 연산안됨 , opacify 함수 또는 transparentize 함수사용

}
~~~

- 문자열 연산 : + 가능 
- 불린연산 : && || ! 


> Interpolation : #{}}
: 프로퍼티값 물론 셀렉터와 프로퍼티명에 사용

~~~
$name: foo;
$attr: border;

p.#{$name} {            // p.foo
  #{$attr}-color: blue; // border-color: blue;
}
~~~

> Ampersand(&)
: 부모요소를 참조하는 셀렉터
~~~
a {
  color: #ccc;

  &.home {
    color: #f0f;
  }
}  
~~~
~~~
//컴파일결과
a.home {
  color: #f0f;
}
~~~

> !default
: 할당되지 않은 변수의 초기값 설정
~~~
// font.scss
$font-size: 16px !default;
$line-height: 1.5 !default;
$font-family: "Helvetica Neue", "Helvetica", "Arial", sans-serif !default;

body {
  font: #{$font-size}/$line-height $font-family;
}
// main.scss
$font-family: "Lucida Grande", "Lucida Sans Unicode", sans-serif;

@import "font";
~~~
이럴때 유용할듯!



@import

분할된 파일을 partial라함. Sass 파일명의 선두에는 underscore(_)를 붙인다. 
(_reset.scss, _module.scss, _print.scss)

~~~
@import "foo.scss";

// 확장자는 생략 가능하다
@import "foo";

// import multiple files
@import "rounded-corners", "text-shadow";

$family: unquote("Droid+Sans");
@import url("http://fonts.googleapis.com/css?family=#{$family}");
~~~


컴파일단축 <https://github.com/mitoolab/TIL/blob/master/CSS/sass-package.json.md>

참고링크  <http://poiemaweb.com/sass-built-in-function>

