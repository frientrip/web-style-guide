# Frip Web Style Guide
프립 웹 프론트엔드 개발자들이 코드를 작성하고, 이해하는데 참고가 될 스타일 가이드입니다.

아래 가이드를 바탕으로 리뷰를 진행해주세요! 변경사항이 있을시 미팅 후 반영합니다.

📢 전반적인 자바스크립트 스타일 가이드는 기본적으로 [AirBnb의 Javascript styled guide](https://github.com/ParkSB/javascript-style-guide)를 따르고 있습니다.

## Naming
### 디렉토리
- 컴포넌트, 컨테이너, 특정 도메인 경우는 **PascalCase**로 명명합니다.
- 클래스 형태가 모인 모듈, 기타 유틸, 커스텀 훅 등인 경우는 **camelCase**로 명명합니다.
- 디렉토리 내에 여러개의 파일들이 들어있다면 **s**를 추가로 붙여 명명합니다.

**Good** 👍
```javascript
- Accordion, ProductDetailPage, Product
- utils, useQueryProductList
```

**Bad** 👎
```javascript
- accordion, UseQueryReviews
```

### 파일명
- 컴포넌트, 클래스 형태의 모듈인 경우는 **PascalCase**로 명명합니다.
- 기타 유틸, 타입, 커스텀 훅 등인 경우는 **camelCase**로 명명합니다.
- 단일 export 형태가 아니라면 **s**를 추가로 붙여 명명합니다.
- 디렉토리 내부 단일 파일이라면(파일이 하나인 형태) **index**로 명명합니다.
- 컴포넌트의 경우 파일명과 **동일**하게 명명합니다.

**Good** 👍
```javascript
- Button.tsx, models/ProductDetailViewModel.ts, PurchasePage/index.tsx
- types, functions

import Button from './Components/Button'
```

**Bad** 👎
```javascript
- button.tsx, models/productDetailViewModel.ts, PurchasePage/PurchasePage.tsx
- type, function

import Button from './Components/Button/index.tsx'
```

### 변수
- 변수 이름은 **camelCase**로 명명합니다.
- boolean 타입은 접두사로 **is**를 붙여 명명합니다.
- 배열과 같은 복수의 형태를 가진 변수는 **s**를 붙여 명명합니다.

**Good** 👍
```javascript
const isPurchase: boolean = true || false;
const subTitle: string = '';
const userLists: User[] = props.users;
```

**Bad** 👎
```javascript
- const SubTitle = 'tigger';
- const user = props.users;
```

### 함수
- 함수 이름은 **camelCase**로 명명합니다.
- get 동사는 범위가 넓고 추상적이므로 특정한 대상에 대한 확실한 동사를 사용합니다.
- 이벤트 핸들러의 경우 **접두사 + 명사 + 동사** 순으로 명명합니다.
- 이벤트 핸들러는 **handle** 접두사를 붙여 사용합니다.

**Good** 👍
```javascript
const fetchProductList = () => {
  // do something..
}

const searchProduct = () => {
  // do something..
}

// 이벤트 핸들러
const handleButtonClick = () => {
  // do something..
}
```

**Bad** 👎
```javascript
const getProduct = () => {
  // do something..
}

// 이벤트 핸들러
const click_button = () => {
  // do something..
}
```

### 상수
- 상수 이름은 **UPPER_SNAKE_CASE**로 명명합니다.

**Good** 👍
```javascript
const COLLECTION_LIST_PER_PAGE = 10;
```

**Bad** 👎
```javascript
const collection_list_per_page = 10;
```

### enum
- 열거형의 이름은 **PascalCase**로 명명합니다.

**Good** 👍
```javascript
enum BookingStatus {
  // do something..
}
```

**Bad** 👎
```javascript
enum BOOKING_STATUS {
  // do something..
}
```

### 약어
- 약어로 시작하는 경우에는 **소문자**로 명명합니다.
- 약어로 시작하는 경우가 아닐 때는 **대문자**로 명명합니다.

**Good** 👍
```javascript
const uuid = '';
const userID = 'tigger';
const imageURL = 'https://..'
```

**Bad** 👎
```javascript
const ID = '124233';
const URLLocation = '/products/123';
```

### 확장자
- 리액트 컴포넌트 파일에는 **.tsx** 확장자를 사용합니다.
- 타입스크립트가 적용된 모듈은 **.ts** 확장자를 사용합니다.

## 함수 형태
- 공통 및 유틸성으로 사용되는 함수는 **함수 선언**을 통해 사용합니다.
- 특정 모듈 혹은 컴포넌트에 종속된 함수는 **화살표 함수**를 통해 사용합니다.

**Good** 👍
```javascript
// 공통 유틸 함수
function formatNumber(num): string {
  // do something..
}

// 컴포넌트 내 이벤트 핸들러
const handleButtonClick = (): void => {
  // do something..
}
```

**Bad** 👎
```javascript
// 공통 유틸 함수
const removeHTMLTag = (html, tagName) => {
  // do something..
}

// 컴포넌트 내 이벤트 핸들러
function handleInputChange(): {
  // do something..
}

// 반환 타입 명시하지 않음
function loggedInUsers(): User[] {
  // do something..
}
```

### 반환 타입
- 리모트 커스텀 훅을 제외한 모든 함수는 반환 타입을 명시합니다.
  - 리모트 커스텀 훅의 경우 반환 타이핑의 시간대비 효율이 낮다고 판단하였습니다.
  - 반환 타입을 명시하는 이유는 타입스크립트 컴파일 단계에서 타입 추론에 대한 비용 감소에 있습니다.

**Good** 👍
```javascript
function formatNumber(num): string {
  // do something..
}

const handleClickButton = (): void => {
  // do something..
}

function useQueryProductDetail() {
  // do something..
}
```

**Bad** 👎
```javascript
// 반환 타입 명시하지 않음
function loggedInUsers() {
  // do something..
}

function useQueryProductDetail(): ProductDetailResponse {
  // do something..
}
```

## JSX
- JSX는 **PascalCase**로 명명합니다.
- 자식 컴포넌트가 없다면 항상 닫힘 태그를 사용합니다.

**Good** 👍
```react
<Button />
<PaginationGroup />

<Container>
  <Children />
</Container>
```

**Bad** 👎
```react
<Product_Detail />
<SERVICE_QNA />
```

### props
- props는 **camelCase**로 명명합니다.
- prop의 값이 불변의 true라면 생략합니다.

**Good** 👍
```react
<ProductDetail
  productId={12345678}
  productTitle="good"
  isPurchase
/>
```

**Bad** 👎
```react
<ProductDetail
  product_id={12345678}
  ProductTitle="bad"
  isPurchase={true}
/>
```

### key
- key 속성 값을 배열의 인덱스로 사용하지 않고 **유니크한 ID** 값을 사용합니다.

**Good** 👍
```react
{productLists.map((product) =>
  <Product
    key={product.id}
    {...product}
  />
)}
```

**Bad** 👎
```react
{productLists.map((product, index) =>
  <Product
    key={index}
    {...product}
  />
)}
```

### map
- 컴포넌트를 복수로 렌더링 할 때는 **화살표 함수**를 사용합니다.

**Good** 👍
```react
{productLists.map((product) =>
  <Product
    key={product.id}
    {...product}
  />
)}
```

**Bad** 👎
```react
{productLists.map(function (product) {
   return <product key={product.id} {...product} />
})}
```

## 속성

#### img
- img 태그의 **alt** 속성의 경우 반드시 포함시킵니다.
- alt의 속성 값으로 "image", "photo", "picture" 단어를 포함시키지 않습니다.
  - 이미 스크린리더는 위와 같은 단어를 이미지로 인지하고 있기 때문입니다.

**Good** 👍
```react
<img src="hello.jpg" alt="Me waving hello" />

<img src="hello.jpg" alt="" />

<img src="hello.jpg" role="presentation" />
```

**Bad** 👎
```react
<img src="hello.jpg" />

<img src="hello.jpg" alt="Picture of me waving hello" />
```

## ESLint & Prettier & StyleLint
프립 웹 커스텀 린트인 [eslint-config-frip](https://github.com/frientrip/eslint-config-frip)에서 정의한 린트 규칙을 사용합니다.

## License
본 문서의 저작권은 [김준형](https://github.com/fronttigger), [임수민](https://github.com/SuminLim), [프립](https://www.frip.co.kr)에게 있습니다.
