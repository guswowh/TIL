# Vue 문법


## 반응성(Reactivity)
  - 데이터를 갱신하면 화면도 같이 갱신 되는 것을 말한다.


## 구조
  - template : html
    - 자식요소로 템플릿을 추가 할 수 있다
    - 최상위 요소 템플릿에 v-if는 사용 할 수 없다.
    ```
    <template>
      {{ 변수명 }}
    </template>
    ```
  - script : javaScript
    ```
    <script>
      export default {
        name: 'App',
        data() {
          return {
            변수명: "값"
          }
        } 
      }
    </script>
    ```
  - style : css, scss
    - 옵션
      - scoped : 부여된 컴포넌트의 값이 고유해 진다.
      - lang : scss


## 어플리케이션 & 컴포넌트 인스턴스
  - Vue.createApp
    - 어플리케이션 인스턴스 생성하기
    > main.js
    ```
    // 컴포넌트
    const App = { // 최상위 컴포넌트
      ...
    }
    
    app.createApp.mount('#app') // 앱 생성 후 html 요소 연결
    ```
  - 템플릿 refs
    - ref 속성을 이용해 레퍼런스 ID를 자식 컴포넌트나 HTML 요소에 부여함으로써 직접 접근할 수 있다

      문법 | 설명
      --|--
      `<tag ref="이름">` | html
      `this.$refs.이름` | js

  - $nextTick
    - javaScript setTimeout과 같은 기능

  - 라이프 사이클
    - Vue 인스턴스나 컴포넌트가 생성되고 소멸되기까지의 단계

  - 라이프 사이클 훅
    - 라이프 사이클의 각 단계에서 실행되는 함수들
      - beforeCreate()
        - 컴포넌트가 생성되기 직전에 실행 
        - 활용도 떨어짐
      - created()
        - 컴포넌트가 생성된 직후에 실행
        - 활용도 높음
      - beforMount()
        - 컴퍼넌트가 html에 연결 되기 직전에 실행
        - 활용도 떨어짐
      - mounted()
        - 컴퍼넌트가 html에 연결 된 후 실행
        - 활용도 높음


## 템플릿 문법
### 보간법(Interpolatin)
- 이중 중괄호(Mustache)는 데이터를 html이 아닌 텍스트로 해석
```
<span>메시지: {{ 구문 or 표현식 }}</span>
```

### 원시 html
  - html 구문을 분석해서 html 구조로 삽입
  - XSS 보안에 취약

### 디렉티브(Directive)
  - 속성
    - v-fi : 조건문 : 조건이 `true`일때 화면에 렌더링 한다.
      - v-else
      - v-else-if
    - v-show : 조건이 `true`일때 css 속성으로 `display: block`
    - v-for : 반복문
      - key : 데이터를 참조할 수 있는 고유 id 값(필수)
        - 한번 읽은 key의 데이터는 다시 렌더링하지 않고 재사용 한다
    - v-one : 한번만 화면에 렌더링
    - v-html : html구조를 추가할 수 있다
    - v-bind:속성="값" : html 속성을 추가 할 수 있다.
    - v-on:키수식어 : javaScript Event Listener
      - keydown.키코드
    - v-model="데이터" : 양방향 데이터 바인딩
      - 수식어
        - lazy : 값이 입력되고 나서 데이터 갱신
        - number : 숫자 데이터로 형변환
        - trim : 문자열 앞에 공백 출력을 제거한다.

  - 약어
    - :속성 : v-bind
    - @ : v-on

  - 동적 전달인자
    - 자바스크립트 객체의 "컴퓨티드 프로퍼티(계산된 프로퍼티)"


## Data 속성과 Methods
  - data
    - 반응형 데이터, 지정하고자 하는 반응성을 가진 데이터를 정의

  - methods
    - 함수 그룹
    - 변수로 정의 할 경우 반응형 데이터에 접근 할 수 없다
    - 반응형 데이터에 접근 하기위해선 `this`로 참조하여 사용 해야 한다. 


