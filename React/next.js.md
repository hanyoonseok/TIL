# next.js
- 고객 인터랙션의 속도가 중요할 때사용(B to C 서비스)
- 검색엔진 노출에 도움을 준다.
- SSR(Server Side Rendering)을 도와주는 react 프레임워크
- 페이지 첫 방문시에만 `브라우저`->`프론트서버`->`백엔드서버`->`DB`를 거치는 전통 방법으로 렌더링하고, 그 이후의 링킹은 리액트 방식으로 진행.
- 어드민 페이지처럼 검색엔진에 노출될 필요도 없고, 고객 인터랙션 속도도 상대적으로 덜 중요할 땐 사용하지 않는 것이 낫다.

### SSR(서버사이드 렌더링)
> 클라이언트사이드 렌더링 시의 플로우
![제목 없음](https://user-images.githubusercontent.com/28249948/133707388-0ad43438-de9a-4b8f-bf06-358df345bb2c.png)
- 브라우저와 클라이언트끼리 먼저 주고받고, 그 이후 백엔드에서 데이터를 받아오는 형식이기 때문에, 페이지가 렌더링 된 이후에 데이터가 뒤늦게 들어가서 사용자 입장에서는 붕 뜬 느낌을 받을 수 있음.
> 서버사이드 렌더링 시의 플로우
![제목 없음](https://user-images.githubusercontent.com/28249948/133707546-b9434900-8129-4af9-9788-1d448da9dcf5.png)
- 요청을 한 번만 보내도 되기 때문에 초기 로딩속도(컨텐츠 보이는 속도)가 빨라지는 느낌. 

- 쿠키를 브라우저가 아닌 **프론트 서버**에서 백엔드 서버로 보내야 하기 때문에 `credential` 문제가 발생함.
- `getStaticProps` 동적인 데이터를 다룰 수 없기 때문에 언제 접속해도 데이터가 바뀔 일이 없을 때.
- `getServerSideProps` 접속할 때마다 접속한 상황에 따라서 화면이 바뀌어야 할 때

### page split
```jsx
// pages/index.js
const Home = () =>{
    return(
        <div>hello</div>
    )
}
export default Home;
```
- `localhost:3000`의 주소에 hello가 출력된다.
```jsx
// pages/profile.js
const Profile = () =>{
    return <div>내 프로필</div>
}
export default Profile
```
- `localhost:3000/profile`에 내 프로필이 출력
- 이를 통해 pages폴더 내에 파일 명으로 페이지를 구분하여 자동으로 라우팅까지 해주는 것을 알 수 있음.
- `pages` 안에서 폴더를 만들고 .js파일을 생성하면 `localhost:3000/폴더명/파일명` 의 형태로 라우팅이 됨.

### link
- `next`에서는 `react-router`사용 안하고 자체적으로 가지고있는 링크가 있음
- `import Link from 'next/link`
```jsx
<Link href="/"><a>home</a></Link>
```

