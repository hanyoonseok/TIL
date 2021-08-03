# Express  
Express는 node.js로 서버를 만드는 웹framework.    
### 설치  
`npm install express`    
### 시작  
```javascript
const express = require('express')
const app = express()

app.set("port", 5000) //port를 5000번으로 설정
app.listen(port, ()=>{
  console.log('server is running on port ${app.get("port")})
})
```      

# mysql2  
mysql2는 mysql을 async/await 방식으로 구현할 수 있도록 해주는 모듈이다. mysql 모듈은 async/await 방식의 사용이 불가하기 때문에 async/await를 mysql에 사용하고자 한다면 mysql2 모듈을 설치해야한다.    
### 설치  
`npm install mysql2`    
### 시작
로컬환경에 mysql이 설치되어있다는 가정하에 시작한다.      

# dotenv  
dotenv는 환경변수를 파일에 저장할 수 있도록 해주는 모듈이다. .env파일은 key=value의 형태로 이루어져있어야 하고, `gitignore`에 `.env` 나 `*.env`를 추가하여 환경변수의 노출을 방지할 수 있다.    
### 설치  
`npm install dotenv`    
### 시작  
```javascript
//./src/config/config.env
DB_HOST=localhost
DB_PASS=1234
DB_USER=root
DB_PORT=3306
DB_DATABASE=test
```  
```javascript
//app.js
const express = require('express')
require('dotenv').config({path:'./src/config/config.env'})
const db = require('./src/models/index')
```  
**app.js에서 dotenv를 다른 경로보다 상단에 선언해주어야 에러가 발생하지 않는다**  
```javascript
const development={
  username:process.env.DB_USER,
  password:process.env.DB_PASS,
  database:process.env.DB_DATABASE,
  host:process.env.DB_HOST,
  port:process.env.DB_PORT,
}
```  
**다른경로의 .env 파일을 사용하고싶다면 `require('dotenv').config({path:'경로'})` 를 선언 후 사용하면된다.**      

# multer  
이미지는 보통 input[type=file] 태그와 form 태그를 통해서 업로드되고, 이때 form의 method는 post, 인코딩 타입은 multipart/form-data로 되어있어야 한다.  
`<form name="questionForm" method="post" enctype="multipart/form-data" action="/test/save">`.  
express는 사용자가 업로드한 파일을 받아서 저장하는 기본 기능을 제공하지 않기 때문에 이를 관리하기 위해서는 별도의 모듈을 사용해주어야 한다. `multer`는 multipart/form-data로 들어온 이미지를 처리하는 모듈로, 지정한 곳에 이미지 저장이 가능하다. 클라이언트로부터 전달받는 데이터에 파일이 포함되는 경우, req 객체에 file 속성이 추가된다. 파일이 여러개라면 files 속성이 추가된다.    
### 설치  
`npm install multer`    
### 시작  
```javascript
const multer = require('multer')
```    
### 옵션  
Key|Description
:--:|:--:
`dest` or `storage`|파일이 저장될 위치
`fileFilter`|어떤 파일을 허용할지 제어하는 함수
`limits`|업로드된 데이터의 한도
`preservePath`|파일의 base name 대신 보존할 파일의 전체 경로
  
[참고1](https://velog.io/@new_wisdom/Node.js-11-Multer)  
[참고2](https://junspapa-itdev.tistory.com/27)      

# nanoid  
`nanoid`는 랜덤 문자열을 생성해주는 라이브러리이다. UUID보다 빠르다는 장점이있다.
### 설치  
`npm install nanoid`    
### 시작  
```javascript
const {nanoid} =require('nanoid')
const randomstring = nanoid(10) //길이가 10인 랜덤문자열 생성
console.log(randomstring)
```    
