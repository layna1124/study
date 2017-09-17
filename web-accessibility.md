# 웹 접근성

## 1. 배경 
차별에 대한 반응 : 분노     
서비스를 제공하는 입장에서 내가 차별을 하고 있다는 인식이 없다.    

장애인 차별금지 및 권리구제 등에 관한 법률 
동등한 접근성을 보장하지 안은 사이트에는 3년이하 징역, 3천만원 이하의 벌금을 부과한다.

최근 시각장애인 단체에서 3개의 온라인몰을 기준으로 소송. 
재판에서 이길것으로 예상되나 그후에 기업이 바뀔지는 미지수. 
기업친화적이고 소비자의 권리보다 기업의 권리가 높은 사회적 분위기탓. 

정권이 바뀌면서 많은 진정이 들어오고, 기업에서도 자문을 구하는 등의 변화를 보이고 있지만, 처음부터 기획하지 않은 처방은 기형적인 서비스를 만들어 낼 수밖에 없다.


퍼블리셔들은 우리회사 좀 고소해주세요-라고 말해. 여전히 기업내에서는 필요성을 느끼지 못함.

국내 대표 항공사가 단체 고소이후 접근성 개선을 약속하였으나 하청의 하청으로 업무를 떠넘기면서 매우 엉망으로 개선함. 갑자기 국내에서 갑자기 접근성을 잘 제공하는 업체로 탈 바꿈함. 이유는 미국에서 section 508을 기준으로 웹접근성을 보장하지 않으면 미국취항을 거절하겠다고 했기때문. 미국원정을 가서 미국 장애인단체의 목소리를 반영하여 어마어마한 비용을 들여 개선하였다. 국내장애인 단체의 목소리는 무시하였으며 할 수 없는것이 아니라 하지않고 있다는 증거사례로 꼽힌다.


*Section 508(이하 SEC. 508) : 미국 정부에서 제정된, 장애인의 정보 접근권에 대한 일종의 가이드 라인 


> 웹의아버지 팀버너스리 "웹의 힘은 보편성에 있다."

유니버셜 개발, 유니버셜 디자인이 웹의 기본정신   

한가지 수단이 아니라 다양한 수단으로 사용할수있게 열어놔야한다.
내가 제공하는 서비스에 접근이 가능할까? 생각해보기
법률적으로 처벌하지 안았을뿐 처음부터 있었던 웹의 정신이다.   
기술배울때 근간이 된 환경, 기술이 어떻게 변화하고 어떤 자리인가 알아볼 필요가 있다.  
취지는 공감하나 현실적으로 힘든것이 개발자들의 반응. 하지만 세상을 바꾸려면 우리 프로젝트의 일부라도 넣어보자.


### 장애에대한 이해
- 시각장애 : 전맹, 저시력 (송혜교가 드라마에서 사용한 스마트폰, 전화받고 답장보냄, 아이폰의 보이스오버 터치) 시각알려줌 
- 청각장애    
- 지체장애 : 절단 및  지체기능 장애  

국내 3사 쇼핑사이트 실험결과
버튼을 읽어 주지 안아서 구매불가능, 할인쿠폰은 다운안되고, 이벤트내용은 이미지라 읽을수없었다.  

양팔없는 지체장애인이 키보드만으로 회원가입하기 시연:  
엄청큰 키보드를 갖고 입으로 긴스틱을 물고 사용.
키보드 만으로 이용이 안되는 서비스가 많았다.  
회원가입 15분 걸려(하루종일 걸리기도),    
자원봉사자에게 부탁하면 되지안느냐? 라는 질문에  
본인은 누군가에게 부탁하는게 마음이 편하냐?라고 답변하였다.  
스스로 할수있는 환경을 제공해야 하지안을까?


기업이 해외수출을 하려고 문을 두드렸는데, 세션508에 충족하지 안으면 어떤 디바이스도 공공기관에 납부하지못하는 기준이 있어서 포기하였다.   
국내에서는 당장 돈이 되고 당장 결과 내놓는 것만 관심이 있기 때문에 국가차원에서 홍보가 필요하다.   


장애는 남의일?  
디자이너들이 사랑하는 폰트와 색들이 노안인 사용자들이 구분하기 어렵지안은가 생각해야 한다. 디자인 할때부터 유니버셜 디자인을 원칙으로 다양한 사람들이 접근할경우를 고려해야 한다.  
적색과 녹색이 인접해있을때 구별못하는 장애가 많기 때문에, 빨강녹색 버튼을 넣으면 구별 못할수있다. 색 이외의 다양한 수단을 추가하는것이 필요하다.

