### flex-shrink
- default: 1
- 0으로 줄 경우 flex box안에서 공간의 변동을 제한함.(할당된 사이즈를 유지함).

### flex-basis
- default: auto(컨텐츠의 크기)
- 아이템의 점유 크기를 설정
- 크기가 100px이 안되는 아이템에 `flex-basis:100px`을 주면 100px로 할당됨
```jsx
<div class="container"> 
  <div class="item">helloflex</div> 	
  <div class="item">abc</div>
  <div class="item">helloflex</div> 
</div>
```
