### Custom hook
- form data를 다루거나 할 때 onChange 등이 중복되거나 하면 직접 훅을 작성하여 할당하면 중복을 줄일 수 있음.
```jsx
const [id, setId] = useState('');
const [pw, setPw] = useState('');
const onChangeId = useCallback((e)=>{
  setId(e.target.value);
},[]);
const onChangePw = useCallback((e)=>{
  setPw(e.target.value);
},[]);
```
폼 데이터를 다룰 때 위와같은 상황이 자주 발생하는데 이를 아래와 같이 바꾸면
```jsx
// hooks/useInput.js
import {useState, useCallback} from 'react';

export default (initialValue=null) =>{
    const [value, setValue] = useState(initialValue);
    const handler = useCallback((e)=>{
        setValue(e.target.value);
    },[]);
    return [value, handler];
}
```
아래와 같이 코드 양을 줄일 수 있다.
```jsx
import useInput from '../hooks/useInput';
const [id, onChangeId]=useInput('');
...
<input type="text" onChange={onChangeId}/>
```
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
