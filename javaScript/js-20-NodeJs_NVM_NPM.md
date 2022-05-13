# javaScript NODE.js, NVM, NPM

<br />

## - Node.js
- Chrome V8 JavaScript 엔진으로 빌드된 JavaScript 런타임  
  (프로그래밍 언어가 동작하는 컴퓨터 환경)

## - NVM(Node Version Manager)
  - 노드 버전을 관리 하는 프로그램이다.

    > 명령어
    - nvm --version : 노드 버전 확인
    - nvm install 노드버전넘버 : 노드버전 설치
    - nvm ls : 노드 버전 리스트 (ls : list)
    - nvm use 노드버전넘버 : 사용할 노드 버전
    - nvm undinstall 노드버전넘버 : 노드 버전 삭제

## - NPM(Node Package Manager)
- 전 세계의 개발자들이 만든 다양한 기능(페키지, 모듈)들을 관리하는 플렛폼

  > 명령어
  - npm init -y : npm 설치 (-y : yes) 
  - npm install 페키지명 : 페키지 설치
  - npm i : Package.json에 남아 있는 페키지 설치 내역 재설치
  - npx : Node.js파일을 실행하고 삭제한다.
      - 장점 : 데이터가 남지 않는다
      - 단점 : 실행할때 마다 다운로드 받기 때문에 속도가 느리다.  
      <br />
  - npx -p 페키지이름 실행명령어 : 페키지의 이름과 실행명령어가 다를경우

    > package.json : 현재 프로젝트의 설치된 페키지 정보(직접 관리)
    ```json
    {
      "name": "test",
      "version": "1.0.0",
      "description": "",
      "main": "index.js",
      "script": {
        "dev": "parcel index.html",
        "build": "parcel build index.html"
      },
      "keywords": [],
      "author": "",
      "license": "ISC",
      "devDependencies": {
        "parcel-bundler": "^1.12.4"
      },
      "dependencies": {
        "lodach": "^4.17.21.4"
      }
    }
    ```

    - 옵션 설명
      - main : npm 플렛폼에 업로드 할 파일
      - script : 현재 프로젝트 내부에서 사용할 스크립트 명령어  

        > 사용법
        - 개발환경 서버 실행 : "스크립트이름" : "parcel 파일명.확장자"
        - 브라우저 환경 서버 실행 : "스크립트이름" : "parcel build 파일명.확장자"
          - dist 폴터 : 웹브라우저를 동작시기기 위한 파일들의 목록이 생성되고  
          데이터를 줄이기 위해 코드가 난독화 되어 표현된다.
      <br /><br />  

      - devDependencies : 개발용 의존성 패키지
        - 개발환경에서만 동작
        <br /><br />
      - dependencies : 일반 의존성 패키지
        - 개발환경과 웹 브라우저에서 동장
      <br /><br />

    > package-lock.json : 설치된 페키지 사용에 필요한 페키지들의 정보(자동 관리)
    ```json
    {
      "name": "test",
      "version": "1.0.0",
      "lockfileVersion": 1,
      "requires": true,
      "dependencies": {
        "version": "7.12.13",
        "resolved": "",
        "integrity": "",
        "dev": true,
        "requires": {
          "@babel/highlight": "^7.12.13"
        }
      }
    }
    ```

    > node_modules : 페키지에서 설치된 모듈
      - package.json과 package-lock.js의 정보를 통하여 설치된 파일로  
        삭제해도 재설치가 가능하다

      - package.json과 package-lock.js 모듈설치 정보가 들어 있으며 삭제해선 안된다.
    <br /><br />

- Node Package
  - parcel-bundler
    - 프로젝트 빌드에 필요한 개발용 서버를 생성하는 페키지  
    <br />
    > 명령어
    - npm install parcel-bundler : dependencies에 설치
    - npm install parcel-bundler -D : devDependencies에 설치
    - npm run 스크립트이름 : 스크립트 실행
    <br /><br />

  - lodach
    - 자바스크립트 데이터를 쉽게 다룰 수 있게 해주는 라이브러리
    <br />
    > 명령어
    - npm install lodach : 페키지 설치

- gitignore
  - 파슬 번들러로 후 작업을 통하여 만들어진 파일은 따로 버전관리가 필요 하지 않아  
  깃 이그노어를 통하여 버전관리가 필요하지 않은 파일들을 처리 할 수 있다  
  <br />

  > 사용법
  1. gitignore 파일 생성
  2. 생성된 파일에 사용하지 않을 파일 작성
    - 작성법 : 파일명/
  3. 저장