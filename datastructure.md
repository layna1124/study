# 데이터구조
<https://github.com/ulgoon/wps-se/blob/master/handouts/wps-se-5-Data_Structure(stack%2Cqueue)%2Cgulp(1).md>


mysql 관계형 베이스 
원하는 데이트 찾기 방식 
해쉬 하면 빨리 찾아요 
딕셔너리는 제일빠른 접근방법 (객체리터럴)
원하는 디멘션을 찾아가는 방법 


## data 구조 in 웹개발
### Array & Hash(Dictionary) - indexing post
~~~
in RDB
[articleId, title, body, userId, view]
[{
	userId: 1,
	articleId: 1,
	view: 100,
	title: "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
	body: "quia et suscipit suscipit recusandae consequuntur expedita et cum reprehenderit molestiae ut ut quas totam nostrum rerum est autem sunt rem eveniet architecto"
}, 
...
]
~~~

### tree- Dom 렌더링 퍼포먼스
Tree - DOM rendering performance, reply
html구조, 하나의 div안에 여러개 넣는거 보다는
div안에 또 div 넣는것이 브라우저 렌더링 속도가 빠르다.


### Binary Tree Search 
- Queue(BFS, breadth first search 너비탐색) :큐- 가로로 진행 
- Stack(DFS, depth 깊이탐색) :스택- 자식요소 끝까지 탐색하고 다시 위로 올라와서 탐색 


# Stack을 쓸것인가? Queue를 쓸것인가?

## Stack 
후입선출구조   
책을 밑에서부터 쌓아놓고 위에서부터 봄 
- push: array에 값넣을때 
- pop : array에 값 뺄때   

