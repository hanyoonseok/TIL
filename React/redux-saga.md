# redux-saga
### 설치
`npm install redux-saga`

### generator
> `yield`라는 중단점이 있는 함수라고 생각하면 편함.
```jsx
const gen = function* (){
  console.log(1);
  yield;
  console.log(2);
  yield;
  console.log(3);
  yield 4;
}

const generator = gen();
generator.next(); // 1출력
generator.next(); // 2출력
generator.next(); // 3출력
```
- saga에서 `while(true)`의 개념은 일반적으로 알고있는 무한루프와는 다르다. 이러한 성질로 이벤트 리스너 역할을 할 수 있다.
```jsx
let i=0;
const gen = function* (){
  while(true){
    yield i++;
  }
}

const g = gen();
g.next(); //0
g.next(); //1
g.next(); //2
```
