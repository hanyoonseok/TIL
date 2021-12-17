# `for ... in` vs `for ... of `

### for ... in
> 객체 순환  
> 객체의 모든 열거 가능한 속성에 대해 반복
```jsx
const obj = {
  one:1,
  two:2,
  thr:3,
}
for (let property in obj) {
  console.log(property); // one, two, thr
}
for (let property of obj) {
  console.log(property); // Uncaught TypeError: obj is not iterable
}
```

### for ... of
> 배열 값 순환
```jsx
let arr = [1, 2, 3];
for(let item of arr) {
  console.log(item); // 1, 2, 3
}
for(let item in arr) {
  console.log(item); // 0, 1, 2
}
```
자바스크립트에서는 배열도 객체이기 때문에 에러는 발생하지 않음. 배열의 경우엔 index가 출력됨.

**`string`에 대해서도 반복 가능하다**
```jsx
const str = "string";
for(let value of str) {
  console.log(value) // "s", "t", "r", "i", "n", "g"
}
```

**for...of**는 `string`외에도 `set`, `map`, `TypedArray`, `DOM 컬렉션` 등에도 적용 가능하다
