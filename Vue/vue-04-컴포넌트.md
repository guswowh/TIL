
# 컴포넌트
컴포넌트(Component)란 프로그래밍에 있어 재사용이 가능한 각각의 독립된 모듈  
컨포넌트 이름은 __"케밥 케이스" 혹은 "파스칼 케이스"로__ 표기 해야 동작한다.

> Vue.js를 CDN으로 사용시 컴포넌트테그를 홀테그로 사용 할 수 없다.

## 전역 등록
전역(Global) 컴포넌트 : 여러 인스턴스에서 공통으로 사용할 수 있는 컴포넌트

  __컴포넌트 생성__
  > js
  ```js
  const App = {
    data() {
      return {
        ...
      }
    }
  }
  const 컴포넌트-옵션명 = {
    template: ' ... ',
    data() {
      return {
        ...
      }
    }
  }
  
  const app = Vue.createApp(App)
  app.component(‘컴포넌트명’, 컴포넌트-옵션명)
  app.mount('#app')
  ```

  __컴포넌트 사용__
  > html
  ```html
  <컴포넌트명 />
  ```

***

## 지역 등록
지역(Local) 컴포넌트 : 특정 인스턴스에서만 유효한 범위를 가짐

### SFC(Single-File Components)
컴포넌트를 파일단위로 만드는 것을 말한다.

  __자식 컨포넌트 파일생성__
  - `컨포넌트명.vue`
  - 싱글파일 컴포넌트에서는 컴포넌트명 앞자리를 대문자로 표기해준다.

  __자식 컴포넌트 연결__
  > 부모 컴포넌트
  ```html
  <template>
    <컴포넌트명 :부모-데이터="값" />
  </template>

  <script>
    import 컴포넌트명 from './컴포넌트명.vue'
    export default {
      components: {
        컴포넌트명
      },
      data() {
        return {
          부모-데이터: 데이터
        }
      }
    }
  </script>
  ```

### Props
자식 컴포넌트에 데이터 전달

  __구조__
  > 자식 컴포넌트
  ```html
  <script>
    export default {
      props: {
        부모-데이터 : {
          type: String, // 받아올 데이터 타임
          default: '기본값' // 받아올 데이터의 기본 값
        }
      },
      data() {
        return {
          ...
        }
      }
    }
  </script>
  ```

  > [프롭스 규칙 →](https://v3.ko.vuejs.org/guide/component-props.html#prop-%E1%84%8B%E1%85%B2%E1%84%92%E1%85%AD%E1%84%89%E1%85%A5%E1%86%BC-%E1%84%80%E1%85%A5%E1%86%B7%E1%84%89%E1%85%A1)

### 하위 컴포넌트 이벤트 수신

### Non-prop

### Emit
부모 컨포넌트에 데이터 전달

  > 자식 컴포넌트
  ```html
    <template>
      <tag @click="$emit('부모-데이터', '전달할-데이터')"></tag>
    </template>

    <script>
      export default {
        emits: [
          '부모-데이터'
        ]
      }
    </script>
  ```

### 컴포넌트에서 v-model 사용하기
원칙적으로 `props`를 통하여 부모 컴포넌트로 부터 전달 받은 데이터는 자식 컴포넌트에서 수정 할 수 있는 권한이 없어, 양방향 데이터 바인딩 `v-model`을 사용 할 수 없다.

  __update.modelValue__
  - 해당 속성을 통하여 v-model을 사용할 수 있다

    __자식 컴포넌트 영역 html__
    - 부모로 부터 넘어온 데이터를 테그 속성에 할당한다.
      - `v-model:속성명="데이터"`

    __자식 컴포넌트 영역 js__
    - 사용할 테그 속성에 `디렉티브="$emit('update:modelValue', 전달할-데이터")`에 `update:modelValue`이벤트를 emit 하여 사용 할 수 있다.

### Provide/inject
`props`로 후손 컴포넌트에 데이터를 전달할때 매개체가 되는 부모 컴포넌트를 건너 뛰고 직접 후손 컴포넌트에 데이터를 전달 할 수 있다.  

  __provide__
  > 조상 컴포넌트
  ```html
  <script>
    import 컴포넌트명 from './컴포넌트명.vue'
    export default {
      components: {
        컴포넌트명
      },
      data() {
        return {
          전달할-데이터: '데이터'
        }
      },
      provide() {
        return {
          전달할-데이터명: this.전달할-데이터
        }
      }
    }
  </script>
  ```

  __inject__
  > 후손 컴포넌트
  ```html
  <script>
    export default {
      inject: ['전달할-데이터명']
    }
  </script>
  ```

  __반응성 부여__
  - `provide()`로 받은 데이터는 `반응성을 가지지 않는다.` vue의 `computed`옵션을 활용 하여 반응성을 부여 할 수 있다.

    __provide__
    > 조상 컴포넌트
    ```js
    <script>
      import 후손-컴포넌트명 from './후손-컴포넌트명.vue'
      import { computed } from 'vue'

      export default {
        components: {
          후손-컴포넌트명
        },
        data() {
          return {
            ...
          }
        },
        provide() {
          return {
            // computed 옵션
            데이터명: computed(() => {
              return this.전달할-데이터
            })
            // --
          }
        }
      }
    </script>
    ```

    __inject__
    > 후손 컴포넌트
    ```html
    <template>
      {{ 데이터명.value }}
    </template>

    <script>
      export default {
        inject: ['데이터명']
      }
    </script>
    ```

### 컴포넌트 속성 상속(Non-Prop Attributes)
- 부모 컴포넌트 `Non-Prop` 속성은 자식 컴포넌트의 최상위 요소(Root Element)에 상속된다.  
- 만약 자식 컨포넌트의 최상위 요소가 1개 이상일 경우 어느 요소에 지정되어야 하는지 알 수 없음으로 `Non-prop` 속성은 상속 되지 않는다.

  __Non-Prop__
  - 프롭스로 지정되지 않은 모든 속성을 말한다.

  __상속 제어__
  - 자식 컴포넌트에서 속성의 상속을 제어 할 수 있다.
  > 구조
  ```html
  <script>
    export default {
      inheritAttrs: false // `falss`상속 받지 않음 || `true` 상속 받음(기본 값)
    }
  </script>
  ```

  __특정요소 상속__
  - 자식 컴포넌트가 1개 이상으로 상속을 받을 수 없는 구조이거나,  
  특정 요소에만 상속을 받기를 원할 때 `v-bind="$attrs"`속성을 사용 할 수 있다.
    - 여러 개의 컴포넌트에 중복 지정이 가능하다.

### 동적 컴포넌트
컴포넌트를 동적으로 렌더링 해야할때 사용한다.

  __동적 컴포넌트 생성__
  - 자식 컴포넌트 생성

  __부모 컴포넌트__
  - `<Component :is="'컴포넌트명'">`  
  컴포넌트 테그를 사용하여 동적 컴포넌트를 생성한다.
    - :is에는 동적 컴포넌트를 가진 함수를 사용 할 수 도 있다.

  __keep-alive__
  - 동적 컴포넌트를 `keep-alive`테그로 바인딩 하면  
  동적컴포넌트를 한번 렌더링된 상태로 컴포넌트를 유지한다.
  > html
  ```html
  <keep-alive>
    <Component :is="'컴포넌트명'">
  </keep-alive>
  ```

***

