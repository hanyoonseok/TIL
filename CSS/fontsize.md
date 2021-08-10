# CSS font size
### rem(root em)
> px 값으로 폰트 사이즈 지정시, 미디어 쿼리를 작성할 때 일일히 찾아서 바꿔줘야 한다는 단점이 있다. body태그에 fontsize를 지정해주고 하위 컴포넌트들에 fontsize로 rem을 주면 나중에 미디어 쿼리를 작성할 때 body의 폰트 사이즈만 변경해주면 된다.  
```css
body{
  font-size:16px;
}
a{
  font-size:1.5rem; //24px
}
```