## Computed 속성과 Watch
  - computed
    - 원본 반응형 데이터를 참조하여 계산한 새로운 데이터
    - 속성처럼 사용
    - computed 속성은 기본적으로 getter를 갖는다.
      - getter & setter
        - computed 속성 안에서 `get()`, `set()`을 사용 할 수 있다.

    - Computed 속성의 캐싱 vs 메서드
      - Computed 속성은 계산된 데이터를 캐싱하여 사용하여 한번 계산된 데이터를 재사용 한다.
      - Methods의 함수들은 호출 될 때마다 계산하여 사용한다.

  - watch
    - 반응형 데이터의 기존 값과 변한 값을 감지하여 __첫번째 인수로 변한 값__, __두번째 인수로 기존값을 받는다__
    - [옵션 →](https://v3.ko.vuejs.org/api/options-data.html#watch)

  - props
  - emits


## 클래스와 스타일 바인딩
### HTML 클래스 바인딩
  - 객체 구문
    - `v-bind:class`에 객체를 전달하여 클래스를 동적으로 전환 할 수 있다.
      ```html
      <div :class="{ active: truthy }"></div>
      ```
      - isActive가 truthy일 경우 active속성이 붙는다.

  - 배열 구문
    - 배열을`:class`에 전달하여 클래스 목록을 적용할 수 있다.
      > html
      ```html
      <div :class="[activeClass, errorClass]">
      ```
      > js
      ```js
      data() {
        return {
          activeClass: 'active',
          errorClass: 'error'
        }
      }
      ```

  - 컴포넌트에서 사용하기
    - 

### 인라인 스타일 바인딩
  - 객체 구문
    - `v-bind:style`에 객체 프로퍼티의 속성을 전달하여 적용할 수 있다.
    - 자바스크립트의 객체
    - 카멜 케이스 또는 케밥 케이스로 사용할 수 있다
      > html
      ```html
      <div :style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
      ```
      > js
      ```js
      data() {
        return {
          activeColor: 'red',
          fontSize: 30
        }
      }
      ```
  - 배열 구문
    - `:style`의 배열 구문으로 사용하면, 동일한 요소에 여러 스타일 객체를 적용 할 수 있다.
    - 기존 작성되어 있는 스타일을 뒤에 작성된 스타일과 같다면 덮어 쓴다.
      > html
      ```html
      <div :style="[baseStyle, overridingStyles]"></div>
      ```


## 조건부 렌더링
### v-if
  - 디렉티브 조건에 따라 블록을 렌더링 할 때 사용
  - 블록은 디렉티브의 표현식이 `true`값을 반환할 때만 렌더링 된다.
    > html
    ```html
    <h1 v-if="awesome">awesome이 true면 렌더링 </h1>
    ```
  - 렌더링할 html 테그 요소가 여러개 일때 `<template>`테그로 묶어 준다.
    ```html
    <template v-if="ok">
      <h1>Title</h1>
      <p>Paragraph</p>
      <p>Paragraph</p>
    </template>
      ```
  - v-else
    - v-if 조건이 false일때 렌더링
  - v-else-if
    - v-if 조건이 false일때 조건을 비교한다.
### v-show
  - 렌더링하고 조건에 따라 CSS display 속성을 전환한다.


## 리스트 렌더링
### v-for로 엘리먼트에 배열 매핑하기
  - v-for 디렉티브를 사용하여 배열의 리스트를 렌더링 할 수 있다.

    문법 | 설명
    --|--
    v-for="item in items" | items는 원본 데이터 배열, item은 배열 엘리먼트의 별칭

    > html
    ```html
    <ul id="array-rendering">
      <li v-for="item in items">
        {{ item.message }}
      </li>
    </ul>
    ```
    > js
    ```js
    Vue.createApp({
      data() {
        return {
          items: [{ message: 'Foo' }, { message: 'Bar' }]
        }
      }
    }).mount('#array-rendering')
    ```
### v-for와 객체
  - v-for를 사용하여 객체의 속성을 반복할 수도 있습니다.
    > html
    ```html
    <ul id="v-for-object" class="demo">
      <li v-for="value in myObject">
        {{ value }}
      </li>
    </ul>
    ```
    > js
    ```js
    Vue.createApp({
      data() {
        return {
          myObject: {
            title: 'How to do lists in Vue',
            author: 'Jane Doe',
            publishedAt: '2016-04-10'
          }
        }
      }
    }).mount('#v-for-object')
    ```
### 상태 유지
  - 각 노드의 id를 추적하여, 재사용하거나 순서를 변경하는 등의 작업을 위해 각 아이템에 유일한 `key` 속성을 필수로 준다.
  - `key`속성이 없을 경우 속성이 겹치는 경우 다른 데이터일지라도 같은 데이터로 판단한다.
    > html
    ```html
    <div v-for="item in items" :key="item.id">
      <!-- content -->
    </div>
    ```
  
  
### 필터링/정렬된 결과 표시
  - 원본 데이터를 실제로 변경하거나 재설정하지 않고 `computed`속성을 사용하여 원하는 형태로 변환하여 새로운 계산된 데이터를 반환할 수 있다.
    > html
    ```html
    <li v-for="n in evenNumbers">{{ n }}</li>
    ```
    > js
    ```js
    data() {
      return {
        numbers: [ 1, 2, 3, 4, 5 ]
      }
    },
    computed: {
      evenNumbers() {
        return this.numbers.filter(number => number % 2 === 0)
      }
    }
    ```

### `<template>`에서의 v-for
  - 템플릿의 v-if와 마찬가지로, v-for와 함께 `<template>`태그를 사용하여 여러 요소의 블록을 렌더링 할 수 있다.
    > html
    ```html
    <ul>
      <template v-for="item in items">
        <li>{{ item.msg }}</li>
        <li class="divider" role="presentation"></li>
      </template>
    </ul>
    ```

### v-if가 있는 v-for
  - v-if와 v-for를 함께 사용하는 것은 권장되지 않습니다. 자세한 내용은 [스타일 가이드](https://v3.ko.vuejs.org/style-guide/#avoid-v-if-with-v-for-essential)를 참조하세요.
  - 동일한 노드에 있는 경우, v-if는 v-for보다 우선 순위가 높다.
  - v-if 조건은 v-for 범위의 변수에 접근할 수 없다.
    > html
    ```html
    <!-- This will throw an error because property "todo" is not defined on instance. -->

    <li v-for="todo in todos" v-if="!todo.isComplete">
      {{ todo }}
    </li>
    ```
  - v-for를 래핑(wrapping)하는 `<template>`태그를 사용하면 문제를 해결할 수 있다.
    > html
    ```html
    <template v-for="todo in todos">
      <li v-if="!todo.isComplete">
        {{ todo }}
      </li>
    </template>
    ```


## 이벤트 핸들링
### 이벤트 청취
  - v-on디렉티브는 @기호로, DOM 이벤트를 듣고 트리거 될 때와 JavaScript를 실행할 때 사용한다.
  - v-on:click="methodName" 나 줄여서 @click="methodName"으로 사용한다.
    > html
    ```html
    <div id="basic-event">
      <button @click="counter += 1">Add 1</button>
      <p>The button above has been clicked {{ counter }} times.</p>
    </div>
    ```
    > js
    ```js
    Vue.createApp({
      data() {
        return {
          counter: 1
        }
      }
    }).mount('#basic-event')
    ```

### 복합 이벤트 핸들러
  - 이벤트 핸들러 안에서 복합 메소드를 지정할 수 있습니다.
    > html
    ```html
    <!-- one()과 two() 둘다 버튼 클릭 이벤트를 실행할 수 있습니다.-->
    <button @click="one($event), two($event)">
      Submit
    </button>
    ```
    > js
    ```js
    // ...
    methods: {
      one(event) {
        // 첫번째 핸들러 로직...
      },
      two(event) {
        // 두번째 핸들러 로직...
      }
    }
    ```
    - $event : 인수가 필요하다면 명시적으로 사용 할 수 있다.

### 이벤트 수식어
  - 이벤트 동작을 제어 하기위한 이벤트 수식어

    - .stop : 이벤트 버블링 정지
    - .prevent : 기본동작 방지
    - .capture : 이벤트 켑처링 정지
    - .self : 정확히 자신의 영역을 선택해야 동작
    - .once : 한번만 동작
    - .passive : 화면을 움직이는 동작과 로직이 움직이는 동작을 분리 한다.

### 키 수식어
  - 키보드 이벤트를 청취할 때, 공동 키 코드를 캡처 한다.
    > html
    ```html
    <!-- 키가 'Enter'일때만 `vm.submit()`을 호출할 수 있습니다.-->
    <input @keyup.enter="submit" />
    ```
  - [KeyboardEvent.key](https://developer.mozilla.org/en-US/docs/web/api/ui_events/keyboard_event_key_values)를 통해 노출된 유효 키 이름을 케밥 케이스로 변환하여 수식어로 사용할 수 있다.
    > html
    ```html
    <input @keyup.page-down="onPageDown" />
    ```

  - 흔히 사용되는 키 명령어
    - .enter
    - .tab
    - .delete (“Delete” 와 “Backspace” 키 모두를 캡처합니다)
    - .esc
    - .space
    - .up
    - .down
    - .left
    - .right

  - 시스템 수식어 키목록
    - 다음 수식어를 사용해 해당 수식어 키가 눌러진 경우에만 마우스 또는 키보드 이벤트 리스너를 트리거 할 수 있습니다:
      - .ctrl
      - .alt
      - .shift
      - .meta : 동작을 명확하게 보장하지 않는다.

  - .exact 수식어
    - 다른 시스템 수식어와 조합해 그 핸들러가 실행 되게 한다.
      ```html
      <!-- 아래코드는 Alt 또는 Shift와 함께 눌렀을 때도 실행됩니다.-->
      <button @click.ctrl="onClick">A</button>

      <!-- 아래코드는 Ctrl키만 눌려져 있을 때 실행됩니다.-->
      <button @click.ctrl.exact="onCtrlClick">A</button>

      <!-- 아래 코드는 시스템 키가 눌리지 않은 상태인 경우에만 작동합니다.-->
      <button @click.exact="onClick">A</button>
      ```

  - 마우스 버튼 수식어
    - .left
    - .right
    - .middle


## 데이터 바인딩
  - 데이터 바인딩 이란 두 데이터 혹은 정보의 소스를 모두 일치시키는 기법이다. 즉 화면에 보이는 데이터와 브라우저 메모리에 있는 데이터를 일치시키는 기법이다.

### 단방향 데이터 바인딩
  - Event를 통해서만 코드 상 변수에 데이터 값이 담긴다.

### 양방향 데이터 바인딩
  - 사용자의 입력값이 곧바로 코드 상의 변수에 바인딩 한다.


## 폼 입력 바인딩
  - v-model 디렉티브를 사용하여 input, textarea, select 요소들에 양방향 데이터 바인딩을 생성할 수 있습니다. 
  - IME (opens new window)(중국어, 일본어, 한국어 등)가 필요한 언어의 경우 IME 중 v-model이 업데이트 되지 않습니다. 이러한 업데이트를 처리하려면 __input 이벤트__ 를 대신 사용하십시오.

### 기본사용법
#### 문자열
  > html
  ```html
  <input v-model="message" placeholder="여기를 수정해보세요" />
  <p>메시지: {{ message }}</p>
  ```

#### 여러 줄을 가진 문장
  > html
  ```html
  <span>여러 줄을 가지는 메시지:</span>
  <p style="white-space: pre-line;">{{ message }}</p>
  <br />
  <textarea v-model="message" placeholder="여러줄을 입력해보세요"></textarea>
  ```

#### 체크박스
  - 하나의 체크박스는 단일 boolean 값을 가집니다.
  > html
  ```html
  <input type="checkbox" id="checkbox" v-model="checked" />
  <label for="checkbox">{{ checked }}</label>
  ```

#### 라디오
  > html
  ```html
  <div id="v-model-radiobutton">
    <input type="radio" id="one" value="One" v-model="picked" />
    <label for="one">One</label>
    <br />
    <input type="radio" id="two" value="Two" v-model="picked" />
    <label for="two">Two</label>
    <br />
    <span>Picked: {{ picked }}</span>
  </div>
  ```
  > js
  ```js
  Vue.createApp({
    data() {
      return {
        picked: ''
      }
    }
  }).mount('#v-model-radiobutton')
  ```


### 수식어
#### .lazy
  - 입력을 완료 해야 반영 된다.
    - 인라인 사용시 @input을 @change로 변경
    > html
    ```html
    <!-- "input" 대신 "change" 이후에 동기화 됩니다. -->
    <input v-model.lazy="msg" />
    ```

#### .number
  - 사용자 입력이 자동으로 숫자로 형변환
  > html
  ```html
  <input v-model.number="age" type="number" />
  ```

#### .trim
  - 사용자가 입력한 내용에서 자동으로 앞뒤 공백을 제거
  > html
  ```html
  <input v-model.trim="msg" />
  ```

## 컴포넌트 기초
### 전역 등록
  - 구조
  > js
  ```js
  // Vue 애플리케이션 생성
  const app = Vue.createApp({})

  // button-counter라는 새로운 전역 컴포넌트 정의
  app.component('button-counter', {
    data() {
      return {
        count: 0
      }
    },
    template: `
      <button>
        You clicked me {{ count }} times.
      </button>`
  })
  ```
  - 컴포넌트 재사용
    - 컴포넌트는 얼마든지 반복해서 재사용 할 수 있다.
    > html
    ```html
    <div id="components-demo">
      <button-counter></button-counter>
      <button-counter></button-counter>
      <button-counter></button-counter>
    </div>
    ```

### 지역 등록
  - 컴포넌트 구성하기
  > js
  ```js
  const app = Vue.createApp({})

  app.component('my-component-name', {
    // ... 옵션들 ...
  })
  ```
  ```js
  const options = {
    // ... 옵션들 ...
  }

  const app = Vue.createApp({})
  app.component('my-component-name', options)
  ```
#### Props를 이용해 자식 컴포넌트에게 데이터 전달하기
  - props
    - 컴포넌트에 등록할 수 있는 커스텀 속성입니다.
    - 값이 prop 속성에 전달되면, 그 값은 해당 컴포넌트 인스턴스의 속성이 됩니다.

    > js
    ```js
    const app = Vue.createApp({})
    app.mount('#blog-post-demo')

    app.component('blog-post', {
      props: ['title'],
      template: `<h4>{{ title }}</h4>`
    })
    ```
    > html
    ```html
    <div id="blog-post-demo" class="demo">
      <blog-post title="My journey with Vue"></blog-post>
      <blog-post title="Blogging with Vue"></blog-post>
      <blog-post title="Why Vue is so fun"></blog-post>
    </div>
    ```
#### 하위 컴포넌트 이벤트 수신
  - props
    - 부모 컴포넌트가 자식 컴포넌트에게 데이터 전달 (단방향 데이터 바인딩)

  - emits
    - 자식 컴포넌트가 부모 컴포넌트에게 데이터 전달 (단방향 데이터 바인딩)
    > js
    ```js
    app.mount('#blog-posts-events-demo')
    const app = Vue.createApp({
      data() {
        return {
          posts: [
            { id: 1, title: 'My journey with Vue'},
            { id: 2, title: 'Blogging with Vue'},
            { id: 3, title: 'Why Vue is so fun'}
          ],
          postFontSize: 1
        }
      }
    })

    app.component('blog-post', {
      props: ['title'],
      template: `
        <div class="blog-post">
          <h4>{{ title }}</h4>
          <button @click="$emit('enlargeText')"> // enlargeText === @enlarge-text
            Enlarge text
          </button>
        </div>
      `
    })
    ```
    > html
    ```html
    <div id="blog-posts-events-demo" class="demo">
      <div :style="{ fontSize: postFontSize + 'em' }">
        <blog-post
          v-for="post in posts"
          :key="post.id"
          :title="post.title"
          @enlarge-text="postFontSize += 0.1"
        ></blog-post>
      </div>
    </div>
    ```
  - v-model
    - 

  - [슬롯(Slot)을 이용한 컨텐츠 제공](https://v3.ko.vuejs.org/guide/component-basics.html#%E1%84%8F%E1%85%A5%E1%86%B7%E1%84%91%E1%85%A9%E1%84%82%E1%85%A5%E1%86%AB%E1%84%90%E1%85%B3%E1%84%8B%E1%85%A6%E1%84%89%E1%85%A5-v-model-%E1%84%89%E1%85%A1%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5)
    - HTML 엘리먼트와 마찬가지로 다음과 같이 컨텐츠를 컴포넌트에 전달할 수 있다
      > html
      ```html
      <alert-box>
        Something bad happened.
      </alert-box>
      ```
      > js
      ```js
      app.component('alert-box', {
        template: `
          <div class="demo-alert-box">
            <strong>Error!</strong>
            <slot></slot>
          </div>
        `
      })
      ```
  - 동적 컴포넌트
    - keep-alive를 사용하는 동적 컴포넌트
    
- 재사용성 & 컴포지션
  - Teleport


# 컨포넌트 톺아보기

## Props
  - [Prop 유효성 검사](https://v3.ko.vuejs.org/guide/component-props.html#prop-%E1%84%8B%E1%85%B2%E1%84%92%E1%85%AD%E1%84%89%E1%85%A5%E1%86%BC-%E1%84%80%E1%85%A5%E1%86%B7%E1%84%89%E1%85%A1)
   

















## 컴포넌트
  - Vue 컴포넌트는 Vue 인스턴스이기도 합니다. 그러므로 모든 옵션 객체
  - 기본 HTML 엘리먼트를 확장하여 재사용 가능한 코드를 캡슐화하는 데 도움

## data
  - 컴포넌트의 data 옵션은 함수입니다. Vue는 새로운 컴포넌트 인스턴스 생성의 일환으로 data 함수를 호출

## Methods
  - 컴포넌트 인스턴스에 메서드를 추가하려면 methods 옵션을 사용하세요. methods 옵션은 동작하기를 원하는 메서드들이 담긴 하나의 객체여야 합니다.

## computed
  - 메소드와 달리 컴퓨티드는 케싱을 통해 한번 개산된 데이터를 반복 사용할 수 있다.
  - 컴퓨티드는 기본적으로 값을 받아 오기만 가능하나 옵션을 통하여 
    - getter, setter
      - get()
      - set()
  
## 라이프 사이클 훅

  - beforeCreate()
    - 컴포넌트가 생성되기 직전에 실행 
    - 활용도 떨어짐
  - created()
    - 컴포넌트가 생성된 직후에 실행
    - 활용도 높음
  - beforMount()
    - 컴퍼넌트가 html에 연결 되기 직전에 실행
    - 활용도 떨어짐
  - mounted()
    - 컴퍼넌트가 html에 연결 된 후 실행
    - 활용도 높음

## watch
  - 특정한 데이터가 변경되는 것을 감시하여 실행한다.

## 클레스 바인딩
 

## 조건부 렌더링

## 리스트 렌더링
  - npm i -D shortid : id자동 생성 개발의존성 패키지
  - 배열 변경 감지

## 이벤트 청취
  - 이벤트 수식어 : 자바스크립트의 이벤트를 간소화하여 사용 할 수 있다.
    - stop : 버블링 켑처링 정지
    - self : 정확히 자신을 선택해야 동작
    - passive : 화면을 움직이는 동작과 로직이 움직이는 동작을 분리 한다.
    
  - 키 수식어
    - keydown : 키를 눌렀을때 동작
      - ctrl : 키 수식어
      - shift : 키 수식어
      - enter : 키 수식어
      - esc : 키 수식어
      - 기타 문자 : 키 수식어

## 폼 입력 바인딩
  - 단방향 데이터 바인딩 : 수정 후 갱신 되지 않는다.
  - 양방향 데이터 바인딩 : 수정 후 갱신 된다.

    - 인라인방식(한글 입력 방식)
      - $데이터명

    - 디렉티브 방식(영문 입력 방식)
      - v-model

## 컴포넌트
  - export default
    - props : 부모 컴포넌트와 자식 컴포넌트의 데이터 통신


## [skyPack](https://www.skypack.dev/)



에밋, 프롭스, ref $nextTick(), 