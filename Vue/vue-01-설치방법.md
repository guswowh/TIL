# Vue 설치방법

## CDN
프로토 타이핑 또는 학습목적

***

## NPM
대규모 애플리케이션을 구축할 때 권장하는 방식

***

## CLI
단일 페이지 애플리케이션을 빠르게 구축하는 방식
  - 장점 : 구성 옵션을 최대한 신경 쓰지 않고 문법에만 집중해서 프로젝트를 만들 수 있다.
  - 단점 : 세부적인 옵션들을 정리하면서 프로젝트를 관리하기는 어렵다.

> [설치 링크](https://kr.vuejs.org/v2/guide/installation.html)

***

## Webpack Template

***

## Vite Js

  __버전확인__
  > 터미널
  ```bash
  npm info vite
  ```

  __설치__
  > 터미널
  ```bash
  npm create vite@latest 폴더명
  cd 폴더명
  code . -r
  ```
  - `code . -r` : 현재 코드로 열기

  __패키지 설치__
  > 터미널
  ```bash
  npm i -D eslint eslint-plugin-vue sass
  ```

  __구성파일 설정__
  > vite.config.js
  ```js
  import { defineConfig } from 'vite'
  import vue from '@vitejs/plugin-vue'

  // https://vitejs.dev/config/
  export default defineConfig({
    plugins: [vue()],
    resolve: {
      alias: [
        { find: '~', replacement: `${__dirname}/src`}
      ]
    }
  })
  ```
  > .eslintrc.json
  ```json
  {
    "env": {
      "browser": true,
      "node": true
    },
    "extends": [
      "eslint:recommended",
      "plugin:vue/vue3-recommended"
    ],
    "rules": {
      "semi": ["error", "never"],
      "quotes": ["error", "single"],
      "eol-last": ["error", "always"],

      "vue/html-closing-bracket-newline": ["error", {
        "singleline": "never",
        "multiline": "never"
      }],
      "vue/html-self-closing": ["error", {
        "html": {
          "void": "always",
          "normal": "never",
          "component": "always"
        },
        "svg": "always",
        "math": "always"
      }],
      "vue/comment-directive": "off",
      "vue/multi-word-component-names": "off"
    }
  }
  ```

***