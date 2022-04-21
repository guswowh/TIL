# css

> 선택자는 뒤에서 부터 읽는 것이 정확하게 해석 할 수 있다 특히 nth-child

<br />

- ### 전역속성
  - tabindex :	탭키를 사용하여 웹페이지를 탐색할 때 엘리먼트에 포커스가 가능한지 여부와 포커스가 잡히는 순서를 제어
  - title : 요소의 정보나 설명을 지정
  - style : 요소에 적용할 스타일(css)을 지정
  - class : 중복 가능
  - id : 중복 안됨
  - data-이름=“데이터” : 요소에 데이터를 지정

<br />

  - ### 선언방식
    - 내장방식 : `<style></style>`
    - 인라인방식 : `<태그 style=“”></태그>`
    - 링크방식 : `<link rel=“” href=“”>`
    - 임폴트방식 : `@import url(“”);`

<br />

- ### 선택자
  - 기본 선택자
    - `*` : 전체 선택자
    - tag : 태그 선택자
    - .className : 클레스 선택자
    - #idName : 아이디 선택자

<br />

- ### 복합 선택자
  - 선택자.className : 일치 선택자
  - 선택자 > 선택자 : 자식 선택자
  - 선택자 선택자 : 하위(후손) 선택자
  - 선택자 + 선택자 : 인접 형제 선택자, 다음 형제 요소 “하나”를 선택
  - 선택자 ~ 선택자 : 일반 형제 선택자, 다음 형제 요소 “모두”를 선택

<br />

- ### 가상 클랫 선택자
  - :hober : 마우스 오버 되면 선택
  - :active : 마우스 클릭 선택 때면 미선택
  - :focus : 포커스 되면 선택
    - 포커스가 될 수 있는 요소는 대화형 컨텐츠가 해당된다.
      >해당 요소 : input, a, button, label, select 등…
    - tabindex : 속성을 통해 포커스 퇼 수 있는 요소를 만들 수 있다
      >해당 요소 : 값(tabindex=“-1”) : -1 이 아닌 다른 값을 넣는 것은 논리적 흐름을 방해하기에 권장하지 않는다.
  - :first-child : 형제 요소 중 첫번째 선택자
  - :last-child : 형제 요소 중 마지막 선택자
  - :nth-child : 형제 요소 중 (n)째 선택자
    - nth-child(n) : n번째 선택
    - nth-child(nn) : n x n 번째 선택
  - :not(선택자) : 선택자가 아닌 요소를 선택

<br />

- ### 가상 요소 선택자
  - ::before : 선택 요소의 내부 “앞에” 내용을 삽입
    - 속성 : content: “내용”;
  - ::after : 선택 요소의 내부 “뒤에” 내용을 삽입
    - 속성 : content: “내용”;

<br />

- ### 속성 선택자
  - [속성이름] : 요소의 속성을 선택
  - [속성이름=“값”] : 요소의 속성과 값을 선택

<br />

- ### 스타일 상속
  - 문자속성은 부모 요소로 부터 상속 받는다 (모든 글자/문자 속성은 아님 주의!) 
  - ingerit : 강제 상속

<br />

- ### 우선순위
  1. !mportant(무한대)
  2. 인라인 선언(1000점)
  3. id 선택자(100점)
  4. Class 선택자(10점)
  5. 태그 선택자(1점)
  6. `*` 선택자(0점)
  7. 상속(X)

<br />

- ### 기본속성
  - Margin collapsing
    - 부모 자식 : 위위 마진이 만날때, 아래아래 마진 만날 때
    - 형제 형제 : 위아래 마진이 만날때
  - width, height 기본 속성
    - width/height : auto
    - max width/height : none
    - min width/height : 0
  - 인라인 요소와 블럭 요소의 너비 성질
    - inline : 글자 속성으로 가로 정렬 되며 너비는 줄어드려는 성질
    - block : 글자 속성으로 수직 정렬 되며 너비는 늘어나려는 성질
    - 단위
      - px : 픽셀
      - % : 상대적 백분율
      - em : (부모 글자의 크기) x (n)em
      - rem : (최상위 부모(html) 글자의 크기) x (n)em
      - vw : 뷰포트 가로 너비의 백분율
      - vh : 뷰포트 세로 너비의 백분율

