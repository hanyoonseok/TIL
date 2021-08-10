# React.memo()
> 컴포넌트의 props가 바뀌지 않았다면, 리렌더링을 방지하여 컴포넌트의 리렌더링 성능을 최적화 해주는 함수

#### 사용법
- 마지막에 export 할 때 memo로 감싸주기만 하면 된다.
```javascript
import React, {memo} from 'React';

const User = ({name, email, age}) => {
  return (
    <div>
      ...
    </div>
  )
}

export default memo(User);
```
