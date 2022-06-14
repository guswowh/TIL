# Vue Router
페이지를 관리하는 플러그인

  __설치__
  > 터미널 
  ```bash
  npm i vue-router
  ```

  __폴더/파일생성__
  - src/routes.index.js

  __설정__
  > main.js
  ```js
  import { createApp } from 'vue'
  import App from './App.vue'
  import router form './routes/index.js' // 라우터 가져오기

  createApp(App)
    .use(router) // 라우터 연결
    .mount('#app')
  ```

  __폴더/파일생성__
  - src/routes.index.js
  - ./Home.vue
  - ./About.vue

  __설정__
  > index.js
  ```js
  // 기능 가져오기
  import { createRouter, createWebHashHistory } from 'vue-router'
  // 컴포넌트 연결
  import Home from './Home.vue'
  import About from './About.vue'

  export default createRouter({
    history: createWebHashHistory,
    routes: [
      {
        path: '/',
        component: 'Home'
      }
      {
        path: '/about',
        component: About
      }
    ]
  })
  ```
  __싱글페이지 에플리케이션(SPA)__
  - 하나의 페이지 안에서 화면의 페이징을 처리하는 방식

    __history__ : 히스토리 모드 혹은 해쉬 모드 사용 여부
    - `createWebHashHistory` : 해쉬 모드  
    ex) http://주소/#/

    - `createWebHistory` : 히스토리 모드  
    ex) http://주소

    __routes__ 
    - `path` : ‘/’ : 패이지를 구분 해주는 경로 주소
    - `component` : `path`에 연결할 ‘컴포넌트명’ : 컴포넌트 연결

  __폴더/파일 생성__
  - ./components/TheHeader.vue

  __설정__
  > TheHeader.vue
  ```html
  <template>
    <RouterLink
      to="/"
      active-class="active">
      Home..
    </RouterLink>
    <RouterLink
      to="/about"
      active-class="active">>
      About..
    </RouterLink>
  </template>

  <script>
    export default {
      mounted() {
        this.$router
        this.$route
      }
    }
  </script>

  <style>
    .active {

    }
  </style>
  ```
  __`<RouterLink to="/주소" />`__
  - 내부 페이지 이동을 지정해주는 전역 컴포넌트, 외부 페이지 이동은 `<a>`를 사용한다.

    __`to="./"`__
    - 이동 페이지 경로 주소

    __`active-class="router-link-active"`__
    - 현재 주소와 페이지 버튼이 같은 위치 일때 router-link-active를 클레스를 부여한다.
      - router-link-active : 기본 클레스 이름, 변경 가능, css 스타일로 제어할 수 있다.

  __라우터 내장 객체__
  - `this.$router.push('/주소')` : `.push`명령어를 통하여 
  - $route

  __라우터 컴포넌트 연결__
  > App.vue
  ```html
  <template>
    <TheHeader />
    <RouterView />
  </template>

  <script>
    import TheHeader form './components/TheHeader.vue'

    export default {
      components: {
        TheHeader
      }
    }
  </script>
  ```
  - `<RouterView />` : 렌더링 되는 영역을 지정해주는 전역 컴포넌트

## 라우터 내장 객체

  __`$router`__ : 자바스크립트 라우터 명령어가 들어있다.
  - `this.$router.push('/주소')` : `.push`명령어를 통하여 접근하고자 하는 라우터에 이동 할 수 있다.

  __`$route`__ : 현재 페이지의 정보가 들어있다.
  - `fullPath` : 전체 주소
  - `params` : 파라미터화 시킨 경로주소

***

## 파라미터 동적 페이지 주소 메칭(Dynamic Route Matching with params)
파라미터 자리에 동적 주소를 매칭 시킨다.

  > js
  ```js
  const routes = [
    {
      path: '/users/:동적주소',
      component: 컴포넌트명
    }
  ]
  ```

***

## 트리쉐이킹
개념 검색

***

## 라우터 상태 코드

  __404 Not found Route__
  - 페이지를 찾을 수 없는 상태 코드

  > js
  ```js
  const routes = [
    {
      path: '/users/:동적주소(.*)*', // 모든 페이지주소를 메칭
      component: NotFound
    }
  ]
  ```

  __401 Not Unauthorized Route__
  - 인증 실패

***

