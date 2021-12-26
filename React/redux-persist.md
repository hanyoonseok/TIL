# Redux-persist
> redux 는 새로고침을 하게되면 저장되어있던 state들이 모두 날아간다는 특징이 있다. 이에 대한 방안으로 localstorage나 session storage에 리듀서 state를 저장하여 사용하는 redux-persist 가 있다.

### 배경
`Rubminds` 프로젝트 개발 중 마이페이지에서 찜목록과 프로젝트 현황 페이지로 이동하게 되어 있는데, 매 페이지 접속마다 api요청을 보내는 것이 비효율적이라 느껴지던 와중에 `redux-persist`라는 것을 통해서 상태를 저장할 수 있다는 것을 듣게 됨. 

### 설치
`npm i redux-persist`

### 적용
- rootReducer를 감싼 persistReducer를 선언
```jsx
//root reducer 선언부;
import {persistReducer} from 'redux-persist';
import storage from 'redux-persist/lib/storage'; // 세션에 저장할 때는 redux-persist/lib/storage/session을 임포트

const persistConfig = {
  key:'root',
  storage,
  //whitelist:['user'] 유저리듀서만 로컬스토리지에 저장
}
const rootReducer = ...;
const persistedReducer = persistReducer(persistConfig, rootReducer);
// for typescript 
// const persistedReducer = persistReducer<any, any>(persistConfig, rootReducer); 
export default persistedReducer;
```
- persistStore를 선언하고 어플리케이션의 `<App>`을 `PersistGate`로 감싸줌
```jsx
// store 선언부
import {persistStore} from 'redux-persist';
import {PersistGate} from 'redux-persist/integration/react';
import rootReducer, ... from './modules';

...
const store = createStore(rootReducer, ...);
const persistor = persistStore(store);

ReactDom.render(
  <Provider store={store}>
    <PersistGate persistor={persistor}>
      <App/>
    </PersistGate>
  </Provider>
)
```

### todo 작성 후 새로고침해도 상태가 유지되는 모습
![캡처](https://user-images.githubusercontent.com/28249948/147399498-ced90089-18ac-4bc7-8563-f0cd4a271997.PNG)