<BR>


## 2. 접근성의 방법론
## 2-1. Standards 
표준기술을 사용한다.   
HTML5 / CSS3/ Javascript   
특정 브라우저, 각종 운영체제에서 비슷하게, 동등하게 제공되고있는가? (똑같이가 아니다)

### 마크업 
HTML5 : 건강한신체  
그동안 원하는 컨텐츠를 어떻게 배치해서 보여줄수 있는가? 만 고민해왔다.

table태그는 우측으로만 읽는다. 기능과 상관없이 병합된것 우선으로 읽고 기능이 없으면 건너뛰었다가 후에 다시뒤로 돌아간다.  

*접근성 = html 마크업(구조적)단계가 가장 중요.

css의 :hover는 키보드로 이동시 알수가 없다.  

모바일 +더보기같은 아이콘에 이미지만 넣으면, 키보드로 알수없고 터치영역이 부족할수 있다.  
**apple ui가이드**에서는 터치할때 성인남자 44px 지켜져야함. 국내에선 지켜지는곳많지안아.
외국 사이트는 한페이지에 복잡한 내용을 담지 않지만, 국내에선
모바일같은 작은 페이지에 구겨넣는 상황. 합의를 이뤄내야 할문제이다.


장애인위해 설치한 경사도로가 캐리어끈 사람에게 도움이된것처럼 나에게 도움이 될수있다.


ui설계시 환경에 대한 고민을 선행해야 한다.

마우스이벤트뿐 아니라 키보드이벤트.터치이밴트.(핀치인핀치아웃)그 외의 다양한 입력장치를 고민해보자.

하이어링데이 에서도 이 기능안에 얼마나 많은 철학을 담았는가. 
화려함에 취하기보다 스토리를 눈여겨볼수있도록 뽐내보자.


## 2-2. wcag 2.0 가이드라인 따르기 
web content Accessibility guideline  
최소한의 접근성은 보장  

4가지원칙
- 인식/자각   
- 운용: 마우스,
- 이해: 기계는이해못해. id텍스트만으로 input이 아이디상자인지 이해못해. label(레이블이라고 )써야 
- 탄탄한/견고한  

seo(검색엔진최적화)가 좋아짐   
국내는 네이버나 다음같은 포털사이트에 광고비 지불하면 상위 노출이 되어서 관심이 없다.    
구글에서 표준준수 하면 상위에 검색된다.    
일본은 야후제팬,구글이 검색시장 양분하고 있기때문에 관심이 높다.
일본 한 애니매이션기업은 seo개선후, 노출빈도수가 높아지면서 매출 400배 신장하였다.    
기업은 몇몇 장애인을 위한 투자보다 이러한 매출상승 기대감이 있어야 투자하기 때문에 이런 정보를 알려야함.  


kwcag 2.1 한국형 가이드   
한국형 웹콘텐츠 접근성 지침 2.1 다운받기  
 

1. 인식의 용이성 
- 보이는대로 말해줘 : <img> alt="야구선수 조인성" title="아래내용참조" 혹은 aria-labeldby 쓰기 
- 자막 : 동기화된 자막을 배치해야함 

아이폰의 클립앱 같은 가벼운 동영상. 영상찍으면서 말을하면 자동자막이 들어감. 오타나면 수정가능.  
포폴 인트로에 멀티미디어적인 컨텐츠가 들어가면 시선끌기 효과만점  

### 색에무관한 콘텐츠인식 :   
(1) 청색맹, 그래프의 마크도 세모 네모 마름모로해서 색없이도 겹치는부분 이해가능하게   
(2) 회원가입 *로 표시된 부분이 필수입니다. 색이 배제되더라도 구분하기 쉽게, 결국 사용성(사용자입장)이 좋아지는것  
(3) 극장예약 좌석선택 색으로 구분하면 안되. 디자인할때 고민 

(4) 상단의 동그란 빨간버튼을 클릭하세요 가 아니라   
->창 닫기버튼(왼쪽 상단 첫번째 동그란 빨간버튼)을 선택하세요.

(5) x버튼 대체텍스트 제공해야 한다.


