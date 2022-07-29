# Reac 설치

  __node (npm), yarn 설치__
  - [mac 의 경우] brew 로 node 와 yarn 을 설치하시면 됩니다!
  ```bach
  brew update
  brew install node
  brew install yarn
  ```

  - [windows 의 경우] 직접 인스톨러를 받아서 설치해야 합니다!
    - [node 설치](https://nodejs.org/ko/download/)
    - [yarn 설치](https://classic.yarnpkg.com/lang/en/docs/install/#windows-stable)

  __react 시작__
  - 아래의 명령어를 입력하면, react 로 본격적으로 개발하기 위한 틀이 생성됩니다!
  ```bach
  yarn create react-app firstapp
  ```
  - localhost:3000 에서 아래와 같은 화면을 볼 수 있습니다!
  ```bach
  yarn start
  ```
***

# React 의 변수와 상태 (props, state)

  __component 만들어보기__
  1. src 폴더 안에 _components_ 폴더를 만들고,
그 폴더 안에 _First.js_ 를 만들어주세요!
  2. _Timer.js_ 안에서 _rfce_ 라고 입력하고 엔터를 누르면,아래와 같은 코드가 입력됩니다!  
  이것이 아까 봤던 react 함수형 컴포넌트의 가장 기본적인 형태입니다.
  ```js
  import React from 'react'

  function First() {
    return (
      <div>First</div>
    )
  }

  export default First
  ```
  3. 해당 컴포넌트를 우리가 보려면 App.js에 가서 이렇게 수정해줍시다.
  ```js
  import First from './components/First';

  function App() {
    return (
      <div>
        <First/>
      </div>
    );
  }

  export default App;
  ```

  __props 활용해보기 (비구조할당)__
  - props 는 properties 의 줄임말로, 상위 컴포넌트에서 하위 컴포넌트로 값/변수를 전달하기 위해서 사용됩니다.
  - App.js 와 Timer.js 중에서 상위 컴포넌트는 무엇일까요?
    - Timer.js 컴포넌트를 불러와서 쓰고 있는, App.js 가 상위 컴포넌트입니다!  
    그러므로 현재 상위컴포넌트는 App.js, 하위컴포넌트는 Timer.js 입니다.

  - 컴포넌트 태그 안에다가 변수명 = 값 형태로 적어주시면, 해당 변수를 그대로 해당 컴포넌트 내부에서 쓸 수 있습니다. 
    - 문자의 경우 변수명 = 문자열 ex) name=”김준태" 로 쓸 수 있고
    - 숫자의 경우 변수명 = {숫자} ex) number={5} 로 쓸 수 있습니다.
    ```js
    import First from './components/First';

    function App() {
      return (
        <div>
          <First name="김준태"/>
        </div>
      );
    }

    export default App;
    ```

  - 상위 컴포넌트에서 작성한 변수는 아래처럼 2가지 방식으로 사용할 수 있습니다.
  ```js
  import React from 'react'

  function First({name}) {
    return (
      <div>{name} First</div>
    )
  }

  export default First
  ```

  - 여러 변수를 넘길 수도 있습니다!
  ```js
  import First from './components/Timer';

  function App() {
    return (
      <div>
        <First name="조현재" number={5}/>
      </div>
    );
  }

  export default App;
  ```
  ```js
  import React from 'react'

  function First({name, number}) {
    return (
      <div>이름은 {name}, 숫자는 {number}</div>
    )
  }

  export default First
  ```
  - props 를 쓰는 것이 좋은 이유는, 하위 컴포넌트를 마치 백지수표처럼 쓸 수 있다는 점입니다!  
  틀은 유지한 채로, 값만 우리가 원하는대로 바꿔서 여러 개의 수표를 만들어 놓을 수 있는거죠!
    ```js
    import First from './components/First';

    function App() {
      return (
        <div>
          <First name="조현재" number={5}/>
          <First name="패캠최고" number={2}/>
          <First name="화이팅" number={7}/>
        </div>
      );
    }

    export default App;
    ```

  - props 를 받아올 때는, 비구조할당을 쓰는 것이 가장 좋습니다.  
  비구조할당이란 아래와 같이 변수를 분해하면서 받아오는 것을 말합니다!
    ```js
    const data = {'name': '김준태', 'number': 1}
    ```
    ```js
    const {name, number} = data
    ```
    ```js
    import React from 'react'

    function First(props) {
      const {name, number} = props

      return (
        <div>이름은 {name}, 숫자는 {number}</div>
      )
    }

    export default First
    ```

  __props 더 활용해보기 (기본값 및 타입 설정)__
  - props 를 따로 지정하지 않았을 때, 기본값을 설정하는 방법은 아래와 같습니다.
  ```js
  import React from 'react'

  function First({ name }) {
    return (
      <div>{name}</div>
    )
  }

  First.defaultProps = {
    name: '기본 이름'
  }

  export default First
  ```

  - 더 간단히 해주고 싶다면, 아래처럼 작성할 수 있습니다.
  ```js
  import React from 'react'

  function First({ name='기본 이름' }) {
    return (
      <div>{name}</div>
    )
  }

  export default First
  ```

  - 최근에는 타입스크립트가 그냥 자바스크립트보다 훨씬 더 많이 사용되는 추세인데요,  
  변수마다 타입을 미리 설정해둬서, 서비스의 안정성을 유지할 수 있기 때문입니다.

  - props 의 경우에도 타입을 지정해둘 수 있는데요, 아래처럼 사용할 수 있습니다.
  ```js
  import React from 'react'
  import PropTypes from 'prop-types';

  function First({ name }) {
    return (
      <div>{name}</div>
    )
  }

  First.propTypes = {
    name: PropTypes.string
  }

  export default First
  ```

  - name 은 문자열이라고 지정해두었습니다.  
  핵심 부분은 아래와 같습니다.
  ```js
  import PropTypes from 'prop-types';

  First.propTypes = {
    name: PropTypes.string
  }
  ```

  - proptypes 로는 아래와 같은 종류가 있습니다.
    - array : 배열
    - bool : true / false
    - func : 함수
    - number : 숫자
    - object : 객체
    - string : 문자열
    - any : 아무 종류

  - 만약 name 을 필수적으로 받아야 작동하는 컴포넌트라면?  
  아래처럼 isRequired 를 작성해서, name 이 지정되지 않은 것에 대한 경고를 띄워줄 수 있습니다!
    ```js
    import React from 'react'
    import PropTypes from 'prop-types';

    function First({ name }) {
      return (
        <div>{name}</div>
      )
    }

    First.propTypes = {
      name: PropTypes.string.isRequired
    }

    export default First
    ```

  __state 활용해보기 (onClick 이벤트)__
  - react 는 state 를 쓰지 않는 변수는 업데이트해서 표시해주지 않습니다.

  - 값이 변경될 때마다 해당 부분을 다시 표시해주도록 하려면 useState를 사용하면 됩니다.
  ```js
  const [변수명, set변수명] = useState(변수의 초기값);
  ```

  - 초기값이 0인, test 라는 state 를 만든다면, 아래처럼 만들 수 있습니다.
  ```js
  const [test, setTest] = useState(0);
  ```
    - 여기서 setTest 는 무엇일까요?  
    test 라는 state 의 값을 변경하고자 할 때 사용하는 함수라고 생각하시면 됩니다!

  - 아래처럼 작성한다면, test의 값은 1로 변하면서, react 는 해당 부분을 변경된 test의 값으로 새롭게 표시(render)해줄 것입니다!
  ```js
  setTest(1)
  ```

  - 이를 응용해서 1씩 더해지는 함수는 아래처럼 작성할 수 있습니다!
  ```js
  import React, { useState } from 'react'

  function First() {
    const [test, setTest] = useState(0);
    const countUp = () => {
      setTest(test+1);
    };

    return (
      <div>
        {test}
        <button onClick={countUp}>카운트업!</button>
      </div>
    )
  }

  export default First
  ```

***