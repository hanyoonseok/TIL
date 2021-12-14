# MVC Pattern
> 디자인 패턴 중 하나  
> Model, View, Controller의 약자
- 하나의 프로젝트를 구성할 때 그 구성요소를 세 가지의 역할로 구분함.
- 사용자가 보는 페이지, 데이터 처리, 그리고 이 두 가지를 중간에서 제어하는 컨트롤하는 3가지 구성으로 각자 밭은 바에만 집중할 수 있게 함.
- `Model`과 `View`가 다른 컴포넌트들에 종속되지 않아 변경에 유리하다.

<img src="https://mblogthumb-phinf.pstatic.net/MjAxNzAzMjVfMjIg/MDAxNDkwNDM4ODMzNjI2.nzDNB5K0LuyP4joE2C4rIbL5Ue2F3at7wiI6ZpuTJN0g.WZ6V-WHZygLYW2WSdzcs7uAiAWgAJe3_H0XdkYKkutkg.PNG.jhc9639/1262.png?type=w800" width="100%"> 
사용자가 controller를 조작하면 controller는 model을 통해서 데이터를 가져오고 그 정보를 바탕으로 시각적인 표현을 담당하는 View를 제어해서 사용자에게 전달함.

<img src="https://mblogthumb-phinf.pstatic.net/MjAxNzAzMjVfMjUw/MDAxNDkwNDM4NzI4MTIy.4ZtITJJKJW_Nj1gKST0BhKMAzqmMaYIj9PobYJMFD4Ig.xTHT-0qyRKXsA4nZ2xKPNeCxeU2-tLIc-4oyrWq5WBgg.PNG.jhc9639/mvc_role_diagram.png?type=w800" width="100%">
모델은 컨트롤러에, 컨트롤러는 뷰에, 뷰는 다시 유저, 유저는 다시 컨트롤러를 향해서 감.

### M : Model
- 애플리케이션이 무엇을 할 것인지 정의 (쉽게 하나의 클래스라 생각하자)
- 처음에 정의하는 상수, 초기화 값, 변수 등의 가공(추가, 변경, 삭제)을 책임짐
- 자기 자신이 무엇을 수행하는지에만 집중

### V : View
- 처리한 데이터나 작업 결과를 사용자에게 화면으로 보여주는 역할(DOM 조작에만 집중)
- 자기 자신이 무엇을 수행하는지에만 집중
```jsx
//index.js
const view = new View();
const controller = new Controller(view);

//view가 controller에 종속되지 않도록 객체 생성 후 컨트롤러에 넣어주자
```

### C : Controller
- 모델이 데이터를 어떻게 처리할지 알려주는 역할
- 처리할 역할에 대한 모델을 호출하고, 그 결과를 view에 전달
- 페이지가 로드 되었을 때 뷰에 존재하는 엘리먼트들에 이벤트 리스너를 추가한다.
