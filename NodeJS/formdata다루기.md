# Nodejs에서 formdata 다루기
> 프론트에서 보내는 form data를 파싱하기 위해서는 `body-parser`와 `multer` 필요

### 설치
```jsx
npm install multer body-parser
```

### 적용
```jsx
//nodejs app.js
const express = require('express')
const app = express()
const bodyParser = require('body-parser')
const multer = require('multer')
const formData = multer()

app.use(bodyParser.json())
app.use(bodyParser.urlencoded({
  extended:true
  })
)
app.use(formData.array());
```
- postman에서 `body` -> `form-data` 부분에 key = value 값을 넣어서 확인해본다  
[참고](https://acckolee.tistory.com/entry/Nodejs%EC%97%90%EC%84%9C-form-data-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)
