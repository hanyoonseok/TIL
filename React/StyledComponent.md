# StyledComponent

### 설치
`npm install styled-components`

### 적용
```jsx
import React from 'react';
import styled from 'styled-components';

const Circle = styled.div` //div태그를 스타일링
  width: 5rem;
  height: 5rem;
  background: ${props => props.color || 'black'}; // color props값을 설정해주었으면 그 색으로, 아니면 검은색으로
  border-radius: 50%;
  ${props => 
  props.huge && css` //props.huge가 존재하는 경우에만 width:10rem
    width: 10rem,
  `};
`;

function App() {
  return <Circle color="blue" huge/>;
}
export default App;
```
