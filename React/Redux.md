# Redux

### 키워드
#### 액션(action)
> 상태에 어떠한 변화 필요하게 될 때, 액션이란 것을 발생시킴. 
> 하나의 객체로 표현됨
```jsx
{
  type:"TOGGLE_VALUE",
  text:"hihi"
}
```
액션 객체는 `type` 필드는 필수적으로 가지고 있어야하고, 그 외의 값들은 임의로 넣어줄 수 있음

#### 액션 생성함수
> 액션을 만드는 함수
> 컴포넌트에서 더욱 쉽게 액션 발생시키기 위함.
```jsx
export const changeInput = text => ({ 
  type: "CHANGE_INPUT",
  text
});
```

#### 리듀서(Reducer)
> 변화를 일으키는 함수
> `state`와 `action` 두 가지 파라미터를 받아옴
```jsx
// ex) 카운터를 위한 리듀서
function counter(state, action) {
  switch (action.type) {
    case 'INCREASE':
      return state + 1;
    case 'DECREASE':
      return state - 1;
    default: //리듀서에서는 기존 state를 그대로 반환해야함
      return state;
  }
}
```

#### 스토어(Store)
> 리덕스에서는 **한 애플리케이션당 하나의 스토어** 만듬. 스토어 안에는 현재의 앱 상태, 리듀서가 들어가있고, 몇 가지 내장함수들 있음.

#### Dispatch
> 스토어 내장함수 중 하나. 
> **액션을 발생시키는 것이라고 보면 됨.**
- 파라미터로 액션 전달 `dispatch(action)`해주면 스토어는 리듀서 함수 실행시켜서 해당 액션 처리하는 로직 있으면 액션 참고하여 새로운 상태 생성.

#### 구독(Subscribe)
> 스토어 내장함수 중 하나.
> 함수 형태의 값을 파라미터로 받아옴.
- 파라미터로 특정 함수 전달해주면, 액션이 dispatch 되었을 때 마다 전달해준 함수 호출.
- 보통 react-redux 라이브러리에서 제공하는 `connect` 또는 `useSelector` hook을 사용하여 리덕스 스토어 상태에 구독
