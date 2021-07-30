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
개발시에는 `"development"`의 값을 수정하여 테스트 한다. `dotenv`모듈을 설치하여 config.env파일로 환경변수를 관리하여 github에의 노출을 피하자  
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
