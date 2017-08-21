**ECMAScript6**
===

es5에서는  
변수선언은 var키워드 사용하는데 var키워드 생략시 전역변수화      
중복선언 허용     
변수호이스팅(변수선언 전에 참조)     


변수의 스코프는 좁을수록 좋다
자바스크립트가 길어지면서 전역변수 문제가 커짐
IIFE나 모듈패턴을 사용해도 되지만 
ES6는 let과 const 키워드를 도입하였다. 


# let 

- Block-level scope를 갖는 변수를 선언  
모든 블럭을 유효범위로 인식   
코드 블럭 외부에서는 참조할 수 없다    

{} 중괄호, 코드블럭:  다른 c언어들의 유효범휘  
{} 이안에서만 유효한 변수를 만들려는 의도였으나, js에서는 전역이됨 
~~~
{
  var foo = 456; //이중선언된것  
}
~~~

- 중복선언을 하면 syntaxError : 문법에러 

- 호이스팅을 안하는 것처럼 동작한다 ?   
: 선언과 초기화단계가 한번에 이뤄지지않기 때문. 선언단계(메모리할당안해)와 초기화단계 (foo==undefined)사이의 일시적 사각지대에 들어와 있기때문에 에러처리. 그냥 호이스팅 안된다고 봐도 무방하다.  
eslint에서 var변수 위에쓰라고 빨간줄에러 날것 


- let은 for문의 경우 클로저를 안써도 된다. 

기존의 클로저 사용 
~~~
var funcs = [];

// 함수의 배열을 생성
// i는 전역 변수
for (var i = 0; i < 3; i++) {
  (function (index) { // index는 자유변수
    funcs.push(function () { console.log(index); });//클로저위해 내부함수를 작성 
  }(i));
}

// 배열에서 함수를 꺼내어 호출
for (var j = 0; j < 3; j++) {
  funcs[j]();  //0,1,2출력 살아남음 
}
~~~
push 배열뒤쪽에 넣기. 클로저를 만들고자 하는 지역에 일단 즉시실행함수를 만든다. 매개변수는 지역변수와 동일한것.
function(index) 쓰면 var=index한것도 같은것
이안에 function() 이 내부함수는 외부에서도 쓰기때문에
더 오래 살아남음. 

클로저를 쓰지않고 let을 이용하기
~~~
var funcs = [];

// 함수의 배열을 생성
// i는 for loop에서만 유효한 지역변수이면서 자유변수
for (let i = 0; i < 3; i++) {
  funcs.push(function () { console.log(i); });
}

// 배열에서 함수를 꺼내어 호출
for (var j = 0; j < 3; j++) {
  funcs[j]();
}
~~~

for loop의 let i는 for loop에서만 유효한 지역 변수이다.
 i는 자유변수로서 for loop의 생명주기가 종료하여도 변수 i를 참조하는 함수가 존재하는 한 계속 유지된다.(실행컨텍스트)



- 전역객체와 let 


# const 

- 상수(변치안는수)위해 사용
- 선언과 동시에 할당해줘야한다.
- 재할당이 안된다. 그러나 프로퍼티 변경가능
~~~
// 알아보기어려워 
if (x > 10) {
}

// 이해가 빠르고 유지보수 쉬워 
// "게시판 10개에서 ->  20개로 바꿔"  
const MAXROWS = 10;
if (x > MAXROWS) {
}
~~~

객체 타입 변수 선언에는 const를 사용하는것이 좋다.
~~~
const user = {
  name: 'Lee',
  address: {
    city: 'Seoul'
  }
};
~~~
위처럼 할당해준 객체는 변경될 일이 별로 없기 때문.  
필요할땐 새로운 const user1객체를 만듬.


## ES6를 사용한다면 

- var 키워드는 사용하지 않는다.
- 재할당이 필요한 primitive형 변수에는 let를 사용한다.
- 변경이 발생하지 않는(재할당이 필요없는) primitive형 변수와 객체형 변수에는 const를 사용한다. 


## 탬플릿 문자열(리터럴)

