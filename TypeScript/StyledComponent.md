# Styled-component with TS

### props 
> 타입스크립트에서는 컴포넌트에 타입을 지정해줘야 하기 때문에 `style.ts`에서 따로 props에 대한 interface를 작성해야한다.  
> `styled.div<인터페이스명>` 
```jsx
//style.js
interface Props{
    bgColor?:string,
    color?:string,
}

export const StyledBackground = styled.div<Props>`
    background-color:${props=>props.bgColor};
```
