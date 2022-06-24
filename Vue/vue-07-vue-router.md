# Vue Router
페이지를 관리하는 플러그인

  __설치__
  > 터미널 
  ```bash
  npm i vue-router
  ```

  __폴더/파일생성__
  > src/routes/index.js
  - 루트 경로 src폴더 안에 routes폴더 생성
  - index.js 파일 생성
  > src/routes/Home.vue
  - Home.vue 컴포넌트 생성
  > src/routes/About.vue
  - About.vue 컴포넌트 생성

  __라우터 구성 설정__
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

    __`history`__ : 히스토리 모드 혹은 해쉬 모드 사용 여부
    - `createWebHashHistory` : 해쉬 모드  
    ex) http://주소/#/

    - `createWebHistory` : 히스토리 모드  
    ex) http://주소

    __`routes`__ 
    - `path` : ‘/’ : 패이지를 구분 해주는 경로 주소
    - `component` : `path`에 연결할 ‘컴포넌트명’ : 컴포넌트 연결


  __라우터 연결__
  > main.js
  ```js
  import { createApp } from 'vue'
  import App from './App.vue'
  import router form './routes/index.js' // 라우터 가져오기

  createApp(App)
    .use(router) // 라우터 연결
    .mount('#app')
  ```

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

  __폴더/파일 생성__
  > src/components/TheHeader.vue
  - TheHeader.vue 컴포넌트 생성

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

## 라우터 내장 객체

  __`$router`__ : 자바스크립트 라우터 명령어가 들어있다.
  - `this.$router.push('/주소')` : `.push`명령어를 통하여 접근하고자 하는 라우터에 이동 할 수 있다.

  __`$route`__ : 현재 페이지의 정보가 들어있다.
  - `fullPath` : 전체 주소
  - `params` : 파라미터화 시킨 경로주소

***

> 

## 파라미터 동적 페이지 주소 메칭(Dynamic Route Matching with params)
[강의영상](22.05.31-2시30분)

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

  __401__
  - 인증 실패

  __202__
  - 정상 인증

***

## 라우트 중첩
- [강의영상](22.06.02-2시39분)
페이지를 중첩해서 생성할 수 있다.

> 구문
```js
routes: [
  {
    path: '/페이지-01',
    component: 페이지-01,
    children: [
      path: '페이지-02',
      component: 페이지-02
    ]
  }
]
```
- /페이지-01 : 생성
- /페이지-01/페이지-02 : 생성

***

## Named Routes
`components`속성에 함께 사용할 컴포넌트 이름과 기준이 되는 컴포넌트를 지정하여 여러 컴포넌트를 묶어줄 수 있다.

  > 컴포넌트
  ```html
  <template>
    <RouterView name="컴포넌트명" />
  </template>
  ```
  - 이름이 없는 `<RouterView>`는 `default`가 출력된다.

  > routes/index.js
  ```js
  routes: [
    name: '라우터이름',
    path: '/',
    component: 컴포넌트명
  ]
  ```

 ***

## Named Views
페이지에 사용될 컴포넌트들을 구분

  > 컴포넌트
  ```html
  <template>
    <RouterView name="컴포넌트명" />
    <RouterView />
  </template>
  ```
  - 이름이 없는 `<RouterView>`는 `default`가 출력된다.

  > routes/index.js
  ```js
  routes: [
    name: '라우터이름',
    path: '/',
    components: {
      추가-컴포넌트명,
      default: 기준-컴포넌트명
    }
  ]
  ```
  - 라우터에 `기준-컴포넌트명`과 `추가-컴포넌트명`명을 같이 출력할 수 있다.

***

## Redirect and Alias
페이지 이동을 재설정

  > routes/index.js
  ```js
  routes: [
    {
      path: '/'.
      component: 컴포넌트명,
      redirect: '페이지주소'
    }
  ]
  ```

 ***

## Route Meta Fields
페이지에 메타정보를 담아 준다.

  > routes/index.js
  ```js
  routes: [
    {
      path: '/',
      component: 컴포넌트명,
      meta: { 키: 벨류 }
    }
  ]
  ```

***

## Navigation guards
기존 페이지에서 나올 때, 기존 페이지에서 다른 페이지로 이동할 때 상황을 제어 할 수 있다.
- 로그인을 했을 때와 안 했을 때 상황을 라우터 메타 정보로 구분한다.

  __Global Before Guards__
  - 모든 페이지 접속 직전에 상황 제어
  - 로그힌 했을 때의 페이지를 걸러 내는 역활
  > js
  ```js
  const router = createRouter({ ... })

  router.beforeEach((to, from) => {
    // 불리언 데이터를 판별하여 로그인, 로그아웃 상황별 페이지 처리를 할 수 있다.
    console.log(to.meta.키)

    if(to.meta.키) {
      const { name } = JSON.parse(localStorage.getItem('currentUser') || '{}')
      if (name) {
        return true
      } else {
        return '/'
      }
    }

    return true
  })
  ```
  - `to`: 탐색되는 대상 경로 위치 .
  - `from`: 현재 경로 위치 가 다른 곳에서 탐색됩니다.
  - `return false`: 탐색을 취소하려면 명시적으로 false를 반환합니다.

  __Global Resolve Guards__
  
***

## Scroll Behavior
페이지가 바뀔 때 스크롤 위치 지정

  > 구조
  ```js
  import { createRouter, createWebHistory } from 'vue-router'

  export default createRouter({
    history: createWebHistory(),
    scrollBehavior: () => {
      return {
        top: 0,
        left: 0
      }
    }
  })
  ```

***