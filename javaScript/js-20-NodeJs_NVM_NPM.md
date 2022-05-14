# javaScript NODE.js, NVM, NPM

<br />

## Node.js
- Chrome V8 JavaScript 엔진으로 빌드된 JavaScript 런타임  
  (프로그래밍 언어가 동작하는 컴퓨터 환경)  
  <br />

## NVM(Node Version Manager)
  - 노드 버전을 관리 하는 프로그램이다.

    명령어 | 설명
    --|--
    nvm --version | 노드 버전 확인
    nvm install 노드버전넘버 | 노드버전 설치
    nvm ls | 노드 버전 리스트 (ls : list)
    nvm use 노드버전넘버 | 사용할 노드 버전
    nvm undinstall 노드버전넘버 | 노드 버전 삭제
    <br />

## NPM(Node Package Manager)
- 전 세계의 개발자들이 만든 다양한 기능(페키지, 모듈)들을 관리하는 플렛폼

  명령어 | 설명 | 실행 후 생성 파일 및 폴더
  --|--|--
  npm init -y | npm 설치 (-y : yes) | package.json
  npm install 페키지명 | 일반 의존성 페키지 설치 | node_modules, package-look.json
  npm install 페키지명 -D | 개발 의존성 페키지 설치 | 생성폴터/파일 : node_modules, package-look.json
  npm install | Package.json에 남아 있는 페키지 설치 내역 재설치
  npm i | npm install의 축약형
  npm run 스크립트이름 | 스크립트 실행
  <br />
  
  ### 깃 허브 저장소 다운로드 명령어  
    - npx degit : 버전관리 내역이 포함되지 않은 새로운 프로잭트 다운로드
      문법 | 설명
      --|--
      npx degit 깃허브주소/저장소 다운로드받을폴더 | degit 따로 설치 하지 안아도 된다.
      npm degit 깃허브주소/저장소 다운로드받을폴더 | degit 따로 설치 해야 한다.
      <br />

  ### package.json

    - 현재 프로젝트의 설치된 페키지 정보(직접 관리)

    - 절대 삭제 해선 안됨  
    <br />
    
    > 내용 옵션 설명
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
    옵션 | 설명
    --|--
    name | 프로젝트의 이름
    version | 프로젝트 버전
    description | 프로젝트 설명
    main | npm 플렛폼에 업로드 할 파일
    script | 현재 프로젝트 내부에서 사용할 스크립트 명령어  
    keywords | 키워드
    author | 소유주
    license | 라이센스
    devDependencies | 개발용 의존성 패키지
    dependencies | 일반 의존성 패키지
    <br />

  ### package-lock.json

    - 설치된 페키지 사용에 필요한 페키지들의 정보(자동 관리)

    - 상황에 따라 삭제 가능

      - 페키지에 포함된 페키지의 버전이 다르게 설치 되서 문제가 발생할 수 있음

      - 삭제 후 재설치가 필요한 경우
        - 컴퓨터 환경이 달라져서 안되는 경우  
        <br />
  ### node_modules

    - 페키지에서 설치된 모듈
    - 삭제 후 제설치 가능

    <br /><br />

  ### gitignore
    - 파슬 번들러로 후 작업을 통하여 만들어진 파일은 따로 버전관리가 필요 하지 않아  
    깃 이그노어를 통하여 버전관리가 필요하지 않은 파일들을 처리 할 수 있다  
    <br />

    - 사용법
      1. gitignore 파일 생성
      2. 생성된 파일에 사용하지 않을 파일 작성 (작성법 : 파일명/)
      3. 저장