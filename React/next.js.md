# next.js
- 고객 인터랙션의 속도가 중요할 때사용(B to C 서비스)
- 검색엔진 노출에 도움을 준다.
- SSR(Server Side Rendering)을 도와주는 react 프레임워크
- 페이지 첫 방문시에만 `브라우저`->`프론트서버`->`백엔드서버`->`DB`를 거치는 전통 방법으로 렌더링하고, 그 이후의 링킹은 리액트 방식으로 진행.
- 어드민 페이지처럼 검색엔진에 노출될 필요도 없고, 고객 인터랙션 속도도 상대적으로 덜 중요할 땐 사용하지 않는 것이 낫다.

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

