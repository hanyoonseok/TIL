# 리액트로 full page 만들기

### DOM
![image](https://user-images.githubusercontent.com/28249948/171206986-06802230-5d20-4ddf-845b-d6669edde3a3.png)

### Script
```jsx
  const mainWrapperRef = useRef(); //화면의 wrapper에 마우스 휠 이벤트를 바인딩하기 위해 useRef 사용

  useEffect(() => {
    const wheelHandler = (e) => {
      e.preventDefault();
      const { deltaY } = e;
      const { scrollTop } = mainWrapperRef.current; // 스크롤 위쪽 끝부분 위치
      const pageHeight = window.innerHeight; // 화면 세로길이, 100vh와 같습니다.

      if (deltaY > 0) {
        // 스크롤 내릴 때
        if (scrollTop >= 0 && scrollTop < pageHeight) {
          //현재 1페이지
          mainWrapperRef.current.scrollTo({
            top: pageHeight,
            left: 0,
            behavior: "smooth",
          });
        } else if (scrollTop >= pageHeight && scrollTop < pageHeight * 2) {
          //현재 2페이지
          mainWrapperRef.current.scrollTo({
            top: pageHeight * 2,
            left: 0,
            behavior: "smooth",
          });
        } else {
          // 현재 3페이지
          mainWrapperRef.current.scrollTo({
            top: pageHeight * 2,
            left: 0,
            behavior: "smooth",
          });
        }
      } else {
        // 스크롤 올릴 때
        if (scrollTop >= 0 && scrollTop < pageHeight) {
          //현재 1페이지
          mainWrapperRef.current.scrollTo({
            top: 0,
            left: 0,
            behavior: "smooth",
          });
        } else if (scrollTop >= pageHeight && scrollTop < pageHeight * 2) {
          //현재 2페이지
          mainWrapperRef.current.scrollTo({
            top: 0,
            left: 0,
            behavior: "smooth",
          });
        } else {
          // 현재 3페이지
          mainWrapperRef.current.scrollTo({
            top: pageHeight,
            left: 0,
            behavior: "smooth",
          });
        }
      }
    };
    const wrapperRefCurrent = mainWrapperRef.current;
    wrapperRefCurrent.addEventListener("wheel", wheelHandler);

    return () => {
      //wrapperRefCurrent.removeEventHandler("wheel", wheelHandler);
    };
  }, []);
```

### CSS
```css
.main-wrapper {
  overflow-y: hidden;
  height: 100vh;
}

.main-item {
  height: 100vh;
}
```

[참고](https://codingbroker.tistory.com/128)
