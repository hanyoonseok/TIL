# Sass (Syntactically Awesome Style Sheets)
> CSS pre-processor 로서, 복잡한 작업을 쉽게 할 수 있게 해주고, 코드의 재활용성을 높여줄 뿐만 아니라, 코드의 가독성을 높여주어 유지보수를 쉽게 해줌.

### 설치
`npm i sass`

### 확장자
`.scss` `.sass`

### 예시
- 변수 선언 및 새로운 함수 사용
```jsx
// button.js
<button className="Button">sass button</button>

// style.scss
$blue:#228be6 //변수 선언
.Button{
  ...
  background:$blue; //변수사용
  &:hover{
    background:lighten($blue, 10%); //마우스 올렸을 때 배경색을 10% 더 밝게
  }
  &:active{
    background:darken($blue, 10%); //클릭했을 때 배경색을 10% 더 어둡게
  }
}
```
- className에 CSS 클래스 이름 동적 할당  
`npm install classnames`
```jsx
// button.js
<button className={classNames('Button', size)}>sass button</button>
//classNames 문법
classNames('foo', 'bar'); // => 'foo bar'
classNames('foo', { bar: true }); // => 'foo bar'
classNames({ 'foo-bar': true }); // => 'foo-bar'
classNames({ 'foo-bar': false }); // => ''
classNames({ foo: true }, { bar: true }); // => 'foo bar'
classNames({ foo: true, bar: true }); // => 'foo bar'
classNames(['foo', 'bar']); // => 'foo bar'

// style.scss
.Button{
  &.large { //Button 클래스, large 클래스 모두 적용시
    height: 3rem;
    padding-left: 1rem;
    padding-right: 1rem;
    font-size: 1.25rem;
  }

  &.medium {
    height: 2.25rem;
    padding-left: 1rem;
    padding-right: 1rem;
    font-size: 1rem;
  }

  &.small {
    height: 1.75rem;
    font-size: 0.875rem;
    padding-left: 1rem;
    padding-right: 1rem;
  }
  
  & + &{ //.Button + .Button 일 때
    margin-left:1rem; //우측에 있는 버튼에 여백 설정
  }
}
```
- @mixin 을 사용하여 기능 재사용
```jsx
$blue: #228be6;
$gray: #495057;
$pink: #f06595;

@mixin button-color($color) {
  background: $color;
  &:hover {
    background: lighten($color, 10%);
  }
  &:active {
    background: darken($color, 10%);
  }
}
.Button{
  ...
  &.blue{
    @include button-color($blue);
  }
  &.red{
    @include button-color($red);
  }
  &.green{
    @include button-color($green);
  }
}
```
- props 값이 true일 때만 옵션 포함
```jsx
// button.js
<button className={classNames('Button', size, color, { outline })}>

// style.scss
@mixin button-color($color) {
  ...
  &.outline {
    color: $color;
    background: none;
    border: 1px solid $color;
    &:hover {
      background: $color;
      color: white;
    }
  }
}
```

[참고](https://react.vlpt.us/styling/01-sass.html)
