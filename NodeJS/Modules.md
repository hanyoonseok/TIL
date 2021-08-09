# Express  
> Express는 node.js로 서버를 만드는 웹 framework.    
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
> mysql2는 mysql을 async/await 방식으로 구현할 수 있도록 해주는 모듈이다. mysql 모듈은 async/await 방식의 사용이 불가하기 때문에 async/await를 mysql에 사용하고자 한다면 mysql2 모듈을 설치해야한다.    
### 설치  
`npm install mysql2`    
### 시작
로컬환경에 mysql이 설치되어있다는 가정하에 시작한다.      

# dotenv  
> dotenv는 환경변수를 파일에 저장할 수 있도록 해주는 모듈이다. .env파일은 key=value의 형태로 이루어져있어야 하고, `gitignore`에 `.env` 나 `*.env`를 추가하여 환경변수의 노출을 방지할 수 있다.    
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
> 이미지는 보통 input[type=file] 태그와 form 태그를 통해서 업로드되고, 이때 form의 method는 post, 인코딩 타입은 multipart/form-data로 되어있어야 한다.  
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
> `nanoid`는 랜덤 문자열을 생성해주는 라이브러리이다. UUID보다 빠르다는 장점이있다.    
### 설치  
`npm install nanoid`    
### 시작  
```javascript
const {nanoid} =require('nanoid')
const randomstring = nanoid(10) //길이가 10인 랜덤문자열 생성
console.log(randomstring)
```
      
# moment  
> `moment`는 날짜 데이터들을 아주 유연하게 변경 및 비교, 계산까지 해주는 모듈이다.    
### 설치
`npm install moment`    
### 시작  
```javascript
const moment = require('moment')
moment() // Tue Oct 03 2021 14:41:08 GMT+0900
//형식 지정
moment().format('YYYY-MM-DD HH:mm:ss') //2021-08-15 14:41:08
```  
[참고](http://devstory.ibksplatform.com/2018/01/nodejs-momentjs.html)
      
# jsonwebtoken
> 선택적 서명 및 선택적 암호화를 사용하여 데이터를 만들기 위한 인터넷 표준이다.  
### 설치
`npm install jsonwebtoken`    
### 사용 이유
1. 사용자가 자신의 비밀 값으로 서버에 로그인하게 되면, 서버는 jwt를 리턴. token을 인증값으로 사용하여 보안 이슈를 막을 수 있음.
2. 인코딩된 사이즈가 작아서 http와 html 환경에서 사용하기 좋음.
3. JSON parser는 대부분의 프로그래밍이 지원하기 때문에 만들기 쉬움.    
### 사용법
```javascript
const jwt = require('jsonwebtoken')

//토큰 생성
const token = jwt.sign({sub:'uuid'}, 'secret_key');

//decoding
const decoded = jwt.verify(token, 'secret_key');
console.log(decoded.sub) //실행결과:'uuid'
```    
### 옵션
`expiresIn`옵션으로 만료시간을 정할 수 있다.
```javascript
const token = jwt.sign(payload,'secret_key',{
  expiresIn:24h
}) //expires In 24 hours
```
      
# session
> 자주 변하는 데이터를 저장해주는 서버 사이드의 데이터 저장 방식. 쿠키와 달리 서버에 데이터를 저장하고 웹 브라우저는 session id만을 가지고 있기 때문에 쿠키보다 안전함.    
### 설치
`npm install express-session`  
express-session만으로는 제대로 된 기능 제공할 수 없음. mysql을 저장소로 하는 `express-mysql-session`도 깔아주어야 함  
`npm install express-mysql-session`    
### 시작
```javascript
const app = express()
const session = require('express-session')
app.use(session({
  secret:'sessionsecret' //반드시 필요한 옵션. 세션을 해당 값으로 암호화
  resave:false, //세션이 변경되지 않아도 계속 덮어쓰기 됨. default 값은 true이나, false를 권장
  saveUninitialized:true, //세션이 저장되기 전에 uninitialized 상태로 미리 만들어 저장
})
```    
### 사용
`req.session.세션명 = 세션value`  

```javascript
//세션 생성
router.post('/', (req,res)=>{
  req.session.userid = req.body.id
  console.log(req.session.userid)
})

//세션 삭제
req.session.destroy((err)=>{
  //여기선 session에 접근 불가
})

//세션 저장
req.session.save((err)=>{
})
```    
### 예시
```javascript
//로그인 api
var sess = req.session;
...
sess.username = req.body.username;
```
      
# redis
> session 데이터를 저장하는 곳. express-session을 사용할 때 session값을 메모리 스토어에 저장하는데 이는 서버를 재시작하면 저장된 내용들이 모두 날아감. 때문에 서버를 재시작해도 데이터를 유지할 수 있는 방법을 찾아야 함. 레디스는 데이터베이스라서 데이터도 어느 정도 유지되고, 데이터를 불러올 때 메모리에 로드해서 속도가 빠름.
### 설치
`npm install redis`  
redis와 express-session을 연결해주는 `connect-redis`또한 추가적으로 설치해줘야 한다.  
`npm install connect-redis`  
### 시작
```javascript
const express = require('express')
const session = require('session')
const redis = require('redis')
const connectRedis = require('connect-redis')

const client = redis.createClient({host:'localhost', port:6379})
const redisStore = connectRedis(session)

//세션의 저장소로 지정
app.use(session({
  ... //session option
  ,store:new redisStore({
    client
    })
}))
```     
서버쪽 우분투 접속 후  

```
//설치
sudp apt-get update
sudo apt-get install redis-server

//시작
redis-server

//redis 기본포트 확인 
netstat -npat | grep redis 

//접속확인
redis-cli 
set keys values
keys * 

//외부접속허용설정
/etc/redis/redis.conf 에 접속하여 
bind 127.0.0.1 -> bind 0.0.0.0 으로 수정
```
