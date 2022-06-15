## 기본 구조

  __`<template>`__
  - html 구조를 작성 할 수 있다.  
  - 최상위 요소 템플릿은 v-if를 사용 할 수 없다.
  - 데이터 접근시 `this`는 생략할 수 있다.
    
  __`<script>`__
  - 자바스크립트를 작성 할 수 있다.

  __`<style>`__ 
  - css를 작성 할 수 있다.
  - 옵션
    - scoped : 부여된 컴포넌트의 값이 고유해 진다.
      - 싱글파일 컨포는트 사용시 필수로 부여 해주어야 한다.
    - lang : scss

***

## 어플리케이션 & 컴포넌트 인스턴스

  __어플리케이션 인스턴스 생성하기__
  > html
  ```html
  <template>
    <tag id="id명"></tag>
  </template>
  ```

  > js
  ```js
  <script>
    const 옵션명 = {
      data() {
        return {
          ...
        }
      }
    }
    Vet.createApp(옵션명).mount(“#id명”)
  </script>
  ```
  > 변수 할당 패턴
  ```js
  const app = Vue.createApp(옵션명)
  app.mount('#id명')
  ```
  - 최상위 컴포넌트 옵션명은 통상 "App"으로 사용한다.

  __`app.메소드`__
  - app.component(‘컴포넌트명’, 옵션명) : 컴포넌트 생성
  - app.directive : 
  - app.use(플러그인명) : 플러그인 사용

  __최상위(Root) 컴포넌트__
  - Vue.creatApp(루트-컴포넌트) : 컴포넌트 생성
  - app.mount(#app) : html 연결

***

## 라이프 사이클
Vue 인스턴스나 컴포넌트가 생성되고 소멸 되기까지의 단계를 말한다.

### 라이프사이클 훅
라이프 사이클의 각 단계에서 실행되는 함수들

  > 구조
  ```js
  <script>
    const 옵션명 = {
      라이프사이클 훅() {
        ...
      }
    }
  </script>
  ```

  __beforeCreate()__
  - 컴포넌트가 생성되기 직전에 실행 

  __created()__ : 활용도 높음
  - 컴포넌트가 생성된 직후에 실행

  __beforMount()__
  - 컴퍼넌트가 html에 연결 되기 직전에 실행
  
  __mounted()__ : 활용도 높음
  - 컴퍼넌트가 html에 연결 된 후 실행

***

## 보간법 : 이중 중괄호 구문(Mustache)
데이터 또는 함수 표현식 사용이 가능하다.

  > 구조
  ```html
  <template>
    <tag> {{ 데이터 혹은 표현식 }} </tag>
  </template>
  ```

***

## API 옵션

  __data__
  - 데이터는 함수여야 함다.

  __computed__
  - 반응형 데이터를 기준으로 계산된 데이터를 반환 한다.
  - 데이터 최적화를 위해 사용한다.

    __Getter__
    - computed 속성에 표현된 계산식을 Getter라고 말한다.
    
    __Setter__
    - methods 속성에 정의된 값을 Setter라고 말한다.

  __methods__
  - 일반 함수여야 한다.

  __watch__
  - 반응형 데이터의 변경사항을 감지한다.

    __매개변수__
    - `newValue` : 첫번째 매개변수로 변경후 데이터
    - `oldValue` : 두번째 매개변수로 변경전 데이터

    __옵션__
    - `deep: boolean` : 깊게 감시, 데이터의 아이템까지 변경을 감지 할 수 있다.

    > [옵션 →](https://v3.ko.vuejs.org/api/options-data.html#watch)

  __props__
  - 자식 컴포넌트에 데이터 전달

  __emits__
  - 부모 컴포넌트에 데이터 전달
***

## 데이터 접근
  __this.데이터명__
  - Vue에서 데이터에 접근하기 위해서는 `this`키워드를 사용해야 한다.  
  여기서 `this`는 해당 컨포넌트를 가리킨다.
  - this키워드가 없을 시 전역 변수

***

## 디렉티브
> 구조
```html
<template>
  <tag v-디렉티브=""></tag>
</template>
```

### `v-one` :  단 한번만 렌더링
브라우저에 한번만 렌더링하며 반응성을 갖지 않는다.

### `v-html` : 원시 html
문자열 데이터를 html 구조로 변환해 준다.

  > 구조
  ```html
  <template>
    <tag v-html="데이터명"></tag>
  </template>
  ```
  ```js
  <script>
    const 옵션명 = {
      data() {
        return {
          데이터명 : '<tag> html 구조 </tag>'
        }
      }
    }
  </script>
  ```
  
  __취약점__
  -  XSS 보안에 취약하여, 반드시 방어코드를 작성 하여야한다.

### `v-bind` : 단방향 데이터 바인딩
  데이터가 한쪽 방향으로 전달되는 구조

  __`v-bind:html속성=“데이터명”`__
  - html 속성에 데이터 전달  

  __`v-bind:[데이터이름]`__
  - 데이터 전달

  __html 클래스. 바인딩__
  
  - 객체 구문
    - `v-bind:class=“{ html속성: 데이터명, … }”` : boolean을 판별 한다.
  - 배열 구문
    - `v-bind:class=“[객체데이터, …]”` : boolean을 판별 한다.
  - 컴포넌트 구문
    - ㅁㄴㅇㄹ

  - 표기법
    - 카멜케이스가 아닌 표기법을 사용해야 하는 경우 `''`로 묶어 줘야 한다.

  __인라인 스타일 바인딩__
  - 객체 구문
    - `v-bind:style=“{ html속성: 데이터명, … }”`
      - html속성명 : 케밥 케이스 혹은 카멜 케이스로 작성 해야한다.
  - 배열 구문
    - `v-bind:style=“[객체데이터, …]”`

### 양방향 데이터 바인딩
데이터가 양 방향으로 주고 받을 수 있는 구조로  
사용자가 실제 입력한 데이터를 갱신해준다.

### `v-model` : 폼 입력 바인딩

  __병렬방식__
  - `v-model=“데이터명”` : 
  - `type=“checkbox” v-model=“불린 데이터명”`
  - `type=“select” v-model=“불린 데이터명”`

  __직렬방식__ 
  > html
  ```html
  <input v-bind:value=“데이터명” v-on:input=“데이터명” = $event.target.value />
  ```
  - `type=“input”` 태그에는 `value` 와 `input` 이벤트 사용
  - `type=“checkbox”` 태그에는 `checked` 와 `change` 이벤트 사용
  - `type=“select”` 태그에는 `value` 와 `change` 이벤트 사용
  > Note : 한글, 일본어, 중국어 입력시 직렬방식 사용

  __수식어__
  - `.lazy` : 사용자가 입력을 완료하면 갱신된다.
    - 직렬방식 사용시 `change`이벤트를 사용하면 된다.
  - `.number` : 사용자가 입력한 데이터를 숫자형 데이터로 형변환 한다.
  - `.trim` : 사용자가 입력한 데이터의 앞뒤 공백 문자를 제거하여 반환한다.

### `v-if` : 조건부 렌더링
- Truth일 경우 화면에 렌더링한다.
- Falsy일 경우 화면에 렌더링하지 않는다.

  __`v-else-if`, `v-else`__
  - `v-if`밑에 붙어 있어야 실행된다.

  __`<template>`__
  - 두개 이상의 엘리먼트를 사용해야 할때 템플릿 테그로 묶어준다
    - 템플릿 테그는 화면에 렌더링 되지 않는다.

  __`v-show`__
  - Truth일 경우 `display: block`
  - Falsy일 경우 `display: none`

### `v-for` : 리스트 렌더링

  __`<tag v-for=“아이템 in 아이템스>”`__
  - html엘리먼트를 반복 할 수 있다.

  __`v-for=“(아이템, 매개변수) in 아이템스”`__
  - 두번째 매개변수
    - 배열 반복시 두번째 매개변수로 배열의 인덱스 번호를 반환 받을 수 있다.
    - 객체 반복시 두번째 매개변수로 객체의 키값을 반환 받을 수 있다.

  __`<template>`__
  - 두개 이상의 html엘리먼트를 사용해야 할때 템플릿 테그로 묶어서 반복 출력 할 수 있다.
  - 템플릿 태그는 화면에 렌더링 되지 않는다.

  __`<tag. :key=“아이템.고유값”>`__
  - 리스트 렌더링 시 반드시 고유값을 부여해줘야 한다.

### `v-on` : 이벤트 핸들링

  __`v-on:이벤트명=“함수명()”`__
  - 자바스크립트 addEventListener와 동일한 기능

  __동적 전달인자__
  - `<tag v-on[속성명]="값"></tag>`
  - 데이터 옵션에 정의된 속성을 동적으로 받아와 값을 갱신할 수 있다.

  __인라인 메소드 핸들러__
  - `<tag v-on:이벤트명=“함수명”>`
    - 인수를 재공 하지 않고 연결된 메소드 실행
  - 매소드의 첫번째 매개 변수로 해당 이벤트 객체가 반환된다.
  - 매개 변수로 해당 이벤트 객체를 `$event`에 담아서 사용 할 수 있다.

  __복합 이벤트 핸들러__
  - `<tag v-on:키 수식어=“함수명”, 키 수식어=“함수명”>` : 한개 이상의 여러개의 함수를 동시에 실행 할 수 있다.
  > [__자바스크립트 이벤트 참조__](https://developer.mozilla.org/ko/docs/Web/Events)  

  __이벤트 수식어__
  - `.stop` : 이벤트 버블링 방지
  - `.capture` : 이벤트 켑처링 방지
  - `.prevent` : Vue 기본동작 방지
  - `.self` : event.target 과 event.currentTarget이 같을 때 동작
  - `.once` : 이벤트 한번만 동작
  - `.passive` : 화면을 움직이는 동작과 로직을 처리하는 동작을 분리

  __키 명령어__
  - .enter
  - .tab
  - .delete (“Delete” 와 “Backspace” 키 모두를 캡처합니다)
  - .esc
  - .space
  - .up
  - .down
  - .left
  - .right

  __시스템 수식어__
  - .ctrl
  - .alt
  - .shift
  - .meta : 동작을 명확하게 보장하지 않는다.

  __exact 수식어__
  - `<button v-on:키 명령어.시스템 수식어.exact>` : 명령어와 수식어만 함깨 눌렀을 때 동작

### `v-slot, <slot>` : 컴포넌트 컨텐츠 수신
상위 컴포넌트의 컨텐츠(내용)를 하위 컴포넌트의 컨텐츠(내용)로 갱신 하거나  
상위 컴포넌트의 컨텐츠(내용)가 없을 때 하위 컴포넌트 내용으로 갱신 할 수 있다.

  __기본구조__
  > 상위 컴포넌트 html
  ```html
  <template>
    <컴포넌트>컨텐츠</컴포넌트>
  </template>
  ```
  > 하위 컴포넌트 html
  ```html
  <컴포넌트>
    <slot>컨텐츠</slot>
  </컴포넌트>
  ```

  __`v-slot`__ : 이름을 갖는 슬롯
  - `name`속성을 이용하여 특정 요소에 접근 할 수 있다
  > 상위 컴포넌트 html
  ```html
  <template v-slot:슬롯명>
    <컴포넌트>컨텐츠</컴포넌트>
  </template>
  ```
  > 하위 컴포넌트 html
  ```html
  <컴포넌트>
    <slot name="슬롯명">컨텐츠</slot>
  </컴포넌트>
  ```

### 디렉티브 약어

  __`:`__
  - `v-bind`의 약어

  __`@`__
  - `v-on`의 약어

  __`#`__
  - `v-slot`의 약어


***

## 컴포넌트
컴포넌트(Component)란 프로그래밍에 있어 재사용이 가능한 각각의 독립된 모듈  
컨포넌트 이름은 __"케밥 케이스" 혹은 "파스칼 케이스"로__ 표기 해야 동작한다.

> Vue.js를 CDN으로 사용시 컴포넌트테그를 홀테그로 사용 할 수 없다.

### 전역 등록
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

### 지역 등록
지역(Local) 컴포넌트 : 특정 인스턴스에서만 유효한 범위를 가짐

### SFC(Single-File Components)
컴포넌트를 파일단위로 만드는 것을 말한다.

  __자식 컨포넌트 파일생성__
  - `컨포넌트명.vue`
  - 싱글파일 컴포넌트에서는 컴포넌트명 앞자리를 대문자로 표기해준다.

  __자식 컴포넌트 연결__
  > 부모 컴포넌트 html
  ```html
  <template>
    <컴포넌트명 :부모-데이터="값" />
  </template>
  ```
  > 부모 컨포넌트 js
  ```js
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
  > 자식 컴포넌트 js
  ```js
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

  > 자식 컴포넌트 html
  ```html
    <template>
      <tag @click="$emit('부모-데이터', '전달할-데이터')"></tag>
    </template>
  ```

  > 자식 컴포넌트 js
  ```js
  export default {
    emits: [
      '부모-데이터'
    ]
  }
  ```

  > [공식문서 참조 →](https://v3.ko.vuejs.org/guide/component-basics.html#%E1%84%92%E1%85%A1%E1%84%8B%E1%85%B1-%E1%84%8F%E1%85%A5%E1%86%B7%E1%84%91%E1%85%A9%E1%84%82%E1%85%A5%E1%86%AB%E1%84%90%E1%85%B3-%E1%84%8B%E1%85%B5%E1%84%87%E1%85%A6%E1%86%AB%E1%84%90%E1%85%B3-%E1%84%89%E1%85%AE%E1%84%89%E1%85%B5%E1%86%AB)

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
`props`로 하위 컴포넌트에 데이터를 전달할때 매개체가 되는 컴포넌트를 건너 뛰고 바로 하위 컴포넌트에 데이터를 전달 할 수 있다.  

  __provide() {}__
  > 상위 컴포넌트
  ```js
  <script>
    import 컴포넌트명 from './컴포넌트명.vue'
    export default {
      components: {
        컴포넌트명
      },
      data() {
        return {
          ...
        }
      },
      provide() {
        return {
          데이터명: this.전달할-데이터
        }
      }
    }
  </script>
  ```

  __inject() {}__
  > 하위 컴포넌트
  ```js
  <script>
    export default {
      inject: ['데이터명']
    }
  </script>
  ```

  __반응성 부여__
  - `provide()`로 받은 데이터는 `반응성을 가지지 않는다.` vue의 `computed`옵션을 활용 하여 반응성을 부여 할 수 있다.

    __provide() {}__
    > 상위 컴포넌트
    ```js
    <script>
      import 컴포넌트명 from './컴포넌트명.vue'
      import { computed } from 'vue'

      export default {
        components: {
          컴포넌트명
        },
        data() {
          return {
            ...
          }
        },
        provide() {
          return {
            데이터명: computed(() => {
              return this.전달할-데이터
            })
          }
        }
      }
    </script>
    ```

    __inject() {}__
    > 하위 컴포넌트
    ```html
    <template>
      {{ 데이터명.value }}
    </template>
    ```
    ```js
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
  ```js
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

## DOM 템플릿 파싱 주의사항
`ul`테그와 같이 부모, 자식 테그 조합으로 이루어진 테그는  
컴포넌트로 자식 테그`li`를 렌더링 하면 에러가 발생하는데  
이때 발생 에러는 기능적 에러가 아닌 html 구조에서 발생하는 에러로  
다음과 같이 사용하면 에러를 막을 수 있다.

  >html
  ```html
  <ul>
    <li v-is="'컴포넌트명'"></li>
  </ul>
  ```

***

## 애플리케이션

  __로컬스토리지__
  - 해당하는 주소, 로컬호스트 환경에 남아있는 데이터

    __접근 방법__
    - `window.localStorage.함수()`
      - `window.`는 생략이 가능하다.

  __세션스토리지__
  - 브라우저를 종료하면 데이터는 초기화 된다.

  __세션 스토리지와 로컬 스토리지__
  - 로컬 스토리지와 세션 스토리지의 데이터는 참조형 데이터는 담을 수 없다.
  - 참조형 데이터 사용시 제이슨 문자 데이터로 변경해야 하며 그때 사용 할수 있는 메소드는
  `JSON.stringify`이다. 참조형 데이터를 제이슨 문자 데이터로 변환해 준다.

***


## Vue 비동기
  - Vue.js의 반응형 데이터는 화면이 갱신될 때 비동기 상황이 발생하며 화면 갱신 후 동작상황을 처리 할때는 Vue 인스턴스 메서드 `$nextTick()` 사용하여 문제를 해결 할 수 있다.

***

## 컴포지션 API
API 옵션의 로직을 읽기 쉽게 로직을 정리해 줄 수 있다.

  __setup()__
  - `import { 반응형-데이터 } = vue`
    - vue페키지에서 반응성을 가진 데이터를 객체 구조분해로 가져온다.
  - 활용하려는 데이터를 `반응형-데이터`에 `변수로 할당`하여 반응성을 부여한다.
  - `변수명.value`로 데이터를 호출 할 수 있다.
  - `반응형-데이터`

    __ref__
    - `ref(값)` : 데이터

    __computed__
    - `computed(() => {})` : 계산된 데이터

    __watch__
    - `watch(감시할-데이터, () => {})` : 감시할 데이터

    __mounted__
    - `onMounted() => {}` : 라이프사이클 훅

    __created__
    - `setup() {}` : 라이프사이클 훅

  __setup(props, context)__
  - 첫번째 매개변수로 `props`를 받고
  - 두번째 매개변수로 `this`를 받는다.
    - `context.속성명`으로 접근 할 수 있다.
  
  __$emit__
  - `context.emit('전달할-데이터')`로 데이터를 전달 할 수 있다.

  > js
  ```js
  <script>
    import { ref } from 'vue' // 반응성 데이터 가져오기 

    export default {
      setup() {
        let 데이터명 = ref(값)
        function 함수명() {
          데이터명.value // 데이터 접근
        }
      }

      return {
        데이터명,
        함수명
      }
    }
  </script>
  ```

  > [라이프사이클 훅 →](https://v3.ko.vuejs.org/guide/composition-api-lifecycle-hooks.html)

***

## CRUD

  - Read : 조회
  - Create : 추가
  - Update : 수정
  - Delet : 삭제

***

## API method 방식 
기능 적으로는 `POST`방식만 사용해도 되지만 명시적으로 `RESTFULL`하게 작성 해야한다.

  - GET : 읽기
  - POST : 쓰기
  - PUT : 수정
  - DELETE : 삭제

> 하나의 API를 생성하여 재사용 한다.

***

## API 레퍼런스

### Vue 인스턴스 속성

  __$refs__
  - DOM요소에 직접 접근하여 엘리먼트를 제어한다.
  - 컴포넌트 메소드 영역에서 요소를 지칭하는 ref속성을 참조하여 데이터를 사용 할 수 있다.
    - `<input ref="데이터이름">` html 요소에 `ref속성` 지정  
    - `this.$refs.데이터이름` js 컴포턴트 메소드 영역에서 `$refs` 속성으로 html `ref속성` 참조

  __$attrs__
  - 부모 컴포넌트 속성 상속

### Vue 인스턴스 메서드

  __$nextTick()__
  - setTimeOut()과 같은 기능
  - 반응형 데이터의 변경사항이 생겼을 때 화면 갱신 후 처리를 지정 할 수 있다.
  - 콜백 함수 패턴으로 사용 할 수 있지만 `$nextTick()`은 프로미스 인스턴스를 반환한다. 따라서 명시적으로 비동기 패턴을 지정하여 사용 할 수 있다.

***

## Teleport
컴포넌트를 원하는 html테그 구조에 이동시킬 수 있다.

> html
```html
<Teleport to="css선택자"> ... </Teleport>
```
- 해당 html테그 마지막 자식요소로 밀어 넣는다

***

## 플러그인
플러그인은 Vue 전역에 기능을 추가하는 방식이다.  
플러그인 생성시 이름 앞에는 `$`를 붙인다.  
ex)`$이름`

  __플러그인 생성__
  > 플러그인.js
  ```js
  export default {
    // install 플러그인 설치 메소드
    install: (app, options) => { 
      // 플러그인 코드는 여기에
      // globalProperties : 전역 맴버를 등록할 수 있다.
      app.config.globalProperties.$플러그인명 = () => {
        ...
      }
    }
  }
  ```

  __플러그인 연결__
  > main.js
  ```js
  import { createApp } from 'vue'
  import 플러그인명 from './주소'
  import App from './App.vue'

  createApp(App)
    .use(플러그인명) // 플러그인 연결
    .mount('#app')
  ```

  > [플러그인 작성하기 →](https://v3.ko.vuejs.org/guide/plugins.html)  
  > [애플리케이션 설정 →](https://v3.ko.vuejs.org/api/application-config.html)

  __플러그인 사용__
  - `$플러그인명`을 호출 하여 전역에서 사용 할 수 있다.

***