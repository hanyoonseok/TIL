### useCallback
> 함수를 캐싱해주는 콜백
- 컴포넌트에 `props`로 넘겨주는 함수는 꼭 `useCallback`을 써야함
- 캐싱을 통해 성능 최적화
```jsx
const testFunction = useCallback(()=>{
  // 함수 내용
},[])
```

### useMemo
> 값을 캐싱해주는 콜백
```jsx
const style = useMemo(()=>{
  {marginTop:10}
},[])
```