통상적으로 
자바스크립트는 ''  
json html css 는 ""  
es6에서 문자열은  ``백틱 사용    

- 띄어쓰기 : 백슬래시(\)
- ${expression} : 템플릿 대입문에는 문자열뿐만 아니라 표현식(하나의값으로 수렴되는식)도 사용할 수 있다.
~~~
console.log(`1 + 1 = ${1 + 1}`); // 1 + 1 = 2
const name = 'ungmo';

console.log(`Hello ${name.toUpperCase()}`); 
~~~

## Arrow 함수 

function 키워드대신 화살표(=>)로 함수선언 
~~~
// 매개변수 지정 방법
    () => { ... } // 매개변수가 없을 경우
     x => { ... } // 매개변수가 한개인 경우, 소괄호를 생략가능 
(x, y) => { ... } // 매개변수가 여러개인 경우

// 함수 몸체 지정 방법
x => { return x * x }  // single line block
x => x * x             // 함수 몸체가 한줄의 표현식이라면 중괄호를 생략할 수 있으며 자동으로 return된다. 위 표현과 동일하다.

() => { return { a: 1 }; }
() => ({ a: 1 })  // 위 표현과 동일하다. 객체 반환시 소괄호를 사용한다.

() => {           // multi line block.
  const x = 10;
  return x * x;
};
~~~
return문 안써도 한줄짜리 기본 리턴함 

- Arrow 함수는 익명함수로만 사용 (no 기명함수)
- 함수선언식 만들수 없으니까 호출하기 위해서 함수표현식 사용 
- arrow 함수는 한줄정도의 짧은 함수만들때 사용
- 주로 콜백함수에 사용 (일반적인 함수 표현식보다 표현이 간결)


### Arrow 함수를 쓰는경우
인자의 수가 몇개인지 알수없는 경우의 함수(=가변인자함수)를 쓸때 

기존
~~~
  var array = Array.prototype.slice.call(arguments);
~~~
매개변수 갯수가 확정되지 않은 가변 인자 함수를 구현할 때 arguments 객체사용. 가변 인자 함수의 경우, 파라미터를 통해 인수를 전달받는 것이 불가능하므로 arguments 객체를 활용. 하지만 arguments 객체는 유사배열 객체이기 때문에 배열 메소드를 사용하려면
Function.prototype.call, Function.prototype.apply를 사용하여야 하는 번거로움이 있다.
(배열이 아닌데 slice()는 배열에대한 함수 그래서 array 붙임)
prototype.slice.여기까지가 매서드고 이걸 call 해라라는 뜻 

- ES6의 Arrow function에는 함수 객체의 arguments 프로퍼티가 없다. 참조할 필요가 없다는 뜻.
~~~
var es5 = function () {};
console.log(es5.hasOwnProperty('arguments')); // true

const es6 = () => {};
console.log(es6.hasOwnProperty('arguments')); // false
~~~
es5.hasOwnProperty:뒤에준 이름의 프로퍼티가 있는가?
es6에는 없다고 나옴
(...args) 쓰면 배열로 집어넣음  이것을rest파라미터라고함 
~~~
/ ES6
const sum = (...args) => {
  // console.log(arguments); // Uncaught ReferenceError: arguments is not defined
  console.log(Array.isArray(args)); // true

  return args.reduce((pre, cur) => pre + cur);
};

console.log(sum(1, 2, 3, 4, 5)); // 15
~~~


 this는 

 생성자 함수의 this (new와 함께 사용됫을때 선두에서는 참조하는값을 빈객체로 만들어주고 프로퍼티를 셋하고 말미에는 리턴해주는 두가지 일함)과  
 new가 없는 일반함수 에서의 this= window 였는데 

 arrow함수 에서는
 자신만의 this를 생성하지 않고 자신을 포함하고 있는 컨텍스트로 부터 this를 계승 받는다



### 콜백함수의 this의 문제점 

콜백함수 내부의 this가 메소드를 호출한 객체(생성자 함수의 인스턴스)를 가리키게 하기 위해서 해결법. 

지금 콜백함수내 this가 다르니까 

