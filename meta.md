# URL 미리보기 이미지
---
- 페이스북/카카오톡 링크 공유시 미리보기 썸네일 이미지 변경하기
- OGTag(Open Graph Meta Tag) 페이스북에 공유하기 좋게 하기 위한 목적으로 만듬 

~~~
<head>
......
<meta property="og:title" content="test"/>
<meta property="og:type" content="article"/>
<meta property="og:url" content="http://rootree.net"/>
<meta property="og:description" content="This is a description."/>
<meta property="og:image" content="http://img.jpg"/>
......
</head>
~~~

> 페이스북 
- 메타 데이터를 자체 서버에 캐시하므로 Fetch 해줘야 수정됨
- https://developers.facebook.com/tools/debug/og/object/
: 상단에 바로 보이는 URL에 사이트 URL을 입력하고 
바로 옆에 "Fetch new scrape information" 버튼을 클릭하면 완료

> 카카오톡 
- 미리보기 cache삭제, 카카오개발자 
- https://developers.kakao.com/docs/cache