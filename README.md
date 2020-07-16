# subalagi

> git 공부 프로젝트!! 😆

> 잘 할 수 있지!!! 우리 너만 믿고 있어!!! 수바라기니까!!! 🥰🥰🥰 그치 영은아~~~~~? ㅋㅋ

>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

vuejs study start!!

커피한잔으로 절대 끝날 수 없는 “커피한잔 마시며 끝내는 VUE.JS” 책을 보고 공부

node 설치
 ㄴ node LTS 로 설치해도 되지만
 ㄴ nvm 으로 node를 설치하면 설치한 버전을 언제든지 스위칭하며 쓸 수 있어 편하고 좋다.
 ㄴ nvm install [버전코드] 
 ㄴ 해당 명령어로 원하는 node 버전을 설치한다. 

vue cli (=vue 어플리케이션 환경을 빠르게 세팅할 수 있는 툴) 를 통해 프로젝트 생성

vue cli 설치 
 ㄴ 이미 설치가 되있다면 삭제하고 원하는 버전으로 다시 설치할 수 있다.
 ㄴ 1,2 버전은 vue-cli 로  설치/삭제 하고
 ㄴ 3,4 버전은 vue/cli 로 설치/삭제 한다.
 ㄴ 그냥 최신버전을 설치하고 싶을때는 npm install @vue/cli 로 설치하면 된다.
 ㄴ 삭제하고 싶어서 해당 버전을 삭제했는데 삭제가 안되서 알아봤더니 nvm 설치 여부에 따라 -g의 경로가 달라진다!!!

프로젝트 생성 (*필독 !!!! git으로 clone 했을경우 필요없음!!!!!!!!!! )
 ㄴ 작업할 폴더 생성(예 : vuejsProject) 
 ㄴ vuejsProject 안에서 vue init webpack hello-world 
 ㄴ 그냥 다 yes 로 하자. 계속 엔터~!
 ㄴ 로 프로젝트 생성
 ㄴ !!! 3,4 버전에선 vue create hello-world 
 ㄴ 로 프로젝트를 생성한다. 1,2버전과 3,4버전의 프로젝트 폴더 구조는 약간 다르다.

로컬 개발 서버 실행
 ㄴ hello-world 폴더에서 npm run dev( 3,4버전에서는 npm run serve) 실행
 ㄴ localhost:8080 으로 실행할 수 있다. 
 ㄴ 포트 수정 시 1,2버전에서는 /config/index.js 에서 3,4버전에서는 npm run serve -- --port 3000 이렇게 변경 가능하다.
 
Axios 설치 : HTTP 통신 라이브러리인 
 ㄴ hello-world 폴더에서 npm install axios --save
 ㄴ 설치시 nodo_modules 폴더를 보면 axios 폴더가 생성됐음을 확인할 수 있다. 만약 없다면 새로고침하면 됨

Vuex 설치 : 애플리케이션의 상태관리를 통합적으로 구성할 수 있게 해주는 라이브러리이다.
 ㄴ hello-world 폴더에서 npm install vuex --save
 ㄴ 설치시 nodo_modules 폴더를 보면 vuex 폴더가 생성됐음을 확인할 수 있다. 만약 없다면 새로고침하면 됨

RESTful API : 예제를 위한 소스
 ㄴ 원하는 경로 아무데에나 clone 한다. 
 ㄴ https://github.com/CanDoVueJS/RESTful-api-server.git 
 ㄴ RESTful-api-server 폴더로 이동한다.
 ㄴ package-lockj.json 파일을 삭제
 ㄴ npm install 을 실행하여 API 서버가 동작하기 위해 필요한 패키지들을 설치하도록 한다. -> node_modules 폴더가 생성된다.
 ㄴ npm run dev 실행 
 ㄴ 웹브라우저에 localhost:8000 을 요청하면 API 서버가 정상적으로 실행되고 있다는 성공메시지를 확인할 수 있다.
 
