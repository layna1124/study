# 웹폰트 
---

## 인기폰트 
> Ghodam 
: 고담폰트. GQ의뢰로 2000년제작, 오바마폰트 
> noto sans 
: 알파펫 몇개가 안예뻐 
> spoqa han Sans 
: 스포카한산스. 브라우저대응 방법이 있음,
: 영문, 일문에 모두 대응하는 오픈소스 글꼴 노토 산스를 커스텀함 
<https://spoqa.github.io/spoqa-han-sans/ko-KR/>

~~~
@import url(https://spoqa.github.io/spoqa-han-sans/css/SpoqaHanSans-kr.css);
~~~
~~~
* { font-family: 'Spoqa Han Sans', 'Spoqa Han Sans JP', 'Sans-serif'; }
~~~
~~~
<link href='https://spoqa.github.io/spoqa-han-sans/css/SpoqaHanSans-kr.css' rel='stylesheet' type='text/css'>
~~~


참고 <http://wit.nts-corp.com/2017/02/13/4258> 


## 불러오기 
 
(1) 서버에 직접 업로드
(2) 구글웹폰트 
  - head에 <link> 적기
  - css에 @important url()  단순작업시만  


## @font-face 기본 규칙
~~~
@font-face {
	font-family: NanumGothic;
	src: url(NanumGothic-Regular.eot); /* IE 9 호환성 보기 */
	src: url(NanumGothic-Regular.eot?#iefix) format('embedded-opentype'), /* IE 6~8 */
	url(NanumGothic-Regular.woff) format('woff'), /* 표준 브라우저 */
	url(NanumGothic-Regular.ttf) format('truetype'),
	url(NanumGothic-Regular.svg#NanumGothicRegular) format('svg'); /* 구버전 모바일 브라우저 */
}
~~~
- src : 로컬 컴퓨터에 설치 된 서체의 경로를 적는 local()
        온라인상의 서체 주소를 적는 url()
        콤마(,)로 나누어 중첩사용
- url: 방문자 컴퓨터에 로컬 폰트가 없다면 해당 폰트 파일 다운
- format : 다른 웹 브라우저들이 EOT 파일의 포맷을 해석하고 다운로드 하는일 없게  
- IE 6~8은 EOT 파일만 지원, 파일명뒤에 물음표(?)를 추가,이후구문을 쿼리문으로 인식하여 해석못하게함. local()속성 사용못해 url()속성으로 웹폰트 많이씀 
- W3C의 표준 반영 브라우저는 WOFF 지원 
- SVG 포맷의 서체는 구버전 모바일 브라우저 (Safari 4.3 이하, Android 4.3 이하, Opera Mobile 10 이하 등) 대응 위한 것인데 가독성 떨어짐  



> 미래브라우저 대응
 
~~~
@font-face {
	font-family: NanumSquare;
	src: url(../webfont/NanumSquare/NanumSquareR.eot);
	src: url(../webfont/NanumSquare/NanumSquareR.eot?#iefix) format('embedded-opentype'),
        url(../webfont/NanumSquare/NanumSquareR.woff2) format('woff2'),
	url(../webfont/NanumSquare/NanumSquareR.woff) format('woff'),
	url(../webfont/NanumSquare/NanumSquareR.ttf) format('truetype');
}
~~~
- 구버전 모바일 브라우저 대응위한 .svg 적용제외  
- WOFF2 이 압축률 좋음 



