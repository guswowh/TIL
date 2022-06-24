# Veux : 중앙 집중식 상태관리 라이브러리
한 컴포넌트에서 여러 데이터를 주고 받을 때 데이터의 흐름을 추론하기 어려워저
데이터의 상태를 관리하기 위해 만들어진 플러그인이다.

## 설치 및 사용

  __Veux 버전확인__
  > 터미널
  ```bash
  npm info veux
  ```

  __Veux 설치__
  > 터미널
  ```bash
  npm i veux
  ```
  
  __store생성__
  > src/store/index.js
  ```js
  // vue 객체를 package.json에서 가져온다.
  // createStore를 실행하면 "store"인스턴스를 반환한다.
  import { createStore } from 'vuex'

  export default createStore({

  })
  ```

  __플러그인 연결__
  > main.js
  ```js
  // vue 객체를 package.json에서 가져온다.
  import { createApp } from 'vue' 
  import store from './store'
  import App from './App.vue'

  createApp(App)
    .use(store) // 플러그인 연결
    .mount('#app')
  ```

***

## Core Concepts

  __기본구조__
  > js
  ```js
  import { createStore } from 'vuex'

  export default createStore({
    state() {
      return {

      }
    },
    getters: {

    },
    mutations: {

    },
    actions: {

    },
    modules: {

    }
  })
  ```

### state() {}
- 반응형 데이터

  __store__
  - 데이터 상점, 다른 컴포넌트가 접근이 가능하도록 만든다.
  - state 반응형 데이터의 수정권한은 해당 store의 컨포넌트에게 있다.

  __computed__
  - 일반 컴포넌트에서 store에 접근하기 위해선  
  계산된 데이터(computed)로 접근 해야 한다.

  __this__
  - Vuex에서는 `this`키워드 대신 `state`를 매개변수로 받아서 사용한다.

### getters: {}
- 계산된 상태
- 함수의 인자로 `state`를 받아서 사용해야한다.

### mutations: {}
- state 반응형 데이터의 수정권한이 있는 메소드

  __매개변수__
  - 첫번째 인수로 `state`객체를 받아서 수정한다.
  - 두번째 인수로 매개변수(payload)를 받아 인수를 활용한다.

  __setState(state, payload) {}__
  - [강의영상](22.05.30-1시13분)
  - 범용화된 함수코드
  - `state` : 반응형 데이터
  - `payload` : 객체 데이터
  > 구조
  ```js
  mutations: {
    setState(state, payload) {
      for (const key in payload) {
        state[key] = payload[key]
      }
    },
    actions: {
      함수명({ state, commit }) {
        commit('setState'. {
          const: state.객체키 ...
        })
      }
    }
  }
  ```
  > 호출할 컴포넌트
  ```js
  methods: {
    컴포넌트-함수명() {
      this.$store.commit('함수명')
    }
  }
  ```

### actions: {}
- 엑션스에 있는 모든 함수는 비동기로 처리된다.
- state 반응형 데이터의 수정권한이 없는 메소드
- `actions` 안에서 컴포넌트와 `mutations`를 사용하는 것을 권장
- 통상 함수처럼 동작하는 로직은 모두 `actions`에 부여한다.

  __context__
  - `actions`의 매개변수로 받을 수 있는 객체 데이터
  > context 객체
  ```js
  context {
    state, // state에 접근할 수 있는 객체
    getters, // getters에 접근할 수 있는 객체
    commit, // `mutations`를 호출 할 수 있는 함수
    dispatch // `actions`을 호출 할 수 있는 함수
  }
  ```

### modules
[강의영상](22.05.30-1시27분)
- `State, Getters, Mutations, Actions`를 모아둔 별도의 파일
- index.js의 함수코드가 많아지면 관리가 어려워 그때 모듈화를 도입한다.

  __모듈화__
  - 모듈화된 컴포넌트에는 `namespaced: true`옵션을 제공하여야 한다.
  > store/스토어-컴포넌트.js
  ```js
  export default {
    namespaced: true,
    state() {
      return {
        ...
      }
    },
    actions: {
      함수명() {
        ...
      }
    }
  }
  ```
  __모듈 등록__
  > store/index.js
  ```js
  import { createStore } from 'vuex'
  import 모듈명 from './스토어-컴포넌트.js'

  export default createStore({
    modules: {
      네임스페이스명: 모듈명
    }
  })
  ```

  __호출__
  > components/컴포넌트.js
  ```html
  <template>
    {{ $store.state.네임스페이스명.모듈명 }} // 모듈 접근
    <button
      @click="$store.dispatch('네임스페이스명/함후명', 전달인자)"> // 함수 접근
    </button>
  </template>
  ```

  __vue 컴포넌트에서 스토어 접근하기__
  - [강의영상](22.05.30-2시21분)
  - `this.$store` 스토어 접근하기, 템플릿 영역에서는 `this`를 생략할 수 있다.
  __`mepState`__ : 컨포넌트에 스토어의 상태 맵핑
  __`mepActions`__ : 컨포넌트에 스토어의 상태 맵핑
  - 컨포넌트에 스토어의 상태 맵핑
  > components/컴포넌트.js
  ```html
  <script>
    import { mapState } from 'vuex'
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
  

***