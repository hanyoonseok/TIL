# redux-thunk
> `thunk`란 `지연(遲延)`의 의미를 가짐.  
> redux의 미들웨어로서 리덕스 기능을 향상시켜줌.  
> redux가 비동기 액션을 dispatch 할 수 있도록 도와줌.  
> 액션객체가 아닌 함수를 디스패치 가능.  
- 하나의 비동기 액션 안에 여러 개의 동기 액션을 넣을 수 있음. 예를 들어 axios를 보낼 때 request 액션을 dispatch하고 성공하면 다른 액션 dispatch가 가능해짐.
```jsx
const loginAction=(data)=>{
  return (dispatch, getState)=>{
  const state = getState(); //getstate가 initialstate가 됨.
    dispatch(loginRequestAction());
    axios.post('/api/login')
    .then(()=>{
      dispatch(loginSuccessAction(res.data));
    })
    .catch(()=>{
      dispatch(loginFailureAction(err));
    })
  }
}
```
