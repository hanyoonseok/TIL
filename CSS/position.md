# position:static (default)
- 위치를 지정하지 않을 때 사용

# position:fixed
- 상단 바처럼 원래 위치와 상관없이 배치 가능. 
- 상위 요소의 영향을 받지 않기 때문에 화면이 바뀌더라도 고정된 위치를 설정 가능.
- 브라우저 화면의 상대위치를 기준으로 위치 결정.

# position:relative
- 위치를 계산할 때 static의 원래 위치부터 계산함. 
- relative로 배치하면 컴포넌트의 공간을 차지.
- 좌상단이 top:0, left:0

# position:absolute
- 상위 요소에 position:relative가 없을 경우, 최상단 root의 상대위치로 배치.
- 컴포넌트의 공간을 차지 하지 않음.(해당 위치에 다른 컴포넌트 있더라도 옆으로 밀리지 않고 덮어씌어짐)
- position:relative가 있을 경우, 해당 컴포넌트 기준으로 상대위치 결정.
