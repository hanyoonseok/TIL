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
dotenv는 환경변수를 파일에 저장할 수 있도록 해주는 모듈이다.    
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
