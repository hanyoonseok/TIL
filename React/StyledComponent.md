# StyledComponent

### 설치
`npm install styled-components`
***
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
***
### ThemeProvider
> `ThemeProvider`로 감싸진 자식 Component들은 ThemeProvider로 전달받은 theme를 props로 전달받아서 사용이 가능.
```jsx
//App.js
import React from "react";
import { ThemeProvider } from "styled-components";

const App = () => {
  return (
    <div>
      <ThemeProvider theme={theme}>
        <Navbar />
        <Search />
        <IntroBooks />
      </ThemeProvider>
    </div>
  );
};
```
```jsx
//theme.js
const calcRem = (size) => `${size / 16}rem`;

const fontSizes = {
  small: calcRem(14),
  base: calcRem(16),
  lg: calcRem(18),
  titleSize: calcRem(50),
};

const colors = {
  black: "#000000",
  white: "#FFFFFF",
  gray_1: "#222222",
};

const theme = {
  fontSizes,
  colors,
};

export default theme;
```
```jsx
const NavbarWrapper = styled.div`
  // ${}를 사용해서 인자로 theme의 값을 받을 수 있고 원하는 theme의 요소를 사용할 수 있음.
  
  font-size: ${({ theme }) => theme.fontSizes.base};
  color: ${({ theme }) => theme.colors.gray_1};
`;
```
[기타 사용법 참고](https://velog.io/@hoi/Styled-components-ThemeProvider%EB%A5%BC-%ED%99%9C%EC%9A%A9%ED%95%9C-%EC%8A%A4%ED%83%80%EC%9D%BC-%ED%99%98%EA%B2%BD-%EA%B5%AC%EC%B6%95)
***

### createGlobalStyle
> `styled-components`는 `slick-slide`처럼 이미 className이 정해진 컴포넌트의 스타일을 바꿀 수 있음(덮어쓰기)
```jsx
import {createGlobalStyle} from 'styled-components'
const Global = createGlobalStyle`
    .slick-slide{
        display:inline-block;
    }
`
```

### SSR
> `styled-components`는 서버사이드렌더링 시에 따로 설정해주어야 적용이 된다.
