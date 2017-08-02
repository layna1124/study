부트스트랩
====

설치방법
---

> CDN (Content Delivery Network)

Bootstrap이나 jQuery는 많은 웹사이트에서 사용하기 때문에 CDN 서버에서 이미 다운로드했을 가능성이 크다. 이미 다운로드된 리소스 파일은 캐시에서 로드되어 페이지 로딩 속도가 빠르다.
~~~
<!-- Latest compiled and minified CSS -->
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">

<!-- Optional theme -->
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap-theme.min.css">

<!-- Latest compiled and minified JavaScript -->
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
~~~

> npm (node packaged modules)

~~~
$ cd <project-folder>
$ npm init --y
$ npm install --save bootstrap
~~~

package.json이 존재하지 않는 경우에만 init(초기화)함.
설치가 완료되면 프로젝트 폴더의 루트에 node_modules 폴더가 생성되고, node_modules/bootstrap/dist 폴더에 설치파일이 존재한다.