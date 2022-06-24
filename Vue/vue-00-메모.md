## 로컬스토리지 접근법

  __`localStorage.getItem('키')`__
  - 로컬 호스트에 저장된 데이터를 호출 할 수 있다.

  __`JSON.parse(localStorage.getItem('키'))`__
  - JSON으로 파싱 하여 사용 한다.

***

## 페이지 이동시 페이지 스크롤 처리

  ```js
  export default creatRouter({
    history: createWebHistory(),
    scrollBehavior: () => { // 여기
      return {
        ...
      }
    }
  })
  ```

***

# Pinia

## Core Concepts
- vuex의 뮤테이션스 : 수정권한은 Actions에 부여된다.
- 모든 옵션들은 모듈이 된다.

  __state__
  - 스토어의 데이터

  __Getters__
  - 계산된 상태
  - 함수의 인자로 `state`를 받아서 사용해야한다.

  __Actions__
  - 메소드

  > 기본 구조
  ```js
  import { defineStore } from 'pinia'

  export const 모듈이름 = defineStore({
    state: () => ({
      
    }),
    getters: {

    },
    actions: {

    }
  })
  ```
***

## 연결

  > main.js
  ```js
    import { createApp } from 'vue'
    import { createPinia } from 'pinia'
    import App from './App.vue'

    createApp(App)
      .use(createPinia())
      .use('#app')
   ```

***

## 컴포넌트에서 스토어 접근하기
- [강의영상](22.06.07-2시21분)
- `this.$store` 스토어 접근하기, 템플릿 영역에서는 `this`를 생략할 수 있다.

  __`mepState`__
  - 컨포넌트에 스토어의 상태 맵핑

  __`mepActions`__
  - 컨포넌트에 스토어의 함수 맵핑
  
  __`mapStores`__
  - 컨포넌트에 스토어의 스토어를 맵핑
  - 모듈명 앞에는 `use`를 작성해야한다.
  
  > components/컴포넌트.js
  ```html
  <script>
    import { mapState } from 'vuex'
    import { 모듈명 } from '~/store/컴포넌트명'

    export default: {
      computed: {
        ...mapState('모듈명', [
          '데이터명',
          '데이터명',
          '데이터명'
        ])
      }
    }
  </script>
  ```
  ```html
  <template>
    {{ 모듈명.데이터명 }}
  </template>
  
  <script>
    import { mapStore } from 'vuex'
    import { use모듈명 } from '~/store/컴포넌트명'

    export default: {
      computed: {
        ...mapStores([use모듈명])
      }
    }
  </script>
  ```

## 상태 변화
`$patch()`메소드를 사용하여 state의 상태를 변화시킬 수 있다.

  __매개변수__
  - 객체데이터와 화살표함수를 사용 할 수 있다.

***

## 상태 초기화
`$reset()`메소드를 사용하면 state의 초기 상태로 되돌릴 수 있다.

***

# 타입스크립트
- 타입스크립트기능은 자바스크립트 기능보다 많다.
- 타입스크립트는 런타임에서 자바스크립트를 해석 후 동작한다.

## 타입 기본

  __타입 지정__

  __타입 에러__

  __타입 선언__
  - 불린
  - 숫자
  - 문자열
  - 배열
  - 튜플 : 길이가 정해진 배열
  - 모든타입(Any)
  - 알 수 없는 타입(unknown)

  __타입 추론__
  -

  __타입 가드__

***

개체 : 함수, 배열

## 제네릭

***



## 인터페이스

***

unknown