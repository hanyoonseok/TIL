# react-router-dom

**리액트의 라우팅 방법에는 크게 3가지가 있다.**

**하나는 `Redirect`, 하나는 `history.push`, 마지막으로 `Link`이다.**

**이 세 가지의 차이가 무엇인지, 언제 사용해야 하는 것인지 구분해보자**

## history
- history 스택을 사용.
- **jsx에서 사용 불가**
    - 사용시 함수 안에서 호출하여 활용
- 하위 컴포넌트에서 history 객체 사용시, props를 통해 부모 컴포넌트로부터 전달 받아야 함.
- `history.push`
    - 이동 전 경로를 기억함.
- `history.replace`
    - 이동 전 경로가 남지 않음.
```jsx
import {useHistory} from 'react-router-dom'
const Test = () =>{
  const history = useHistory();
  const goHome = () =>{
    history.push("/home");
    //history.replace("/home");
  }
  return(<button onClick={goHome}>GO</button>)
}
```

## Redirect
- `history.replace`처럼 이동 전 경로가 남지 않도록 할 때 사용
- **jsx에서 사용 가능**
- 상위 컴포넌트로부터 props를 전달받지 않아도 됨.
```jsx
//로그인 정보가 있을 경우 컴포넌트로 이동할 수 있지만
//로그인 정보가 없다면 로그인 페이지로 redirect되도록 하는 코드
import React from 'react';
import { Redirect, Route } from 'react-router-dom';

function PrivateRoute ({ component: Component, ...rest }) {
  return(
    <Route {...rest}
      render = {props => localStorage.getItem('users')?
      (<Component {...props}/>)
      :
      (<Redirect to={{
        pathname:'/users/sign_in',
        state:{from:props.location}
        }}
       />
      )
     }
    /> //Route
  )
}
export default PrivateRoute;
```

## Link
- 내부적으로 `<a>`태그를 통해 작동됨.
- 페이지 전체가 새로고침되는 방식이 아닌, 필요한 부분만 리로드됨.
- **jsx안에서 사용 가능**
- 이동 전 경로가 `history`객체에 남음
    - 이동 전 경로 남기지 않으려면 `replace={true}`옵션 추가
```jsx
import {Link} from 'react-router-dom'
const Test = () =>{
  return(
    <Link to="/home">GO</Link>
    <Link to="/home" replace={true}>GO</Link>
  )
}
```
