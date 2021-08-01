# Sequelize문법      
## 데이터조회  
```javascript
const users = User.findAll({
  where:{id:99} //User테이블에서 ID가 99인 모든 행들을 배열의 형태로 users에 담겠다
})

const user = User.findOne({
  where:{id:99} //User테이블에서 ID가 99인 첫 번째 행을 user에 담겠다
})

User.findById(99).then((result)=>{
  //User테이블에서 ID가 99인 행을 찾겠다.
  //존재하지 않으면 null 반환
})
```    
## Sequelize 옵션들
```javascript
const items = await Item.findAll({
        include:[{model:Proposal,attributes:['date_end']}], 
        attributes:['uuid','item_title','categoryName'],
        where:{status:1},
        raw:false, 
        nest:true, 
        order:[[standard,dir]] //standard를 기준으로 dir하게 정렬
})
```  
`include`옵션은 Item테이블을 기준으로 Proposal테이블을 left join 하는 옵션이다. include 안에서 별도의 attributes 옵션을 주지 않으면, 결과를 받아올 때 각각의 item 요소에 Proposal 테이블의 모든 열들이 함께 join된다.  
`attributes`옵션은 테이블에서 넣어준 '열 이름'만 추출한다. 위의 예시에서는 Item 테이블을 가져오는데 'uuid','item_title','categoryName'열만 가져오겠다는 뜻이다.  
`where`옵션은 sql query에서의 where와 동일하다. 위의 예시에서는 status가 1인 정보만 가져오겠다는 뜻이다.  
`raw`옵션은 true옵션을 줄 경우 left join하는 테이블과 1:N 관계일 때 각각을 단일개체로 생성하여 중복 출력된다. false 옵션을 줄 경우  
```javascript
{
 "items":{
    //items테이블의 row
    "proposal":[
      {
        //proposal테이블의 row
      },
      {
        //proposal테이블의 row
      },
      
    ]
 }
}
```형태로 출력된다.  
`order`옵션은 [[standard, dir]]형태로 standard 열을 기준으로 dir방향으로 정렬한다는 뜻이다. `ex) order:[['id','DESC']]` id를 기준으로 내림차순  
`limit`옵션은 value값 만큼만 출력한다. `ex) limit:10` 10개까지만 출력.    

## Sequelize 연산자
