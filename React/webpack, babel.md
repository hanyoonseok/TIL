# Webpack, Babel

### Webpack
> 모듈 번들러. 여러 개의 모듈을 하나의 파일로 묶어서 보냄으로서 네트워크 비용 낭비를 줄여줌.  
> js, css, 이미지 등 모든 것을 모듈로 봄.

**4가지 속성**
- Entry
    - 웹팩에서 웹 자원을 변환하기 위해 필요한 최초 진입점이자 자바스크립트 파일 경로.
    - `entry`를 통해서 모듈을 로딩하고 파일을 하나로 묶음.
- Output
    - 웹팩에서 `entry`로 찾은 모듈을 하나로 묶은 결과물을 반환할 위치
- Loader
    - 웹팩은 js와 json만 빌드 가능한데, 자바스크립트가 아닌 다른 자원(HTML, CSS, IMG)를 빌드할 수 있도록 도와주는 속성
    - 파일을 해석하고 변환하는 과정에 기여
- Plugin
    - 웹팩의 기본적인 동작 외 추가적인 기능을 제공하는 속성.
    - 결과물의 형태를 바꾸는 역할

### babel
> 자바스크립트 es6 문법을 es5로 변환해주는 트랜스파일러.  
> 이를 통해 react를 일반 브라우저에서도 실행시킬 수 있음.
- 개발자는 최신의 코드를 쓰면서 최대한 많은 사람들(구 버전의 브라우저를 사용하는 사람들)에게 편리한 서비스를 제공하기 위함.

**webpack, babel 설정**  
##### 1. `devDependencies`에 babel 추가
- 바벨에 여러 버전이 있는데 `preset`을 붙여서 받으면 알아서 가능 버전으로 설치됨.  
- `npm i -D @babel/core @babel/preset-env @babel/preset-react`
##### 2. 프로젝트에 `.babelrc` 파일을 만들고 코드 추가
```jsx
//.babelrc
{
  "presets": [
    "@babel/preset-env",
    "@babel/preset-react"
  ]
}
```
##### 3. 웹팩 설정
- `npm i -D webpack webpack-cli webpack-dev-server`
- `webpack`:모듈 번들러인 웹팩.
- `webpack-cli`:웹팩의 커맨드 라인 인터페이스.
- `webpack-dev-server`:개발 서버.
##### 4. 웹팩 설정파일 생성
- 프로젝트에서 `webpack.config.js`파일 생성 후 코드 작성
```jsx
//webpack.config.js
module.exports = {
  mode: 'development', // 현재 모드를 개발환경으로 설정
  entry: './src/index.js', // 애플리케이션 진입점
  output: { // 번들된 파일을 저장할 경로
    filename: 'bundle.[hash].js' // 번들된 파일의 이름. [hash]는 애플리케이션이 컴파일 될 때 웹팩에서 생성된 해시 사용.
  },
};
```
##### 5. package.json에 추가
```jsx
//package.json
...
"scripts":{
  "test": ...,
  "start":"webpack" //이 부분 추가
}
```
##### 6. loader의 사용
- `npm i -D babel-loader html-loader`
- `babel-loader`:es6를 es5로 바꿔주는 바벨을 웹팩에서 사용할 수 있게 해줌.
- `html-loader`:웹팩이 html을 읽을 수 있게 해줌.
```jsx
//webpack.config.js
module.exports={
...
}
// ...
module:{ //loader의 rules 정의
  rules:[
    { //es6 바벨 관련 loader
    test:/\.(js|jsx)$/, //빌드할 파일 확장자 정규식
    exclude:/node_modules/, //제외할 파일 정규식
    use:{
      loader: 'babel-loader', //사용할 로더 이름
      }
    },
    { //html loader
      test:/\.html$/,
      use:[
      {
        loader:'html-loader',
        options:{ //로더 옵션
          minimize:true, //코드 최적화 옵션
        },
      },
      ],
    },
  ],
},
```
##### 7. plugin 설정
- `npm i -D html-webpack-plugin`
- `html-webpack-plugin`:html 관련 plugin. 템플릿 지정하거나 favicon 설정.
```jsx
//webpack.config.js
const HtmlWebpackPlugin = require('html-webpack-plugin');
module.exports={
//..
plugins:[
  new HtmlWebpackPlugin({
    template:'public/index.html', // public/index.html로 템플릿 지정
  })
]
}
```
##### 8. 웹팩 개발서버
- `npm i -D webpack-dev-server`
```jsx
//package.json
"scripts":{
  ...
  "start":"webpack-dev-server"
}
```
```jsx
//webpack.config.js
const port = process.env.PORT || 3000;
module.exports={
  ...
  devServer:{
    host:'localhost', //개발 서버의 url
    port:port,
    open:true //서버가 실행될 때 브라우저를 자동으로 
  }
}
```
##### 9. react 코드 작성
```jsx
//public/index.html
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Webpack-for-react</title>
</head>
<body>
  <div id="root"></div>
</body>
</html>
```

[참고1](https://berkbach.com/%EC%9B%B9%ED%8C%A9-webpack-%EA%B3%BC-%EB%B0%94%EB%B2%A8-babel-%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-react-%EA%B0%9C%EB%B0%9C-%ED%99%98%EA%B2%BD-%EA%B5%AC%EC%84%B1%ED%95%98%EA%B8%B0-fb87d0027766)
[참고2](https://devlog.jwgo.kr/2018/12/03/webpack-babel-react/)
