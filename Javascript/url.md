# 자바스크립트 URL

### 현재 내 URL 가져오기
`window.location.href`

### 현재 내 URL 에서 쿼리스트링 부분만 가져오기
`window.location.search`

### URL 상에 쿼리문 value 가져오기
```jsx
const url = new URL(window.location.href); //url 객체 생성
const urlParams = url.searchParams; // 탐색을 위한 속성
const resultParams = urlParams.get('search'); //search라는 쿼리의 value 값을 가져오고싶다
```

### 특정 파라미터가 있는지 체크
```jsx
const urlParams = new URLSearchParams(window.location.href); // naver.com?hi=1235
console.log(urlParams.has('hi')); //true
console.log(urlParams.has('bye')); //false
```
