# Built-in Object  
자바스크립트가 제공하는  내장객체
웹페이지가 브라우저에 의해 로드되자마자 행위없이 바로 사용

Object 구성 
  - Host Object : 우리가만든것
  - Built-in Object 
    + Standard Built in object 표준빌트인 객체
    + Native Object
      - Bom  
      - Dom
![](http://www.poiemaweb.com/img/object.png)

> Bom : browser object model. 
        window: 현재 브라우저 창
          document : 현재 로드된 웹페이지 
          history : 브라우저 히스토리에 기록된 웹페이지들 
          location : 현재 페이지 url
          navigator : 브라우저관련정보
          screen : 장치의 디스플레이 정보 
          
> Dom : document객체로 전체문서표현 

<hr>
<br><br>


# 표준빌트인객체 
Standard Built in object (global objets)
전역객체의 프로퍼티


## 전역객체 (global objet)
브라우저(Browser-side)에서 전역객체는 윈도우 
노드(Server-side)에서는 전역객체를 의미  

## 전역프로퍼티 
> infinity 

자바스크립트는 8바이트를 갖고표현? 
표현할수있는 수의 한계가있다.
MAX_VALUE 자바스크립트에서 표현하루있는 가장큰수 
~~~
console.log(3/0);  // Infinity   3을 0으로 나누면 무한대
console.log(-3/0); // -Infinity  -3을0으로 나누면 음의무한대
console.log(Number.MAX_VALUE * 2);  //한계를 넘기때문에 Infinity 
console.log(typeof Infinity); // number. Infinity 도 타입number
~~~ 

> NaN
숫자가 아닐때.
형변환 하려고 하지만 안 될때 
~~~
console.log(Number('xyz')); // NaN  문자열을 숫자로 형변환하려고 하지만 
console.log(1 * 'string');  // NaN
console.log(typeof NaN);    // number
~~~ 


## 전역함수 

> eval()    

문자연산 하지만 사용금지. 사용자로 부터 입력받은게 보안상 문제될수

> isFinite()

유한수인가? = infinity가 아닌지를 체크 
숫자가 아닌것을 주면 false
~~~
//상태를 난타냄 is
console.log(isFinite(Infinity));  // false

console.log(isFinite(null));      // true: null->0
// null널은 기본으로 형변환하려함. 0은 유한수이므로 true가 나옴 
~~~

> isNaN()  

NaN 이냐?
매개변수로 전달될값이 NaN인지 검사 true false로 반환
숫자가 아닌닐땐 변환후 검사
~~~
isNaN(NaN)       // true
isNaN(undefined) // true: undefined -> NaN
isNaN({})        // true: {} -> NaN
isNaN('blabla')  // true: 'blabla' -> NaN

isNaN(true)      // false: true -> 1 로인식. 숫자니까
isNaN(null)      // false: null -> 0 
isNaN(37)        // false
isNaN('')        // false: '' -> 0  빈문자
isNaN(' ')       // false: ' ' -> 0 스페이스 
//date
isNaN(new Date())             // false: new Date() -> Number
isNaN(new Date().toString())  // true:  String -> NaN
~~~

  try{
    foo();
  }catch(e){
    //e에 레퍼런스에러넣어서 ..404로 간다던지 
  } 

> parseFloat() : 소수점까지 , 첫 숫자만 반환
~~~
parseFloat('3.14');     // 3.14
parseFloat('10.00');    // 10 정수로 
parseFloat('34 45 66'); // 34 앞에수자변환
parseFloat(' 60 ');     // 60 스페이스 무시 
~~~

> parseInt() : 정수로 변환 

> encodeURI()  

: 매개변수로 전달된 URI를 인코딩 

![](http://www.poiemaweb.com/img/uri.png)

- 인코딩: uri문자들을 이스케이프 처리하는것 
이스케이프 처리: 네트워크를 통해 정보를 공유할 때 어떤 시스템에서도 읽을 수 있는 ASCII 아스키코드로 변환하는 것
- UTF-8 특수문자의 경우, 1문자당 1~3byte, UTF-8 한글 표현의 경우, 1문자당 3btye이다. 예를 들어 특수문자 공백(space)은	%20, 한글 ‘가’는 %EC%9E%90으로 인코딩된다.
- 알파벳, 0~9의 숫자, - _ . ! ~ * ‘ ( )는 이스케이프처리에서 제외


# 표준빌트인 객체

## 기본자료형 Number를 위한 레퍼객체
기본자료형이 wrapper객체의 메소드를 사용할수 있는 이유?
기본자료형으로 프로퍼티나 메소드를 호출할때  기본자료형과 연관된 wrapper객체로 일시적으로 변환, 프로포타입 객체를 공유하기 때문

### Number 생산자 

### Number 속성 
객체생성 안해도 Number.propertyName 으로사용 

> Number.EPSILON : 가장작은수. 미세한 오차
연산이 Number.EPSILON보다 작으면 같은 수로 인정

> Number.MAX_VALUE : MIN_VALUE 다 큰 숫자 infinity

> Number.MIN_VALUE

> Number.POSITIVE_INFINITY : 양의무한대  Infinity를 반환. 아니면 undifined

### Number 함수 
전역함수 isFinite()는 인수를 숫자로 변환 
Number.isFinite()는 인수를 *형변환 안하므로* 
유한수 아니면 무조근 false 

> Number.isInteger() : 인자 정수인지 boolean

> Number.isNaN() : 

> Number.isSafeInteger() : 

> Number.prototype.toExponential() :

> Number.prototype.toFixed() : 소수점 이하자리를 반올림 문자열로  
~~~
//인자 안줄수도 있어
numObj.toFixed();       // '12346': 소수점 이하를 반올림
numObj.toFixed(1);      // '12345.7' : 소수점 1자리를 유지한 상태로 반올림 
numObj.toFixed(6);      // '12345.678900' : 없으면 6자리까지 0채움 
~~~

> Number.prototype.toPrecision() : 전체 자릿수 지정 

> Number.prototype.toString()  : 숫자를 문자열로 

> Number.prototype.valueOf() : Number 객체의 기본자료형 값


## Math

상수: 변하지안는수 

Math는 생성자 함수 아님 = 일반객체= 프로토타입없음 

> Math.PI : 파이값 

> Math.abs() : 절대값반환, 숫자아니면 NaN

> Math.round() : 반올림처리 

> Math.sqrt() : 루트 

> Math.ceil() : 정수로 올림

> Math.floor() : 정수로내림

> Math.random() 

> Math.pow() : 첫째인수를 두번째인수로 제곱  

> Math.max() : 숫자중 가장 최대수 

~~~
Math.max( 1, 2, 3 );  // 3

// apply 호출패턴
var arr = [1, 2, 3];
var max = Math.max.apply(null, arr); // 3

// ES6 
// 스프레드 연산자...를 쓰면 복사    
var max = Math.max(...arr); // 3
~~~

> Math.min() : 가장최소수


## Date

Date객체는 날짜와 시간제공 메서드 
라이브러리 많음 


날짜와 시간을 가지는 Date 객체의 생성자 종류 
~~~
Date() // 현재날짜 
Date(0) 1970년 1월1일0시0부0초
Date(dateString)
Date(2000, 11, 25)
Date("mm dd, yyyy hh:mi:ss")
Date(year, month[, day, hour, minute, second, millisecond])
~~~

Data Object가 생성되면 내장함수들을 get과 set을 붙여서 사용가능
~~~
//2010-01-14를 세팅할때
var myDate=new Date();
myDate.setFullYear(2010,0,14);
// 5일 후를 세팅
var myDate=new Date();
myDate.setDate(myDate.getDate()+5);
~~~


new 연산자없이 사용하면 결과값을 문자열로반환

===

> 요일구하기(문제)

2016년 1월1일은 금요일이다. 2016년 a월 b일은 무슨 요일일까?
두수 a,b를 입력받아서 a월 b일이 무슨 요일인지 출력하는
getDayName함수를 완성하세요.
요일의 이름은 일요일부터 토요일까지 각각 SUN,MON,TUE,WED,THU,FRI,SAT
를 출력한다. 예를 들어 a=5, b=24가 입력된다면 5월 24일은 화요일이므로 TUE를 반환한다.

funtion getDayname(a,b){
}
console.log(getDayName(5,24)); // tue

<br>
---

# String

String 객체는 기본자료형인 string을 다룰 때 유용한 프로퍼티와 메소드를 제공하는 레퍼(wrapper) 객체. 변수 또는 객체 프로퍼티가 문자열을 값으로 가지고 있다면 String 객체의 별도 생성없이 String 객체의 프로퍼티와 메소드를 사용.

- String 객체는 String() 생성자 함수를 통해 생성
- new 연산자를 사용 안하고 String() 생성자 함수를 호출하면 String 객체가 아닌 문자열 리터럴을 반환
- 일반적으로 문자열를 쓸때는 기본자료형의 문자열 사용
- 매개변수로 전달한 index 번호에 해당하는 위치의 문자를 반환 
- index 번호는 0 ~ (문자열 길이 - 1) 사이의 정수
~~~
var str = 'Hello';

console.log(str.charAt(0)); // H
console.log(str.charAt(1)); // e
console.log(str.charAt(2)); // l
console.log(str.charAt(3)); // l
console.log(str.charAt(4)); // o
// 지정한 index가 범위(0 ~ str.length-1)를 벗어난 경우 빈문자열을 반환한다.
console.log(str.charAt(5)); // ''

for (var i = 0; i < str.length; i++) {
  console.log(str.charAt(i));
}
~~~
- 유사배열객체이므로 for문으로 돌릴수있다.
- 문자열찾고 반환하기

~~~
str.indexOf(searchValue[, fromIndex])
// searchValue: 검색할 문자 또는 문자열
// fromIndex : 검색 시작 index (생략할 경우, 0)

var str = 'Hello World';

console.log(str.indexOf('l'));  // 2
console.log(str.indexOf('or')); // 7
console.log(str.indexOf('or' , 8)); // -1
~~~

~~~
var str = 'Hello Hello'; //기본자료형은 안변함 
var replacedStr = str.replace('Hello', 'Lee');
console.log(replacedStr);
console.log(str);

// 정규표현식
replacedStr = str.replace(/hello/gi, 'Lee'); 
console.log(replacedStr);
console.log(str);
~~~


> str.split([separator[, limit]])
~~~
str.split([separator[, limit]])
// separator: 구분 대상 문자열 또는 정규표현식
// limit: 구분 대상수의 한계를 나타내는 정수
~~~
문자열을 구분한 후 배열로 반환 

> String.prototype.substring(): 문자반환 

- str.substring(indexA[, indexB])ㅣ
- 첫번째인수 > 두번째인수 : 교환됨 
- 두번째 인수생략 : 첫번째인수값 빼고 전부반환 
- 인수 < 0 또는 NaN인경우 : 0취급 전부반환
- 인수 > 문자열길이(str.length) : 

> String.prototype.toLowerCase() : 모두소문자 

> String.prototype.toUpperCase() : 모두대문자 


# Array
배열은 1개의 변수에 여러값을 저장할때 사용 
Array객체는 다양한 내장 메소드를 갖고있다.(e.g.sort)

## 배열의 생성

1. 배열리터럴

인덱스 0부터 
값을 쉼표로 구분하여 대괄호 []로 묶는다.

~~~
//배열리터럴
var emptyArr = [];
var numbersArr = [
  'zero', 'one', 'two', 'three', 'four'
];

//객체리터럴
var numbersObject = {
  '0': 'zero',  '1': 'one',   '2': 'two',
  '3': 'three', '4': 'four'
}
~~~
변수리터럴과 달리 프로퍼티명이 없고 값만존재한다.
~~~
var emptyArr = [];
var emptyObj = {};

console.dir(emptyArr.__proto__);
console.dir(emptyObj.__proto__);
~~~
numbersArr는 Array의 프로토타입을 상속받고
numberObj는 Object의 프로토타입을 상속

[]안에 데이터타입이 다를수있다.

배열리터럴은 결국 내장함수 Array() 생성자함수로 단순화시킨것
Array.prototype.constructor 프로퍼티로 접근가능
~~~
//매개변수 1개이고 숫자일때
new Array(arrayLength)

//매개변수로 전달된 숫자를 length 값으로 가지는 빈 배열 생성
var arr = new Array(2);
console.log(arr.length, arr); // 2 [undefined, undefined]
//그외
new Array(element0, element1[, ...[, elementN]])

//매개변수로 전달된 값을 요소로 갖는 배열 생성
var arr = new Array(1, 2, 3);
console.log(arr.length, arr); // 3 [1, 2, 3]
~~~

2. 배열요소추가

순서없이 필요한 인덱스 위치에 값을 저장
~~~
var arr = [];
console.log(arr[0]); // undefined

arr[0] = 'one';
arr[3] = 'three';
arr[7] = 'seven';

console.log(arr); // ["one", undefined × 2, "three", undefined × 3, "seven"]
~~~

3. 배열요소삭제 

delete 요소값만삭제 
Array.prototype.slice() 요소까지 삭제
console.log(checkPalindrom(''));



# 정규표현식 
자바스크립트가 아니고 다른 언어 (js는 함수만 제공)
문자열에서 특정 내용을 찾거나 대체 또는 발췌할때  
이메일 형식체크 등 유저의 입력값 체크할때 유용 
반복문과 조건문으로 구현가능하지만 간단히 처리
가독성 나쁨 
~~~
var tel = '0101234567팔';
var myRegExp = /^[0-9]+$/;
console.log(myRegExp.test(tel)); // false
~~~

- test라는 함수 조건부합하는지 true false 반환 

정규표현식을 변수에 할당하면 정규표현식객체가 만들어지고
함수로 호출하면됨.

~~~
var myRegExp = /regexr/ig;
~~~
/regexr/ 이안의단어를 
i 대소문자 구별말고 
g 모두찾아라 
m 행이바껴도 검색 

match
test 있는지 없는지만 찾아 
. 은 임의의 문자 한개 

~~~
var targetStr = 'AA BB Aa Bb';
// 임의의 문자 3개
var regexr = /.../;

console.log(targetStr.match(regexr)); // 'AA '  스페이스포함3개 
~~~

자주쓰는
~~~
// abc로 시작하는가  
var targetStr = 'abcdef';
var regexr = /^abc/;
console.log(regexr.test(targetStr)); // true
~~~
~~~
// 모두 숫자인지 검사
var targetStr = '12345';
var regexr = /^\d+$/;
console.log(regexr.test(targetStr)); // true
~~~
~~~
// 알파벳 대소문자 또는 숫자로 시작하고 끝나며 4 ~10자리인지 검사 
var targetStr = 'abc123';
var regexr = /^[A-Za-z0-9]{4,10}$/
console.log(regexr.test(targetStr)); // true
~~~
~~~
// 특수문자 포함여부 
var targetStr = 'abc#123';
var regexr = /[\{\}\[\]\/?.,;:|\)*~`!^\-_+<>@\#$%&\\\=\(\'\"]/gi
console.log(regexr.test(targetStr)); // true
~~~

