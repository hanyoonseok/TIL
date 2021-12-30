# e.preventDefault vs e.stopPropagation

### preventDefault
```jsx
<a href="/">
  <div onClick={()=>alert('click')}>click</div>
</a>
```
위 처럼 설계되어 있다고 가정할 때, `click`을 누르면 a태그에 의해 href 속성의 주소로 이동하게 된다. 이때 a태그에 등록된 주소로 이동하지 않게 하려면 `preventDefault()`를 사용하여 방지할 수 있다. 이 처럼 `preventDefault()`는 브라우저 고유의 동작을 중단시켜주는 역할을 함. 이 외에도 `onSubmit` 이벤트의 페이지 리프레쉬 등의 현상을 방지할 수 있음. 적용한 코드는 아래와 같음.
```jsx
const onclickClick = useCallback((e)=>{
  e.preventDefault();
  alert('click');
},[])
<a href="/">
  <div onClick={onclickClick}>click</div>
</a>
```

### stopPropagation
```jsx
<div onClick={()=>alert('부모')}>
  <div onClick={()=>alert('자식')}>
    클릭
  </div>
</div>
```
위 처럼 설계되어 있다고 가정할 때, `클릭`을 누르면 `자식`->`부모` 순으로 메시지가 발생한다. 이때 `부모`를 띄우지 않고 `자식`만 띄우고 싶을 때는 부모 엘리먼트의 이벤트 전달을 중단해야 한다. 이때 `stopPropagation`을 사용한다. 적용한 코드는 아래와 같다.
```jsx
const onclickClick = useCallback((e)=>{
  e.stopPropagation();
  alert('자식');
},[])

<div onClick={()=>alert('부모')}>
  <div onClick={onclickClick}>
    클릭
  </div>
</div>
// '자식'만 출력
```

### 결론
`preventDefault`는 브라우저 고유의 행동(페이지 이동, 리프레쉬)를 막아주는 함수라고 생각하면 되고, `stopPropagation`은 부모 엘리먼트로의 이벤트 전달을 막아주는 함수라고 생각하자!
