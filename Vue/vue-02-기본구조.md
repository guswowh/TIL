# 기본 구조

  > html
  ```html
  <template>
    <tag v-디렉티브:데이터=""></tag>
  </template>
  ```
  - html 구조를 작성 할 수 있다.  
  - 최상위 요소 템플릿은 v-if를 사용 할 수 없다.
  - 데이터 접근시 `this`는 생략할 수 있다.
    
  > js
  ```html
  <script>
    data() {
      return {
        ...
      }
    },
    computed() {

    },
    watch() {

    },
    created() {

    }
  </script>
  ```
  - 자바스크립트를 작성 할 수 있다.

  > css
  ```html
  <style scoped lang="scss">
    ...
  </style>
  ````
  - css를 작성 할 수 있다.
  - 옵션
    - scoped : 부여된 컴포넌트의 값이 고유해 진다.
      - 싱글파일 컨포는트 사용시 필수로 부여 해주어야 한다.
    - lang : scss

***

## 어플리케이션 & 컴포넌트 인스턴스

  __어플리케이션 인스턴스 생성하기__
  > 구조
  ```html
  <template>
    <tag id="id명"></tag>
  </template>

  <script>
    const 루트-컴포넌트 = {
      data() {
        return {
          ...
        }
      }
    }

    Vet.createApp(루트-컴포넌트).mount(“#id명”)
  </script>
  ```
  - 최상위 루트 컴포넌트명은 통상 "App"으로 사용한다.
  - `Vet.createApp(루트-컴포넌트)`를 `app` 변수에 담아서 사용하기도 한다.

  __최상위(Root) 컴포넌트__
  - `.creatApp(루트-컴포넌트)` : 컴포넌트 생성
  
  __`App.메소드`__
  - `.mount(#app)` : html tag 연결
  - `.component(‘컴포넌트명’, 옵션명)` : 컴포넌트 생성
  - `.use(플러그인명)` : 플러그인 사용

***

## 라이프 사이클
- Vue 인스턴스나 컴포넌트가 생성되고 소멸 되기까지의 단계를 말한다.

### 라이프사이클 훅
- 라이프 사이클의 각 단계에서 실행되는 함수들

  > 구조
  ```html
  <script>
    created() {
        ...
    }
  </script>
  ```

  __`beforeCreate() {}`__
  - 컴포넌트가 생성되기 직전에 실행 

  __`created() {}`__ : 활용도 높음
  - 컴포넌트가 생성된 직후에 실행

  __`beforMount() {}`__
  - 컴퍼넌트가 html에 연결 되기 직전에 실행
  
  __`mounted() {}`__ : 활용도 높음
  - 컴퍼넌트가 html에 연결 된 후 실행

***

## 보간법 : 이중 중괄호 구문(Mustache)
- "데이터" 또는 "함수 표현식" 사용이 가능하다.
- HTML 데이터는 일반 텍스트로 해석 된다. HTML 데이터를 출력하려면  
`v-html` 디렉티브를 사용할 수 있다.

  > 구조
  ```html
  <template>
    <tag> {{ 데이터 혹은 표현식 }} </tag>
  </template>
  ```

***

## 동적 전달인자
- `<tag v-on:[속성명]="값"></tag>`
- 데이터 옵션에 정의된 속성을 동적으로 받아와 값을 갱신할 수 있다.

  > 구조
  ```html
  <template>
    v-bind:[attr]="msg"
    v-on:[event]="add"
  </template>
  <script>
    data() {
      return {
        msg: 'active'
        attr: 'class'
        event: 'click'
      }
    }
  </script>
  ```

***

## API 옵션

### data
- 데이터는 함수여야 함다.

  > 구조
  ```html
  <script>
    data() {
      return {
        ...
      }
    }
  </script>
  ```

<br />

### computed

  __Computed 캐싱__
  - 반응형 데이터를 기준으로 계산된 데이터를 반환 한다.
  - 데이터 최적화를 위해 사용한다.
  > 구조
  ```html
  <template>
    <tag>{{ 함수명() }}</tag>
    <tag>{{ 함수명() }}</tag>
    <tag>{{ 함수명() }}</tag>
  </template>

  <script>
    data() {
      return {
        데이터명: '데이터'
      }
    },
    computed: {
      함수명() {
        return this.데이터명 ...
      }
    }
  </script>
  ```

  __Getter__
  - computed 속성에 표현된 계산식을 Getter라고 말한다.
  
  __Setter__
  - methods 속성에 정의된 값을 Setter라고 말한다.

  <br />

  > 구조
  ```html
  <template>
    <button @click="실행()">
      실행
    </button>
    <tag>{{ 함수명() }}</tag>
  </template>

  <script>
    data() {
      return {
        데이터명: 데이터
      }
    },
    computed: {
      함수명() {
        return this.데이터명 ...
      }
    },
    methods: {
      실행() {
        this.데이터명 += '새로운-데이터'
      }
    }
  </script>
  ```
  __Getter & Setter__
  > 구조
  ```html
  <template>
    <button @click="실행()">
      실행
    </button>
    <tag>{{ 함수명() }}</tag>
  </template>

  <script>
    data() {
      return {
        데이터명: 데이터
      }
    },
    computed: {
      함수명() {
        get() {
          return this.데이터명 ...
        },
        set(새로운-데이터) {
          this.데이터명 = '새로운-데이터'
        }
      }
    },
    methods: {
      실행() {
        this.함수명() += '새로운-데이터'
      }
    }
  </script>
  ```

<br />

### methods
- 일반 함수여야 한다.
- 화살표 함수에서 `this`는 자신이 선언된 함수(렉시컬) 범위 에서 정의되어 `undefined`를 출력한다.

  > 구조
  ```html
  <script>
    data() {
      return {
        데이터명: 데이터
      }
    },
    methods: {
      함수명() {
        ... return this.데이터명
      }
    }
  </script>
  ```

<br />

### watch
- 반응형 데이터의 변경사항을 감지한다.

  __매개변수__
  - `newValue` : 첫번째 매개변수로 변경후 데이터
  - `oldValue` : 두번째 매개변수로 변경전 데이터

  __옵션__
  - `deep: boolean` : 깊게 감시, 데이터의 아이템까지 변경을 감지 할 수 있다.

  > [옵션 →](https://v3.ko.vuejs.org/api/options-data.html#watch)

  > 구조
  ```html
  <script>
    watch: {
      함수명(newValue, oldValue) {
        ...
      },
      deep: true
    }
  </script>
  ```

<br />

***

## 데이터 접근

  __this.데이터명__
  - `<script>`에서 데이터에 접근하기 위해서는 `this`키워드를 사용해야 한다.  
  여기서 `this`는 해당 컨포넌트를 가리킨다.
  - this키워드가 없을 시 전역 변수

***



