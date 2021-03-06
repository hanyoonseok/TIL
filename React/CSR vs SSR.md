# CSR(Client Side Rendering)

### 동작 과정
<img src="https://media.vlpt.us/images/vagabondms/post/0289f96e-c34d-48a9-b942-eb9376ab43af/image.png" width="100%"/>

##### 1. CDN이 html과 js로 접근 가능한 링크를 클라이언트로 전송
> **CDN** : aws의 cloudflare를 생각하면 됨. 엔드 유저의 요청에 '물리적'으로 가까운 서버에서 요청에 응답하는 방식
##### 2. 클라이언트에서 html과 css, js를 다운받음
##### 3. js 실행되고 데이터를 위한 api가 호출됨
> 이 때부터 placeholder 보임
##### 4. api로부터 받아온 데이터들이 화면에 배치되고, 이 때부터 인터랙션 가능

### 특징
- 검색엔진에 불리. 구글은 크롤러안에 자바스크립트 엔진이 있어 괜찮지만, 네이버나 다음은 그렇지 않기 때문에 빈 페이지로 인식함
- 최초 로딩시간이 김
- 다른 페이지로의 이동 시간은 빠름(이미 처음에 다 받아왔기 때문에)
- 사용자에게 보여줘야 하는 데이터의 양이 많을 때 좋음(로딩창 띄우면 되서)

# SSR(Server Side Rendering)

### 동작 과정
<img src="https://media.vlpt.us/images/vagabondms/post/8c4c7988-c35d-4722-8e78-4c4f4bbb54a5/image.png" width="100%"/>

##### 1. 서버가 즉시 렌더링 가능한 html을 만들고 클라이언트에 전달
> 이 때부터 유저는 화면 볼 수 있음(인터랙션은 x)
##### 2. 클라이언트가 자바스크립트 다운받음
> 이 때부터 유저는 컨텐츠들을 볼 수 있지만 사용자 조작은x. 대신 기억해둠
##### 3. 프레임워크(리액트) 실행시킴
> 기억해뒀던 사용자 조작 실행. 이 때부터 인터랙션 가능

### 특징
- 검색엔진에 유리. 애초에 서버 사이드에서 컴파일되어 클라이트로 넘어오기 때문.
- 최초 로딩시간이 짧음(html만 먼저 그려주기 때문)
- 다른 페이지로의 이동 시간은 불리(위의 동작을 그대로 한 번 더 하기 때문)