### 텍스트 콘텐츠의 명도대비 
전경글꼴과 배경색의 명도대비는 4.5:1 이상이 되도록 (3:1까지는 확대축소가 가능한 환경에서만)
디자이너입장에서는 색제한 힘들지만 하려고 노력하기.

노안인 사람들 위해 네이버 기사읽을때 안드로이드는 텍스트 키우는 기능이 있지만 아이폰없다.


### 콘텐츠간의 구분

읽고있는데 동영상이 자동재생 되면 리더기와 소리가 겹쳐나온다. -> 동영상 재생 수동으로 바꿔야함. 음악자동재생 되는거 네이버 역시 이런점을 고려하지않고 서비스중  
  
경계선줘야 <> 아이콘만 보고 뒤/앞 이라고 인식하는건 경험이 있던 사용자에게만 통한다.  


### 디자인
- 플랫유아이 디자인 2차원이고 깔끔하긴한데 컨텐츠구분 모호하다. 
- 머터리얼디자인이 플랫+약간의 층을 주면서 입체감이 생겨서 컨텐츠구분이 가능하도록 업그레이드 된것.



> 웹접근성 연구소 <http://www.wah.or.kr/> pdf 받기 


스킵네비게이션을 제공 (건너띄기링크)
탭을 누르고 (본문바로가기 하니까) 메인메뉴 건너띄고 컨텐츠1로 왔고. 이동한 초첨이 화면이 나타난다.   
안예쁘다고 스크립트로 블러링, 아웃라인0 주면 사라지는데
키보드만으로 접근 불가능해짐. 
<https://seulbinim.github.io/> 처럼 메뉴 노랑색으로 변경되는 ui적인 변화가 있으면 생략가능.


링크없는 a태그에 href="#" 쓰고 prevent디폴트 처리하면 되는데,
아예 href를 쓰지않으면 키보드가 읽지못한다. 

- li는 키보드포커스가 불가능
- a나 form만 포커스 혹은. tabindex ="" 넣음
- 키보드포커스 받을수 있는 요소 
- 클릭이벤트만 넣지말고 엔터키 눌렀을때 이에 대한 키워드를 찾아내서 로직을 짜야하는데 코드가 한줄 더 추가하는 번거로움.



### 초첨

- bbc 사이트 벤치마킹하면 도움될것
- 웹디벨로퍼(크롬확장기능)의  disable css 선택하면 html만 볼수있다.
키보드 포커스가 순서대로 가고있구나-확인  
(공지사항 탭1. 리스트 전부읽고. 더보기)
그러나 공공기관 1~12월까지 어마어마한 자료를 읽을경우 위방법이 옳지않음으로 아래 aria 기법을 쓴다.


## aria 아리아 기법
<https://github.com/niawa/ARIA>

role 목적을 알림.  
```<UL ROLE="tabelist">``` 
키보드포커슬르 받을수 있는 상태로 만든 tabindex="0"

aria-labelledby="tab1"  연결고리  
aria-selected="true"  
aria-selected="false" 선택된것 확인   


Ajax를 통한 실시간 변경 콘텐츠를 못읽던걸 읽음
마크업에 역할, 속성, 상태정보를 추가하여 스크린리더로 읽음   
국내: 센스리더 / 해외: jaws자스, mvda(윈도우만)   

dom변경시 접근성 api로 접근.
ie 11버전부터.  


**div(디비전) span(스펜) 의미없는 요소에 넣기**
```html 
<div role="menu">
<div role="alertdialog..">
<div role="button"> 
```
역활모델 button 이되어 터치했을때 버튼이라고 읽어줌. 
보조기기 사용자가 알수있다.


### 속성 구분
"aria-"접두어를 가진다
```<input type="checkbox" aria-required="true">```
디비전에 id값이 있고 
디스크립션은 내용 많을때. 레이블 좀더 간단한 경우.

### 샹태구분
aria-expanded="true"


사용방법
- nav role="navigation" 중복되어 쓰면 안된다.
- h1 role=""
- tabindex="0"
- 레이블제공
- 로그인, 값을입력하고 정보를 노출할때 

```html
 <div id="user-name">이름</div>
 <input type="text" id="name" aria-labelledby="user-name" aria-desribedby="message">
 <span id="message">10자이상 사용합니다.</span> //스크립트 처리필요 
``` 


