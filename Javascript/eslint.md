# Vanila JS ESlint airbnb 컨벤션 적용

1. eslint, prettier 패키지 다운
```jsx
npm i eslint --save-dev
npm i prettier -D
npm i eslint-config-prettier eslint-plugin-prettier
```
만약 `eslint-config-prettier` `eslint-plugin-prettier`가 `dependencies` 프로퍼티에 들어가있으면 `devDependencies`로 옮겨줌.

2. eslint 설정
`npx eslint --init` 혹은 `npm eslint --init`
```jsx
?How would you like to use ESLINT? -> To check syntax, find problems, and enforce code style
?What type of modules does your project use? -> Javascript modules (import/export)
?Which framework does your project use? -> None of these
?Does your project use TypeScript? -> No
?Where does your code run? -> Browser
?How would you like to defind a style for your project? -> Use a popular style guide
?Which style guide do you want to follow? -> Airbnb: https://github.com/airbnb/javascript
?What format do you want your config file to be in? Javascript
//이후 모두 yes
```

3. eslintrc.js 파일 수정 (없을 경우 생성하여 수정)
```jsx
module.exports ={
  env: {
    browser: true,
    es6: true,
  },
  extends: [
    'airbnb-base', 'plugin:prettier/recommended'
  ],
  globals: {
    Atomics: 'readonly',
    SharedArrayBuffer: 'readonly',
  },
  parserOptions: {
    ecmaVersion: 2018,
    sourceType: 'module',
  },
  rules: {
    'no-console': 'off',
    // 개인에 맞게 rule 이곳에 정의
    // prettier 정의 하려면
    'prettier/prettier': [
      'error',
      {
        singleQuote: true,
        semi: true,
        useTabs: false,
        tabWidth: 2,
        trailingComma: 'all',
        printWidth: 100,
        bracketSpacing: true,
        arrowParens: 'avoid',
        endOfLine: 'auto',
      },
    ],
  }
}
```

[참고](https://ooyuolog.tistory.com/51)

### 특정 부분만 `no-undef` 예외 처리하기
eslint가 적용된 프로젝트에서 외부 라이브러리를 가져다 쓸 때 다음과 같이 `no-undef`를 마주하게 될텐데, 이 때 eslint의 `no-undef` 옵션을 끄고싶지는 않고, 외부 라이브러리만 예외적으로 처리하고 싶을 때 사용
![제목 없음](https://user-images.githubusercontent.com/28249948/144403133-60c2632d-1d56-47df-8e13-5e6343b3cd88.png)

`.eslintrc.js` 파일에서 globals 옵션에 추가해준다.  
![캡처](https://user-images.githubusercontent.com/28249948/144403401-2c21103f-07f2-4292-bf16-f73863fb612c.PNG)