(1) this = that   
that변수쓰기   
(2) map(func, this) 두번째인자   
(3) bind   
bind는 모든함수들이 부를수있어 function prototype이므로 
바인드함수 명시적으로 호출
map에서 적절치안음  

(4) es6에서  Lexical this  
Arrow function은 자신만의 this를 생성하지 않고 자신을 포함하고 있는 컨텍스트로 부터 this를 받음.   
Arrow Function은 콜백함수내에 this가 다르게 
부르는것을 막기 위해 쓰는것으로 애초에 나온것.

※ react 와 node써도 es5써도 되는데 angular는 es6써야함 

## 기본파라미터 초기값 
체크 및 초기화를 간편화
x, y에 인수가 할당되지 않으면 초기값 0이 할당된다.

## rest파라미터 
하나 이상의 파라미터를 묶습니다.
넘겨 받은 배열 [1, 2, 3, 4, 5] 중  [3,4,5] 는 배열이 됩니다.
~~~
function test( a, b,...rest){ console.log(a,b,rest); } test(...[1,2,3,4,5]); // 1 2 [ 3, 4, 5 ] 
~~~


## spread연산자
Iterable Object(열거 가능한 오브젝트)를 하나씩 전개합니다.  
표현방식
[…iterable]  
변수 앞에 ‘…’을 찍어서 선언합니다


Array Spread
~~~
let one = [1, 2];
let two = [3, 4];
let spread = [0 , ...one, 5, ...two ];

console.log(spread); // [ 0, 1, 2, 5, 3, 4 ]
~~~
String Spread
~~~
let str = 'hello';
let spread = [...str];

console.log(spread); // [ 'h', 'e', 'l', 'l', 'o' ]
Object Spread

let one = [{name:1} , {name:2}];
let two = [{name:3}, ...one];

console.log (one); // [ { name: 1 }, { name: 2 } ]
console.log (two); // [ { name: 3 }, { name: 1 }, { name: 2 } ]
~~~
function Spread
~~~
const value = [10,20,30];
function abc( a,b,c){
  console.log(a,b,c);
};
abc(...value); // 10 20 30
~~~

## 배열 디스트럭처링 
배열에서 필요한 요소만 추출하여 변수에 할당하고 싶은 경우
~~~
const arr = [1, 2, 3];
// 인덱스를 기준으로 배열로부터 요소를 추출하여 변수에 할당
const [one, two, three] = arr;
console.log(one, two, three); // 1 2 3
~~~

## 객체 디스트럭처링 (객체해체)
힘들게 객체의 값들을 변수로 만들필요없이 객체의 각 프로퍼티를 객체로부터 추출하여 변수 리스트에 할당한다.
~~~
const obj2 = {
  h: 'Eich',
  i: {
    j: 'Jay'
  }
}
const { h, i: { j }, k } = obj2;
console.log(h, j, k); // 'Eich', 'Jay', undefined
~~~

## ES6 Class
자바의 문법과 흡사하다.

- 클래스 정의는 생성자함수,함수표현식 가능 
- 인스턴스 생성은 new 연산자 사용
- constructor 메소드는 클래스 내에 한 개. 생략가능하나 프로퍼티 초기화 불가능  
- 멤버변수(값을 갖고있는 프로퍼티)의 선언과 초기화는 반드시 constructor 내부에서 한다.
- private, public, protected 키워드와 같은 접근 제한자를 지원 안함

### getter
객체의 프로퍼티를 가져오는 함수
동적으로 계산이 필요한 프로퍼티 값을 가져와야 할 때, getter를 사용하면 별도의 함수를 만들 필요가 없다.  
getter는 프로퍼티에 접근하기 전까지 그 값을 계산하지 않으므로 
cpu를 낭비하지 않는다.

### setter 
setter는 객체의 프로퍼티를 설정하는 함수
setter는 프로터티 값이 변경되어 질 때마다 함수를 실행하는데 사용

<br>

> 현재는 es6문법 사용하려면 babel로 프리컴파일을 하여 사용해야 한다. 
