# React hooks를 이용한 Carousel 제작

**1. 컴포넌트 제작**
```jsx
//...js
return (
    <S.CarouselContainer size={size}> //props로 받은 사이즈로 width,height 결정
      <S.CarouselPrev onClick={prevClick} /> //이전 버튼
      <S.CarouselNext onClick={nextClick} /> //다음 버튼
      <S.CarouselWrapper ref={CarouselWrapper}>
        {
          imgs.map((v,i) => {
          <S.CarouselImg src={v} key={i} size={size}/>//props로 받은 사이즈로 width,height 결정
          })
        }
      </S.CarouselWrapper>
    </S.CarouselContainer>
  );
  
// style.js
export const CarouselContainer = styled.div`
  width: ${(props) => props.size};
  height: ${(props) => props.size};
  overflow: hidden;
  position: relative;
`;

export const CarouselWrapper = styled.div`
  display: flex;
`;

export const CarouselImg = styled.img`
  width: ${(props) => props.size};
  height: ${(props) => props.size};
`;

export const CarouselPrev = styled(GrFormPrevious)`
  border: none;
  position: absolute;
  top: 50%;
  left: 1%;
  font-size: 3rem;
  background-color: #fff;
  z-index: 10;
  cursor: pointer;
  border-radius: 50%;
`;
export const CarouselNext = styled(GrFormNext)`
  border: none;
  position: absolute;
  top: 50%;
  right: 1%;
  font-size: 3rem;
  background-color: #fff;
  z-index: 10;
  cursor: pointer;
  border-radius: 50%;
`;
```
**2. 상태관리**
```jsx
const CarouselWrapper = useRef(null);
const [currentImg, setCurrentImg] = useState(0); //현재 보여지는 이미지 인덱스
const totalImgs = 5; //총 이미지 개수-1
useEffect(() => { //슬라이드로 이동하는 애니메이션을 만듬
    CarouselWrapper.current.style.transition = 'all 0.4s ease-in-out';
    CarouselWrapper.current.style.transform = `translateX(-${currentImg}00%)`; 
  }, [currentImg]);
```
**3. 클릭이벤트 추가**
```jsx
//next버튼 클릭시
const nextClick = useCallback(() => {
    if (currentImg >= totalImgs) {
      // 더 이상 넘어갈 슬라이드가 없으면
      setCurrentImg(0); // 1번째 사진으로
    } else {
      setCurrentImg(currentImg + 1);
    }
  }, [currentImg]);
// Prev 버튼 클릭 시
const prevClick = useCallback(() => {
    if (currentImg === 0) {
      setCurrentImg(totalImgs); // 마지막 사진으로
    } else {
      setCurrentImg(currentImg - 1);
    }
  }, [currentImg]);
```

**전체코드**
```jsx
import React, { useState, useCallback, useRef, useEffect } from 'react';
import * as S from './style';

const Carousel = ({size}) => {
  //추후 props로 이미지 url 담긴 배열 받아서 처리
  const CarouselWrapper = useRef(null);
  const [currentImg, setCurrentImg] = useState(0);
  const totalImgs = 5; //이미지 개수-1
  useEffect(() => {
    CarouselWrapper.current.style.transition = 'all 0.4s ease-in-out';
    CarouselWrapper.current.style.transform = `translateX(-${currentImg}00%)`; // 백틱을 사용하여 슬라이드로 이동하는 애니메이션을 만듭니다.
  }, [currentImg]);
  const nextClick = useCallback(() => {
    if (currentImg >= totalImgs) {
      // 더 이상 넘어갈 슬라이드가 없으면
      setCurrentImg(0); // 1번째 사진으로
    } else {
      setCurrentImg(currentImg + 1);
    }
  }, [currentImg]);
  // Prev 버튼 클릭 시
  const prevClick = useCallback(() => {
    if (currentImg === 0) {
      setCurrentImg(totalImgs); // 마지막 사진으로
    } else {
      setCurrentImg(currentImg - 1);
    }
  }, [currentImg]);
  return (
    <S.CarouselContainer size={size}>
      <S.CarouselPrev onClick={prevClick} />
      <S.CarouselNext onClick={nextClick} />
      <S.CarouselWrapper ref={CarouselWrapper}>
        {
          imgs.map((v,i) => {
          <S.CarouselImg src={v} key={i} size={size}/>//props로 받은 사이즈로 width,height 결정
          })
        }
      </S.CarouselWrapper>
    </S.CarouselContainer>
  );
};
export default Carousel;

//style
export const CarouselContainer = styled.div`
  width: ${(props) => props.size};
  height: ${(props) => props.size};
  overflow: hidden;
  position: relative;
`;

export const CarouselWrapper = styled.div`
  display: flex;
`;

export const CarouselImg = styled.img`
  width: ${(props) => props.size};
  height: ${(props) => props.size};
`;

export const CarouselPrev = styled(GrFormPrevious)`
  border: none;
  position: absolute;
  top: 50%;
  left: 1%;
  font-size: 3rem;
  background-color: #fff;
  z-index: 10;
  cursor: pointer;
  border-radius: 50%;
`;
export const CarouselNext = styled(GrFormNext)`
  border: none;
  position: absolute;
  top: 50%;
  right: 1%;
  font-size: 3rem;
  background-color: #fff;
  z-index: 10;
  cursor: pointer;
  border-radius: 50%;
`;

```

[참고](https://velog.io/@97godo/React-Hooks%EB%A1%9C-Carousel-%EB%A7%8C%EB%93%A4%EA%B8%B0)
