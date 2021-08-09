# var 
```javascript
var name = 'test'
console.log(name) // test

var name = 'ttesstt'
console.log(name) // ttesstt
```
`var`는 변수를 한 번 더 선언했는데도 에러메시지 발생하지 않고, 새로 선언된 변수 값이 할당된다. 코드량 많아졌을 때, 중복 선언하여도 에러 메시지를 발생하지 않기 때문에 매우 안좋고 어디서 어떻게 사용 될지 파악하기도 힘들다.
    
# let & const
```javascript
let name = 'test'
console.log(name) // test

let name = 'ttesstt'
console.log(name) // error 메시지 출력

const nameconst = 'test'
console.log(name) // test

const nameconst = 'ttesstt'
console.log(name) // error 메시지 출력
```
`let`은 중복 선언시 에러메시지를 발생시킨다. `const`도 마찬가지로 에러메시지를 발생시키는데, 이 둘의 차이는 `let`은 재선언, 재할당이 가능하지만, const는 모두 불가능하다.
