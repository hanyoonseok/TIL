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
