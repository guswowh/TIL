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