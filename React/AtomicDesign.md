# Atomic Design
> 컴포넌트를 원자(atoms), 분자(molecules), 혼합물(organisms), 물질 등의 개념으로 웹에 적용하여 인터페이스를 세분화한 디자인 시스템을 만드는 방법론
<img width="700" src="http://bradfrost.com/wp-content/uploads/2019/06/atomic-design-product.jpg">

## 구성
#### ATOMS
- 인풋, 라벨, 버튼 등 1차원적인 요소들.  
#### MOLECULES
- 그 자체로는 의미가 없거나, 의미가 흐린 atom들끼리 결합하여 만들어진 재사용성이 가능한 원자조합 결합체.  
#### ORGANISMS
- atom들의 그룹, molecules, 혹은 같은 성질을 가진 organism을 포함한 개념. 본격적인 uio. 
#### TEMPLATES
- 본격적인 organisms의 uio를 배치하는 레이아웃 구성.  
#### PAGES
- template에 실제 데이터 혹은 더미 데이터를 넣어 특정 인스턴스 페이지를 구성.    

## CSS
> 재사용성을 높이기 위한 `Styled-Component` 채택.
- 컴포넌트 생성과 동시에 스타일링 하기 때문에 스타일을 여러 곳에서 불러올 필요가 없음.
- css 파일의 중복 적용을 피할 수 있음.
- props 값을 스타일링 할 때 그대로 사용 가능.
- `styled-components-breakpoint`로 미디어 쿼리 대응 가능.
