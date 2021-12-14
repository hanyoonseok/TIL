# Dataset
> 별 다른 조작없이 html 요소에 추가적인 정보를 저장할 수 있도록 해주는 추가적인 DOM 속성

### 문법
어떤 엘리먼트에나 `data-` 속성을 넣어서 사용.
```jsx
<button data-product-name="콜라">추가</button>
```

### 접근
- 자바스크립트에서 dataset에 접근할 때는 엘리먼트 객체를 가져오고 `.dataset`을 통해 접근하면 된다.
- 하이픈이 여러 개 존재할 경우 `camelCase`로 접근한다.
```jsx
const button = document.getElementById('product-price-button');
button.dataset.productName // 콜라
```

### 문제점
- 개발자 모드를 통해서도 저장된 dataset에 대한 열람이 가능하기 때문에 예민한 데이터는 저장하지 않는다
- 인터넷 익스플로러 11+ 이전 버전은 dataset을 지원하지 않는다