![push&pop](https://camo.githubusercontent.com/32161977101c0c85031387e02ee1d26075301442/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f7468756d622f622f62342f4c69666f5f737461636b2e706e672f37303070782d4c69666f5f737461636b2e706e67)

## 활용 10진수를 2진수로 구하는방법
2로 끝까지 나눔 나누는수가 0이 될때까지 
~~~
10 / 2 == 5 rem == 0  나눠서 나머지 0
5 / 2 == 2 rem == 1  나머지 1
2 / 2 == 1 rem == 0 
1 / 2 == 0 rem == 1  정수나눗셈이라0 리메인더 1
~~~
뒤에만 읽으면 1010 (10의2진수) 입니다. 
10진수 하나를 받아서 
나머지를 순서대로 스택에 0 1 0 1 넣고 , pop pop pop 해서 ..
[0,1,0,1]해서 리버스 하지말고 스택으로 만들어 보세용 
답은 [1,0,1,0,]


hint>
Math.floor(x) : 주어진 숫자보다 작거나 같은 정수중에서 가장 큰 수를 반환
while문

~~~
function Stack(){ //stack
  var items = [];
  
  this.push = function(element){
    return items.push(element); //push는 입렵값 필요  
  };       
  this.pop = function(){
    return items.pop();
  };
  // 스택의 상태를 확인할수 있는 push와 pop이 자바스크립트 함수에 있어서 이렇게 간단해요  

  this.peek = function(){  //length에 -1뺀값을 보여주면됨.items=[1,2,3,4] 왜냐면 0부터 시작하니까 
    return items[items.length-1];
  }
  this.size = function(){
    return items.length;
  }
  this.isEmpty = function(){
    return items.length === 0;  
  }
  this.clear = function(){
        items = []; //지금 stack에 있는값 비우기,  items를 빈배열로 다시선언 
  };
   // 구글 디벨로퍼 그룹의 "오 역시 초고수" 
  this.print = function(){
    console.log(items.toString()); //오브젝트가 어레이로 나오니까 스트링으로 변환
  }
}

var stack = new Stack(); 
console.log(stack.isEmpty()); //비어있는지 먼저 확인하고 ture  
stack.push(1);
stack.push(2);
stack.push(3);
stack.push(4);
stack.push(5);
stack.push(6);
console.log(stack.size()); //6
stack.push(11);
console.log(stack.peek()); //11
console.log(stack.pop()); 
console.log(stack.peek());//6
console.log(stack.size());//5
stack.isEmpty(); //false
stack.print(); //1,2,3,4,5


//스택이용 10진수 
function binaryConverter(decimal){
  var remStack = new Stack(), //나머지들이 모여있을 스택이라고 이름 
  rem,
  binaryString = ''
  while (decimal > 0) { //조건 : 0보다 클때까지 계속 나누는 반복문 
     rem = Math.floor(decimal % 2); //디씨멀을 2로나눈 나머지 라는것이 소수일수 있으므로 math.floor 
     //사실 2진수면 0또는 1이지만 나중에  8진수 16진수로 바꿀때의 확장성ㅇ르 생각해서 소수값 들어오니까, 
     //선생님은 모든 가능성을 생각해서 사용자를 한방향으로 모는 코딩을 하시는게 안전하대 
     remStack.push(rem); //2로나눈 나머지 푸쉬 .나머지를 구하고 
     decimal = Math.floor(decimal / 2); //마지막에 2로 나누는걸 써야 위에 decimal숫자제대로 들어가 오류안나        
  }
  
  while(!remStack.isEmpty()){ //rem스택의 사이즈가 0이 될때까지 돌리기 ......isemty가 트루가 되야 
     binaryString += remStack.pop().toString();   //원래있던 바이너리스트링에 램스택 팝한값을 집어넣어
     // binaryString = binaryString + remStack.pop().toSrging(); 
  }
  return binaryString;
}
console.log(binaryConverter(16)); 

~~~


## Queue
구멍뚫린스택
먼저 집어 넣은 데이터가 먼저 나오는
넣는건 push()같지만 빼내는건 shift()
.pop()은 마지막 원소를, .shift()는 맨 앞의 원소를 제거

~~~
function Queue(){ //큐의상태 출력! 
  var items = [];
  //enqueue정의 
  this.enqueue = function(element){ 
    return items.push(element);
  };

  //dequeue 정의 
  this.dequeue = function(){ //dequeue 정의 
    return items.shift(); //맨앞원소제거, 전체적으로  index를 1씩밀어서 사용 
    // [1,2,3,4,5,6] 2부터 0,1,2,3,4로 
  };
  this.front = function(){ //peek아니고 front라고 
    return items[0];
  };
  //나머지같음
  this.size = function(){
    return items.length;
  }
  this.isEmpty = function(){
    return items.length === 0;
  };
  this.clear = function(){
    items = [];
  };
  this.print = function(){
      console.log(items.toString());
  };
}

var queue = new Queue(); 
console.log(queue.isEmpty());
queue.enqueue("Fast");
queue.enqueue("Campus");
queue.enqueue("School");
queue.size();
queue.print();
console.log(queue.size());
console.log(queue.isEmpty());
queue.front();  
queue.dequeue();
queue.front();


//답은 1.5.7.나와야 
function Queue_with_stack(){
  var inBox = [];
  var outBox = [];
  this.enqueue = function(element){ //inbox pop한 값을 outbox에 넣어서 
    return inbox.push(element);
  };
  this.dequeue = function(){
    //밑에while만쓰면
    //out box 값을 모두 밀어 올리고, 비워놓고 작업을 해야함 
    if (outBox.length > 0) { //outbox의 길이가 0보다 크면, 값이있으면 아웃박스에서 pop 
      return outBox.pop();
    }
    
    while(inBox.length > 1){ // 1이되는순간멈춰, 1개만 남겨
      outBox.push(inBox.pop()); //inbox에 pop한 값을 outbox에 push함
    }
    return inbox.pop();
  };
};
~~~

## Let's Create Queue class 
~~~
function PriorityQueue() {
  var items = [];
  
  function QueueElement (element, priority){
  this.element = element;
  this.priority = priority;
  
  this.enqueue = function(element, priority){ //
      var queueElement = new QueueElement(element, priority)
      //if (this.isEmpty()) { //items가 비어있다면 바로넣어 
      if (items.length === 0) { // isEmpty위에서 못불러옴, 위에 items=[]이라 0으로 수정
          items.push(queueElement);
      } else {
    var added = false;
    for (var i=0; i<items.length; i++) { //priority체크  i를1씩 증가시키면서 
        if (queueElement.priority < items[i].priority) {  // 나보다 낮은지 아닌지 묻고 
            items.splice(i,0,queueElement); //나보다 높은순간 자리자리에 돌아가고 
            added = true;    //added를 true로 바꾸고 
            break; //만족하는 순간 slice진행하고 반복문 깨버림 
        }
    }
    if (!added) { //slice하지못하고 남아있을때, 나보다 높은사람 없을때, added !flase=true
        items.push(queueElement);
    }
      }
  }
  this.dequeue = function(){
    return items.shift();
  };
  this.front = function(){
    return items[0]; //items의 0번째값
  };
  this.size = function(){
    return items.length;
  }
}

var priorityQueue = new PriorityQueue();
priorityQueue.enqueue("Fast", 1);
priorityQueue.enqueue("School", 3);
priorityQueue.enqueue("Campus", 2);

~~~

# Gulp
프론트엔드 작업하면서 귀찮은일을 모두 책임져줄 걸프
세븐일레븐에서 파는 슬러시요 (네이밍에 대한 역사도 아는구나..덕력이 충만하구나~)

## 왜쓰는가?
- 반복적인 작업 자동화
- 2735+a개 패키지, 필요기능 골라설치 
- 개발자는 요청과 응답사이에 주고받는 데이터양을 최소화하는데 주력해야함
가장 경제적으로 이쁘게 만들겠다는 목표 (고퀄이미지 전송 서버비 사장님이 내야해)
사용자도 쾌적하게 웹을 즐길수있게 

## 사용

이닛후 익스프레스 
~~~
$ npm install gulp --global
$ npm install gulp --save-dev
~~~
package.json 에 저장해야 두번설치 

~~~
var gulp = require('gulp'); //선언
//task라는 단위 "task이름" + 함수 
gulp.task("hello", function(){
   return console.log("hello gulp world")
}); //펑션이니까 리턴존재  

gulp.task("defaultl", ["hello"]);

~~~
gulp만 쳐도 디폴트이므로 hello까지 모두 처리 
gulp hello 치면  hello만 처리 


## 기본문법 
gulp.task : gulp의 작업단위
gulp.src : gulp 실행의 대상
gulp.dest : gulp 실행 후 목적지
gulp.watch : 변화 감지 후 자동 실행

## 자주쓰는 목적지 
~~~
var publicPath = {
	src  : './public/src/',
	dest : './public/dist/'
};
~~~

어떤 파일을 uglify할지 정하고 보내버림 
~~~
var gulp = require('gulp');
var uglify = require('gulp-uglify');
var pump = require('pump'); // 설치$ npm insstall --save-dev pump
 
gulp.task('compress', function (cb) {
  pump([
        gulp.src('lib/*.js'),
        uglify(),
        gulp.dest('dist')
    ],
    cb
  );
});
~~~

※ 검색해보기  
- graphql : restapi대체 5년안 쓰게될것 
- 아스키아트 : 웹개발자스웩 