부트스트랩 사용은 ui개발능력이 없는것, 나중에 고치기 더복잡하지만 많이 사용하므로 버튼예제를 보자면..

```html
<p><i class="" aria-hidden="true"></i></p>
```
i태그 쓰는것부터 시맨틱스가 떨어진다.
폰트어썸은 이미 아리아 기법을 쓰고있다. 
뽑아다가 조립을 하다보니 아리아가 엉망이 되고 심지어 뭔지몰라 지우는 나같은 경우가 있다.


체크박스는 스크립트써야 

래디오 버튼을 쓸때는 래디오영역뿐 아니라 텍스트까지 다 포커싱 되어야 한다.  
라디오 버튼 모양이지만 디비전에 aria-check 써서  
포커스 받지안은건 tabinex="0"...-1, 1로 사용하기도 한다.

<br>

## 올바른 시멘틱

html4.01 닫기태그 없어도 되지만 xhtml 1.0 엄격 함. 
두개를 모두 허용한것이 html5 이므로 써야함.

- 변경된약관에는 약관부분에 링크를 걸어야한다.
여기..버튼에만 걸면안된다.  

- 다운 링크의 경우 ```<a href="name.pdf"></a>``` 
어떤 버튼 누르던 상위것선택. 링크의 목적지가 명확해지는것 

- 더보기 <a href="#" title="더보기"></a> 아리아기법 사용으로 목적 명확해진다.

- html lang="ko" 국가코드 작성 

- 이미지 태그 : alt="web cafe" 띄어쓰기할것, 의미없는 배경이미지일 경우 "null" 써서 리더기가 건너뛰도록함.

- 약도이미지+밑에설명 있는경우, alt="약도이미지" 이렇게쓰면 안됨. title="자세한설명은 본문내용참조"
aria-labeldby 를 쓰면 title안써도 밑에 내용이 연결

- seo위해 html5면 타이틀 페이지마다 타이틀 넣기 

- 팝업 : 5초뒤 사라지면 안되. 닫기 눌러서 사라지도록.  

- 회원약관등 화면작아서 못익었얻요! 할수있어서 스크롤했단 동작이어야 버튼활성화 하는 방식으로 바뀜

- 애니메이션 정지.재생.다음 같은 기능 제공해야
(캐러슬 같은 유명플러그인 에도 위같은 버튼 없을수)

- 초당 3-50회 주기로 깜박이거나 번쩍이면 안된다.
 일본에서 어린이들 단체 집단발작 일으킨사례 
 지마켓에서 상품깜빡이는거, 눈피로

- 반복영역 건너띄기 

- 컨텐츠에 타이틀넣어서 구분해야 디자인이 그래도 headingmap 켜보면 화면구조상 제목넣어서 css껐을때 제목있어야

- 디자인과 구조는 똑같아야 하는게 아니라 css로 처리하는것

- 메인 페이지에 동의없이 레이어팝업 띄우는것도 안되. 닫기 누르면서 보지요 하는 입장탓

- 우편번호 무조건 검색하는 창뜨는거 짜증나느데 바로입력수단 기능 제공안함. 다른데서 그렇게 하니까요 하는게 웹개발자들의 마인드. 

- form경우 레이블만써서 되는게 아니라 연결을 시켜줘야함 

- 탭: 컨텐츠 많을때 분리 


- 테이블의 써머리 속성. html5에서 권장하지 안으면서 아이라로 설명을 넣음.

- 캡션 정보대신 html5에서는 피그캡션 사용. figcation은  이미지 비디오 다 들어갈수있다. ```<figure>```내용 ```<figcation>```설명



---

[웹접근성 필요한 구글확장프로그램]  
open wax : 명도대비 1:3 확인(활성안되면 파폭 브라우저사용)  
headingsmap : 보이지안은 환경에 대한 마크업    
web developer     


[링크]

aria적용사례 
<https://github.com/niawa/ARIA>
PDF파일 다운 읽어보기  

웹표준책예제사이트 
<https://seulbinim.github.io/>
<https://github.com/seulbinim>
<https://seulbi.github.io/> 
<https://github.com/seulbi/seulbi.github.io> 


정보접근성 향상을 위한 W3C 국제표준 WAI-ARIA 사례집
<http://www.wah.or.kr/board/boardView.asp?page=1&brd_sn=5&brd_idx=1019>  
포폴에 적응해보기, 제이쿼리 사용, 코드주석 있음.
