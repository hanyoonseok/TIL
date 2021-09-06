# Redux
> 컴포넌트들의 상태 관련 로직을 다른 파일로 분리시켜 더욱 효율적인 관리.  
> 모든 글로벌 상태를 하나의 커다란 상태객체에 넣어 사용함으로써 글로벌 상태관리를 손쉽게 해줌.
- 프로젝트 규모가 클 때
- 비동기 작업을 자주 할 때
- 리덕스 사용이 편리할 때 사용
<img width="80%" src="https://image.slidesharecdn.com/006-170302100440/95/006-react-redux-framework-5-638.jpg?cb=1488450003" >
<img width="80%" src="https://image.slidesharecdn.com/006-170302100440/95/006-react-redux-framework-6-638.jpg?cb=1488450003" >  

#### 구조
- `flux`구조
<img width="80%" src="https://miro.medium.com/max/798/1*oRBseHE_yxtlbcRTrbkRnQ.png" >

### 왜? 사용해야 하는가
- 모든 페이지에서 공통으로 필요한 정보가 있음 (로그인 한 사용자 정보, 로그인 여부 등)
- 공통된 데이터들을 부모에서 자식으로 매번 내려주는 것이 반복되므로 중앙에서 컴포넌트로 보내주는 것이 편하다.
- 이 저장소 역할을 하는 것이 **redux**
- 비동기 요청이 많을 때, context api로 구현해도 결국은 redux와 형태가 비슷해지기 때문에 redux 사용하자.
- 에러가 났을 때 에러의 위치 추적이 쉽다.
- 앱의 규모가 커져서 중앙 저장소의 몸집이 커지더라도 리듀서를 쪼갬으로써 어느 정도 극복 가능하다.
- 다만 코드량이 많아진다는 단점이 있다.

### 적용
> `react-redux` 라이브러리 사용
```jsx
// src/index.js
import { createStore } from 'redux';
import { Provider } from 'react-redux';
import rootReducer from './modules';

const store = createStore(rootReducer); // 스토어생성

ReactDOM.render(
  <Provider store={store}> 
    <App />
  </Provider>,
  document.getElementById('root')
);
```
- `Provider`로 감싼 모든 컴포넌트에서 리덕스 스토어에 접근 가능

### 키워드
#### 액션(action)
> 상태에 어떠한 변화 필요하게 될 때, 액션이란 것을 발생시킴. 
> 하나의 객체로 표현됨
```jsx
const ChangeToggle = {
  type:"TOGGLE_VALUE",
  text:"hihi"
}
```
- 액션을 동적으로 만들어주는 방법 `action creator`
```jsx
const ChangeName = (data) =>{
  type:'CHANGE_NAME',
  data,
}
dispatch(ChangeName('yoonseok'));
```
- 액션 객체는 `type` 필드는 필수적으로 가지고 있어야하고, 그 외의 값들은 임의로 넣어줄 수 있음

#### 액션 생성함수
> 액션을 만드는 함수. 중앙저장소의 데이터를 변경하기 위해서는 꼭 액션을 거쳐야 함.
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
- 액션에 대한 상세정보라고 봐도 무방. ex)ADD_CNT라는 액션이 들어왔는데 얼만큼 추가할건지
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
```jsx
// src/index.js
import { createStore} from 'redux';
import { rootReducer } from './modules'; //modules디렉토리에 만들어둔 루트 리듀서
const store = createStore(rootReducer);
```

#### Dispatch
> 스토어 내장함수 중 하나. 
> **액션을 발생시키는 것이라고 보면 됨.**
- 파라미터로 액션 전달 `dispatch(action)`해주면 스토어는 리듀서 함수 실행시켜서 해당 액션 처리하는 로직 있으면 액션 참고하여 새로운 상태 생성.
- 액션을 `dispatch` 하는 순간 타입과 데이터가 `reducer`로 전달되고, 리듀서에 작성된 액션 처리대로 중앙저장소의 데이터 변경됨.
```jsx
import {useDispatch} from 'react-redux';
const dispatch = useDispatch();
dispatch(액션);
```

#### 구독(Subscribe)
> 스토어 내장함수 중 하나.
> 함수 형태의 값을 파라미터로 받아옴.
- 파라미터로 특정 함수 전달해주면, 액션이 dispatch 되었을 때 마다 전달해준 함수 호출.
- 보통 react-redux 라이브러리에서 제공하는 `connect` 또는 `useSelector` hook을 사용하여 리덕스 스토어 상태에 구독

#### useSelector
> 리액트와 리덕스를 연결해줌
```jsx
//reducers/index.js
const initialState = {
  user:{
    isLoggedIn:false,
    user:null,
    signUpData:{},
    ...
  },
  post:{
    mainPosts:[],
  }
}

//다른 어떤 파일
import {useSelector} from 'react-redux';
const isLoggedIn = useSelector((state)=>state.user.isLoggedIn);
```

### redux-thunk
> 리덕스에서 비동기 작업을 처리할 때 사용하는 미들웨어
> 액션객체가 아닌 함수를 디스패치 가능
- 미들웨어 사용 시 `dispatch`와 `getState` 파라미터로 받아야 함.

### 규칙
- 상태는 읽기전용이다.
> 기존의 상태를 건들이지 않고 불변성을 유지해주어야 함. 왜냐하면 내부적으로 데이터 변경을 감지하기 위해 shallow equality를 검사하기 때문. 겉핥기 식으로 비교를 하기 때문에 좋은 성능 유지 가능.
- 리듀서는 순수한 함수여야 함
> `new Date()`이나 랜덤 생성 등 순수하지 않은 작업은 리듀서 바깥에서 처리해야 함.  
> 이런 것 처리위해 **리덕스 미들웨어** 사용.

### next와 연동
> next에서 리덕스를 사용하는 법은 react에서와 다름
`npm install next-redux-wrapper`
- react에서와 달리 `app.js`에서 `Provider`로 감싸주지 않아도 된다.