<br />

- ### 색상표현
  - 색상 이름 :	브라우저에서 제공하는 색상 이름 (red, tomato, royalblue 등…)
  - Hex 색상코드 : 16진수 색상코드 (#000, #ffffff)
  - RGB : 빛의 삼원색 (rgb(255, 255, 255)
  - RGBA : 빛의 삼원색  + 투명도 (rgba(0,0,0,0.5)
  - HSL : 색상, 채도, 명도 (hsl(120,100%, 50%)
  - HSLA : 색상, 채도, 명도 + 투명도 (hsla(120, 100%, 50%, 0.3)

<br />

- ### border
  - border-width : 선 두깨
  - border-color : 선 색
  - border-style : 선 스타일
  - border-radius : 모서리 둥굴게

<br />

- ### box-sizing
  - 속성
    - content-box : 기본 속성
    - border-box : 컨텐츠의 패딩과 보더를 포함하지 않고 계산한다.

<br />

- ### overflow
  - 개별 속성
    - overflow-y : y축 제어
    - overflow-x : x축 제어
  - 속성
    - visible : 넘친 내용 그대로(기본 값)
    - hidden : 넘친 내용을 잘라냄
    - scroll : 넘친 내용을 잘라냄, 스크롤바 생성
    - auto : 넘친 내용이 있는 경우에만 잘라내고 스크롤바 생성

<br />

- ### display
  - 속성
    - block : 상자(레이아웃) 요소
    - inline : 글자 요소
    - inline-block : 글자 + 상자 요소
    - flex : 플렉스 박스(1차원 레이아웃)
    - grid : 그리드(2차원 레이아웃)
    - none : 없음
    - 기타 등…

<br />

- ### opacity
  - 값 : 1 (0.1~1)

<br />

- ### font
  - fiont-size : 크기
  - font-weight : 두깨
  - font-style : 글꼴 스타일
  - line-height : 행간
    - 값을 배수로 사용 권장
      > ex) line-height: 2; (font-size x2)
  - font-family : 글꼴 지정
  - color : 글자 색
  -	font-align : 문자 정렬
    - left : 왼쪽 정렬
    - right : 오른쪽 정렬
    - center : 가운데 정렬
    - justify : 양쪽 정렬
  - text-decoration : 문자의 장식
    - none : 장식 없음
    - underline : 밑줄
    - overline : 윗줄
    - line-through : 중앙 선
  - text-indent : 들여쓰기, 내어쓰기

<br />

- ### 레이아웃 구조
  - background-color : 배경색
  - background-image : 배경 이미지
    - 값 : url(“경로”)
  - background-repeat : 반복
  - background-position : 배경 위치
  - backgourne-size : 배경 크기
  - background-attachment : 배경 이미지 스크롤 특성
    - scroll : 이미지가 요소를 따라서 같이 스크롤
    - fixed : 이미지가 뷰포트에 고정, 스크롤 x
    - local : 요소 내 스크롤 시 이미지가 같이 스크롤

<br />

- ### position
  - static : 기준 없음
  - relative : 요소 자신을 기준
  - absolute : 위치 상 부모 요소를 기준
  - fixed : 뷰포트(브라우저)를 기준
  - sticky : 스크롤 영역 기준
    > 요소의 조상 중 하나가 transform, perspective, filter 속성중 어느 하나라도 none이 아니라면그 조상을커테이닝 블록으로 삼습니다.

<br />

- ### z-index
  - 값 : n

<br />

- ### display flex
  - Flex Container (부모 요소)
    - Container 속성
      - display : 디스플레이 선언
        - __flex : 블록 요소와 같이 flex container 정의__
        - inline-flex : 인라인 요소와 같이 flex container 정의
      - flex-direction : 주 축을 설정
        - __row : 행 축 (좌 > 우)__
        - __row-reverse : 행 축 (우 > 좌)(데칼코마니)__
        - column : 열 축 (위 > 아래)
        - column-reverse : 열 축 (아래 > 위)(데칼코마니)
    - Items 속성
      - flex-wrap : 묶음(줄 바꿈) 여부
        - __nowrap : 묶음(줄 바꿈) 없음__
        - __wrap : 여러 줄로 묶음__
        - wrap-reverse : wrap의 반대 방향으로 묶음
      - justify-content : 주 죽(수평 양쪽 정렬)의 정렬 방법을 설정
        - __flex-start : flex items를 시작점으로 정렬__
        - __flex-end : flex items를 끝점으로 정렬__
        - __center : flex items를 가운데 정렬__
        - space-between : 각 flex item 사이를 균등하게 정렬
        - space-around : 각 flex item의 외부 여백을 균등하게 정렬
      - align-items : 교차 축의(수직) 한 줄 정렬 방법
        - __stretch : flex items를 교차 축으로 늘림__
        - __flex-start : flex items를 각 줄의 시작점으로 정렬__
        - __flex-end : flex items를 각 줄의 끝점으로 정렬__
        - __center : flex items를 각 줄의 가운데 정렬__
        - baseline : flex items를 각 줄의 문자 기준선에 정렬
      - align-content : 교차(수직) 축의 여러 줄 정렬 방법
        > 두줄 이상일때 적용 됨
        - __stretch : flex items를 시작점으로 부터 늘려서 정렬__
        - __flex-start : flex items를 시작점으로 정렬__
        - __flex-end : flexfitems를 끝점으로 정렬__
        - __center : flex items를 가운데 정렬__
        - space-between : 각 flex item 사이를 균등하게 정렬
        - space-around : 각 flex item의 외부 여백을 균등하게 정렬
  - Flex items (자식 요소) 
    - order : item의 순서
        - (0~)부터 숫자가 작을 수록 먼저
      - flex-grow : item의 증가 너비 비율
        - (0~)부터 증가 비율
      - flex-shrink : item의 감소 너비 비율
        - (1~)부터 숫자가 높을 수록 컨테이너의 너비에 따라 감소비율 적용
          > (0)은 감소 비율이 없다는 것을 의미
      - flex-basis : 공간을 배분 하기 전에 기본 너비
        - (1~) 아이템의 컨텐츠를 증가 너비 비율 적용
          > (0)은 컨텐츠 너비가 없다
        - 다른 단위도 적용이 가능하다 px, em, rem 등…

<br />

- ### display grid
  - 속성 값
    - px, fr, repeat(개수, 단위)
  - grid Container (부모 요소)
    - grid-template-columns : 열을 명시적 지정
        - 값 : fr, px, repeat()
      - grid-auto-columns : 열을 암시적 지정
        - 값 : fr, px
      - grid-template-rows : 행을 명시적 지정
        값 : fr, px, repeat()
      - __grid-auto-rows : 행을 암시적 지정__
        - 값 : fr, px
      - __grid-gap : 거터를 지정__
        - grid-gap > gap 으로 변경될 예정 (flex와 같이 사용)
      - grid-auto-flow : 배치 하지 않은 아이템을 어떤 방식의 ‘자동 배치 알고리즘(dense)’으로 처리할지 정의
        - 값
          - row : 각 행 축을 따라 차례로 배치
          - column : 각 열 축을 따라 차례로 배치
          - __row dense : 각 행 축을 따라 차례로 배치, 빈 영역 메움__
          - __column dense : 각 열 축을 따라 차례로 배치, 빈 영역 메움__
  - grid Items (자식 요소)
    - 키워드
      - span : 현재 위치에서 셀을 늘리는 키워드
    - __grid-row: 행의 시작과 끝을 지정하는 단축 속성 __
      - 값 : 시작 라인 숫자 / 끝 라인 숫자
      - 키워드 : span
    - __grid-column: 열의 시작과 끝을 지정하는 단축 속성__
      - 값 : 시작 라인 숫자 / 끝 라인 숫자
      - 키워드 : span
      > grid-column과 grid-row는 배치 시 중첩이 가능하다
    - order : item의 순서
      - (0~)부터 숫자가 작을 수록 먼저

<br />

- ### css 상속
  - 주요 상속되는 속성
    - font
      - font-style
      - font-weight
      - font-size
      - line-height
      - font-family
    - color
    - text-align
    - text-indent
    - text-decoration
    - letter-spacing
    - opacity
  - 강제 상속
    > position은 relative(부모)요소로 부터 apsolute(자식)에게 강제 상속 된다.

<br />

- ### css 전환 효과
  - transition
    - 요소의 전환(시작과 끝) 효과를 지정하는 속성
  - 단축 속성
    - transition: 속성명 지속시간 타이밍함수 대기시간;
    - 개별 속성
      - transition-property : 전환 효과를 사용할 속성 이름
      - transition-duration : 전환 효과의 지속시간을 지정
        - 단위 : s
      - transition-timing-function : 전환 효과의 타이밍(Easing) 함수를 지정
        - __ease : 느리게 - 빠르게 - 느리게 = cubic-bezier(0.25, 0.1, 0.25, 1)__
        - __linear : 일정하게 = cubic-bezier(0, 0, 1, 1)__
        - __ease-in : 느리게 - 빠르게 = cubic-bezier(0.42, 0, 1, 1)__
        - __ease-out : 빠르게 - 느리게 = cubic-bezier(0, 0, 0.58, 1)__
        - __ease-out : 느리게 - 빠르게 - 느리게 = cubic-bezier(0.42, 0, 0.58, 1)__
        - cubic-bezier : 자신만의 값을 정의(0~1)
        - steps(n) : n번 분할된 애니메이션
      - transition-delay : 전환 효과가 몇 초 뒤에 시작할지 대기시간을 지정
        - 단위 : s
  - transform
    - 문법
      1. transform : 변환함수1 변환함수2 변환함수3…;
      2. transform : 원근법 이동 크기 회전 기울임;
    - 2D 변환 함수
      - __translate(x,y)(x)/(y) : 이동(x축, y축)__
      - __scale(x,y)/(x)/(y) : 크기(x축, y축)__
      - __rotate(deg) : 회전(각도)__
      - __skew(x,y)/(x)/(y) : 기울임(x축, y축)__
      - matrix(n,n,n,n,n,n) : 2차원 변환 효과
    - 3D 변환 함수
      - translateZ(z) : 이동(z축) : 이동(z축)
      - translate3d(x,y,z) : 이동(x축, y축, z축)
      - scaleZ(x) : 크기(z축)
      - scale3d(x,y,z) : 크기(x축, y축, z축)
      - __rotateX(x) : 회전(x축)__
      - __rotateY(y) : 회전(y축)__
      - rotateZ(z) : 회전(z축)
      - rotate3d(x, y, z, a) : 회전(x축, y축, z축, a축)
      - __perspective(n) : 원근법(거리)__
      - __blackface-visibility : 3d 변환으로 회전된 요소의 뒷면 숨김 여부__
      - matrix3d(n,n,n,n,n,n,n,n,n,n,n,n,n,n,n,n) : 3차원 변환 효과

<br />

- ### CSS 변수
	- 선언 : —변수이름: 속성
	- 호출 : 속성: var(—변수이름, 대체 값)
	  > 보통 선언은 ::root 에서 하여 전역으로 사용할 수 있게 한다.

<br />

- ### html 와 :root 의 차이점 
  - 명시도 점수의 차의가 있다.

<br />

- ### media Query
	- css 문법 : @media type and (기능) {}
		- @media type and (기능) and (기능) {}
		- @media (orientation: portrait) {} : 세로 길이가 더 길때(폰 디바이스 정방향)
		- @media (orientation: landscape) {} : 가로 너비가 더 길때(폰 디바이스 가로 방향)
	- html 문법 : `<link rel=“” href=“” media=“(기능)” />`
      - media type
      - all : 기본 값
      - screen : 화면
      - print : 프린터
  - 기능
      - max-width : 최대 너비
      - min-width : 최소 너비
      - width: 너비

<br />

- ### convention
	- 표기법
		- dash-case(kebab-case) : HTML, CSS
		- snake_case :  HTML, CSS
	- BEM(Block Element Modifier) 방법론
		- 요소__일부분 : Underscore(Lodash) 기호로 요소의 일부분을 표시
		- 요소—상태 : Hyphen(Dash) 기호로 요소의 상태를 표시