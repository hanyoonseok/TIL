# Sequelize        
## 설치  
```javascript
npm install sequelize sequelize-cli -g    
```
<u>-g 로 글로벌 옵션을 주어야 이어지는 `sequelize init`에서 에러가 나지 않는다</u>    
## sequelize 초기화  
```javascript
sequelize init 
```
## sequelize 설정  
1.  config/config.json  
```javascript
{
  "development": {
    "username": "root",
    "password": null,
    "database": "db(스키마)이름",
    "host": "127.0.0.1",
    "dialect": "mysql"
  },
  "test": {
    "username": "root",
    "password": null,
    "database": "database_test",
    "host": "127.0.0.1",
    "dialect": "mysql"
  },
  "production": {
    "username": "root",
    "password": null,
    "database": "database_production",
    "host": "127.0.0.1",
    "dialect": "mysql"
  }
}
```  
개발시에는 `"development"`의 값을 수정하여 테스트 한다.  
`dotenv`모듈을 설치하여 config.env파일로 환경변수를 관리하여 github에의 노출을 피하고 싶다면 config.json을 config.js로 바꾸자. [바꾸는법](https://velog.io/@hyunju-song/sequelize%EB%A1%9C-DB%EC%85%8B%ED%8C%85%ED%95%A0-%EB%95%8C-%ED%99%98%EA%B2%BD%EB%B3%80%EC%88%98-%ED%8C%8C%EC%9D%BC-%EC%84%A4%EC%A0%95-%EB%B0%8F-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0 "config.js로 바꾸는 법 + dotenv 사용법")    
2.  models/index.js
```javascript
let sequelize;
if (config.use_env_variable) {
  sequelize = new Sequelize(process.env[config.use_env_variable], config);
} else {
  sequelize = new Sequelize(config.database, config.username, config.password, config);
}
```  
config.json파일의 설정값을 읽어 sequelize 객체 생성    
```javascript
fs
  .readdirSync(__dirname)
  .filter(file => {
    return (file.indexOf('.') !== 0) && (file !== basename) && (file.slice(-3) === '.js');
  })
  .forEach(file => {
    const model = require(path.join(__dirname, file))(sequelize, Sequelize.DataTypes);
    db[model.name] = model;
  });
```  
`models`폴더 아래에 존재하는 모든 js 파일을 읽어, mysql과 연결했을 때 파일명에 해당하는 테이블 생성    
3.sequelize 연결  
```javascript
//app.js에서 
const models = require("./models/index.js");

models.sequelize.sync().then( () => {
  console.log(" db connect successfully");
  
}).catch((err) => {
  console.log("fail to connect");
  console.log(err);
}
```  
`sync()`를 통해 mysql에 연결    

## 관계형
- hasMany
예를 들어, 한 유저가 게시글을 여러 개 게시할 수 있음. 하지만 한 게시글은 한 명의 작성자만 있을 수 있음.
```javascript
// model/user.js
... sequelize code
User.associate=(db)=>{
  db.User.hasMany(db.Post);
}
```
```jsx
// model/post.js
... sequelize code
Post.associate=(db)=>{
  db.Post.belongsTo(db.User); // 한 게시글의 작성자는 한 명의 유저이다.
}
```
`belongTo`를 통해 관계를 지정하면 `posts`테이블에 `UserId`라는 고유한 column이 생성된다.
