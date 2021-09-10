# redux-saga
### 설치
`npm install redux-saga`

### generator
> `yield`라는 중단점이 있는 함수라고 생각하면 편함.
```jsx
const gen = function* (){
  console.log(1);
  yield;
  console.log(2);
  yield;
  console.log(3);
  yield 4;
}

const generator = gen();
generator.next(); // 1출력
generator.next(); // 2출력
generator.next(); // 3출력
```
- saga에서 `while(true)`의 개념은 일반적으로 알고있는 무한루프와는 다르다. 이러한 성질로 이벤트 리스너 역할을 할 수 있다.
```jsx
let i=0;
const gen = function* (){
  while(true){
    yield i++;
  }
}

const g = gen();
g.next(); //0
g.next(); //1
g.next(); //2
```

### 사용법
- rootsaga를 만들고 그 안에 내가 만들고싶은 비동기 액션들을 넣어줌.
```jsx
import {all, fork, take, call} from 'redux-saga/effects'
function logInAPI(){
    return axios.post('/api/login')
}

function* logIn(){
    try{
        const result = yield call(logInAPI);
        yield put({ //put은 dispatch라고 생각하면 편함.
            type:'LOG_IN_SUCCESS',
            data:result.data
        })
    }
    catch(err){
        yield put({
            type:'LOG_IN_FAILURE',
            data:err.response.data,
        })
    }
}
function* watchLogin(){
    //로그인이란 액션이 실행될 때 까지 기다리겠다.
    //LOG_IN_REQUEST액션 끝나면 logIn이란 함수 실행
    yield take('LOG_IN_REQUEST', logIn);
}
function* watchLogout(){
    yield take('LOG_OUT');
}
function* watchAddPost(){
    yield take('ADD_POST');
}

export default function* rootSaga(){
    yield all([ //이 모든 액션을 동시에 실행해준다.
        fork(watchLogin), //fork는 이 함수를 실행한다는 것.
        fork(watchLogout),
        fork(watchAddPost),
    ])
}
```
- `fork`는 비동기 함수 호출
- `call`은 동기 함수 호출

### take
 - `take`는 한 번만 실행해주고 사라짐. 이를 보완하려면 `while(true)`로 감싸주어야함. `while take`는 동기적으로 동작함.
### takeEvery
 - `takeEvery`는 비동기로 동작.
### takeLatest
> 실수로 마우스 2번 클릭하던지 할 때, 앞선 클릭은 무시하고 마지막 클릭만 수용.
