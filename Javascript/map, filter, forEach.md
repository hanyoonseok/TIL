### map
- 배열 내의 모든 요소 각각에 대하여 주어진 함수를 호출한 결과를 가진 **새로운 배열**을 만듬.
- 원래의 배열은 바뀌지 않음
```jsx
let numbers=[1, 4, 9];
let newArr = numbers.map(x =>{
  return Math.sqrt(x);
})
```

### forEach
- 주어진 함수를 배열 내의 요소들에게 실행한다 (for loop와 비슷)
- 원래 배열은 바뀌지 않음
```jsx
let arr=[1, 2, 3];
arr.forEach(x => console.log(x));
```

### filter
- 주어진 함수에 속한 조건을 통과한 요소들을 **새로운 배열**로 반환
- 원래 배열은 바뀌지 않음
```jsx
const isEven = (val) => {
  return val % 2 === 0;
}
let numbers = [1, 2, 3, 4];
let filtered = numbers.filter(isEven);  //[2, 4]
```
