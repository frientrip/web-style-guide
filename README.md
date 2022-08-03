# 웹 스타일 가이드

💡 프립 웹 프론트엔드 개발자들이 코드를 작성하고, 이해하는데 참고가 될 스타일 가이드입니다.
아래 가이드를 바탕으로 리뷰를 진행해주세요! 변경사항이 있을시 미팅 후 반영합니다.

전반적인 자바스크립트 스타일 가이드는 기본적으로 [AirBnb의 Javascript styled guide](https://github.com/ParkSB/javascript-style-guide)를 따르고 있습니다.

**기존 레거시 코드 중 웹 스타일 가이드에 맞지 않은 경우에도 피처 개발 간 변경이 필요한 파일에 한해서 수정해주세요! (변수명 변경으로 도메인마다 수정이 불가피하여 볼륨이 커지는 경우 제외)**

## Naming

### 디렉토리

- 컴포넌트, 컨테이너, 특정 도메인 경우는 **PascalCase**로 명명합니다.
- 클래스 형태가 모인 모듈, 기타 유틸, 커스텀 훅 등인 경우는 **camelCase**로 명명합니다.
- 디렉토리 내에 여러개의 파일들이 들어있다면 **s**를 추가로 붙여 명명합니다.

**Good** 👍

```jsx
- Accordion, ProductDetailPage, Product
- utils, useQueryProductList
```

**Bad** 👎

```jsx
- accordion, UseQueryReviews
```

### 파일명

- 컴포넌트, 클래스 형태의 모듈인 경우는 **PascalCase**로 명명합니다.
- 기타 유틸, 타입, 커스텀 훅 등인 경우는 **camelCase**로 명명합니다.
- 단일 export 형태가 아니라면 **s**를 추가로 붙여 명명합니다.
- 디렉토리 내부 단일 파일이라면(파일이 하나인 형태) **index**로 명명합니다.
- 컴포넌트의 경우 파일명과 **동일**하게 명명합니다.

**Good** 👍

```jsx
- Button.tsx, models/ProductDetailViewModel.ts, PurchasePage/index.tsx
- types, functions
```

```jsx
import Button from './Components/Button'
```

**Bad** 👎

```
- button.tsx, models/productDetailViewModel.ts, PurchasePage/PurchasePage.tsx
- type, function
```

```jsx
import Button from './Components/Button/index.tsx'
```

### 변수

- 변수 이름은 **camelCase**로 명명합니다.
- boolean 타입은 접두사로 **is**를 붙여 명명합니다.
- 배열과 같은 복수의 형태를 가진 변수는 **List**를 붙여 배열임을 확실히 명시합니다.
- 이차원 배열일 경우 **Lists**를 붙여 배열의 배열임을 확실히 명시합니다.

**Good** 👍

```jsx
const isPurchase: boolean = true || false;
const subTitle: string = '';
const userList: User[] = props.users;
const categoryPathLists: CategoryPath[] = props.pathLists; // [[1234, 2345], [2345, 3456]]
```

**Bad** 👎

```jsx
- const SubTitle = 'tigger';
- const user = props.users;
- const categoryPaths = props.pathLists; // [[1234, 2345], [2345, 3456]]
```

### 함수

- 함수 이름은 **camelCase**로 명명합니다.
- get 동사는 범위가 넓고 추상적이므로 특정한 대상에 대한 확실한 동사를 사용합니다.
- 이벤트 핸들러의 경우 **접두사 + 명사 + 동사** 순으로 명명합니다.
- 이벤트 핸들러는 **handle** 접두사를 붙여 사용합니다.

**Good** 👍

```tsx
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

```jsx
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

```jsx
const COLLECTION_LIST_PER_PAGE = 10;
```

**Bad** 👎

```jsx
const collection_list_per_page = 10;
```

### enum

- 열거형의 이름은 **PascalCase**로 명명합니다.

**Good** 👍

```jsx
enum BookingStatus {
  // do something..
}
```

**Bad** 👎

```jsx
enum BOOKING_STATUS {
  // do something..
}
```

### 약어

- 약어로 시작하는 경우에는 **소문자**로 명명합니다.
- 약어로 시작하는 경우가 아닐 때는 **대문자**로 명명합니다.

**Good** 👍

```jsx
const uuid = '';
const userID = 'tigger';
const imageURL = 'https://..'
```

**Bad** 👎

```jsx
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

```jsx
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

```jsx
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

- 리모트 커스텀 훅을 제외한 모든 함수는 **반환 타입을 명시**합니다.
    - 리모트 커스텀 훅의 경우 반환 타이핑의 시간대비 효율이 낮다고 판단하였습니다.
    - 반환 타입을 명시하는 이유는 타입스크립트 컴파일 단계에서 타입 추론에 대한 비용 감소에 있습니다.

**Good** 👍

```jsx
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

```jsx
// 반환 타입 명시하지 않음
function loggedInUsers() {
  // do something..
}

function useQueryProductDetail(): ProductDetailResponse {
  // do something..
}
```

## 조건문

- 렉시컬 선언을 포함하는 case, default 구문 안에 블록을 만들 때는 괄호를 사용하세요

**Good** 👍

```jsx
switch (foo) {
  case 1: {
    let x = 1;
    break;
  }
  case 2: {
    const y = 2;
    break;
  }
  case 3: {
    function f() {
      // ...
    }
    break;
  }
  case 4:
    bar();
    break;
  default: {
    class C {}
  }
}
```

**Bad** 👎

```jsx
switch (foo) {
  case 1:
    let x = 1;
    break;
  case 2:
    const y = 2;
    break;
  case 3:
    function f() {
      // ...
    }
    break;
  default:
    class C {}
}
```

## 속성

### img

- img 태그의 **alt** 속성의 경우 반드시 포함시킵니다.
- alt의 속성 값으로 "image", "photo", "picture" 단어를 포함시키지 않습니다.
    - 이미 스크린리더는 위와 같은 단어를 이미지로 인지하고 있기 때문입니다.

**Good** 👍

```jsx
<img src="hello.jpg" alt="Me waving hello" />

<img src="hello.jpg" alt="" />

<img src="hello.jpg" role="presentation" />
```

**Bad** 👎

```jsx
<img src="hello.jpg" />

<img src="hello.jpg" alt="Picture of me waving hello" />
```

## Typescript

### 타입 선언

- 객체 형태의 타입을 지정할 때에는 **interface**를 사용합니다.
- 그 외 선언 병합 등 유틸리티 타입을 사용하는 경우에는 **type**을 사용합니다.

**Good** 👍

```tsx
interface GoodType {
	stringProperty: string;
	numberProperty: number;
}

type GoodType = Pick<GoodType, 'stringProperty'>
```

**Bad** 👎

```jsx
type BadType = {
	stringProperty: string;
	numberProperty: number;
}
```

### Properties

- 인터페이스 내 property는 **primitive/object property**, **function property**의 순서로 구분하여 선언합니다.

**Good** 👍

```jsx
interface GoodType {
	stringProperty: string;
	numberProperty: number;
	objectProperty: {
		nestedProperty: string | number;
	};

	onClick: () => void
}
```

**Bad** 👎

```jsx
// primitive property와 object property간 줄바꿈을 한 경우
interface BadType {
	stringProperty: string;
	numberProperty: number;

	objectProperty: {
		nestedProperty: string | number;
	};

	onClick: () => void
}

// primitive/object property와 function property 사이 줄바꿈을 하지 않은 경우 
interface BadType {
	stringProperty: string;
	numberProperty: number;
	objectProperty: {
		nestedProperty: string | number;
	};
	onClick: () => void
}
```

## JSX

- JSX는 **PascalCase**로 명명합니다.
- 자식 컴포넌트가 없다면 항상 닫힘 태그를 사용합니다.

**Good** 👍

```jsx
<Button />
<PaginationGroup />

<Container>
  <Children />
</Container>
```

**Bad** 👎

```jsx
<Product_Detail />
<SERVICE_QNA />
```

### props

- props는 **camelCase**로 명명합니다.
- prop의 값이 불변의 true라면 생략합니다.

**Good** 👍

```jsx
<ProductDetail
  productId={12345678}
  productTitle="good"
  isPurchase
/>
```

**Bad** 👎

```jsx
<ProductDetail
  product_id={12345678}
  ProductTitle="bad"
  isPurchase={true}
/>
```

### key

- key 속성 값을 배열의 인덱스로 사용하지 않고 **유니크한 ID** 값을 사용합니다.

**Good** 👍

```jsx
{productLists.map((product) =>
  <Product
    key={product.id}
    {...product}
  />
)}
```

**Bad** 👎

```jsx
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

```jsx
{productLists.map((product) =>
  <Product
    key={product.id}
    {...product}
  />
)}
```

**Bad** 👎

```jsx
{productLists.map(function (product) {
   return <product key={product.id} {...product} />
})}
```

### styled-components

- styled-component로 선언이 필요없는 태그의 경우 일반 JSX(소문자)로 사용하거나 React.Fragment를 이용합니다.

**Good** 👍

```jsx
// style이 필요없는 img 태그
<img src={iconImported} alt="next-button" />

// style이 필요없는 container 태그
<div>
	{getSomeTexts()}
</div>
```

**Bad** 👎

```jsx
// style이 적용되어 있지 않은 태그ㅈ
const NonStyledDiv = styled.div``

<NonStyledDiv>
	{getWrongText()}
</NonStyledDiv>
```

## React / ESLint & Prettier & StyleLint

프립 웹 커스텀 린트인 [eslint-config-frip](https://github.com/frientrip/eslint-config-frip)에서 정의한 린트 규칙을 사용할 예정입니다. (개발 중)

### hook

**순서**

- 다음과 같은 순서로 선언하여 사용합니다.
    1. react/react-router-dom 등 외부 라이브러리에서 제공하는 hook
    2. 프로젝트 내에서 생성한 custom hook

**Good** 👍

```jsx
// custom hooks first
const { toast } = useToast()

const { productDetailPageData } = useQueryProductDetailPageData(id);

// native hooks
const [isHello, setIsHello] = useState(false)
const [data, setData] = useState<DataType>()

const ref = useRef()
```

**Bad** 👎

```jsx
// 순서 지켜지지 않음
const [isHello, setIsHello] = useState(false)
const { toast } = useToast()

const { productDetailPageData } = useQueryProductDetailPageData(id);
const [data, setData] = useState<DataType>()

const ref = useRef()
```

**기능별**

- 컴포넌트 내 사용된 hook의 성격 및 기능에 따라 줄바꿈으로 분리합니다.
- 성격 및 기능 순서는 정해져있지 않습니다.

**Good** 👍

```jsx
// Message 관련
const { toast } = useToast()
const { customAlert } = useAlert()
const { message } = useMessage('purchase')

// GQL
const { productDetailPageData } = useQueryProductDetailPageData(id);
const { downloadCouponMutation } = useDownloadCouponMutation();

// 유틸
const { page } = usePage()
const { scroll } = useScroll()

const [isHello, setIsHello] = useState(false)

const ref = useRef()
```

**Bad** 👎

```jsx
// 기능 및 성격 분리되지 않음
const { toast } = useToast()
const { productDetailPageData } = useQueryProductDetailPageData(id);

const { customAlert } = useAlert()
const { downloadCouponMutation } = useDownloadCouponMutation();

const { message } = useMessage('purchase')
```

### Import order

- 파일 내 모듈을 import할 경우 react, builtin(빌트인 모듈), external(외부 모듈), internal(내부 모듈 / 절대 경로), parent & siblings(상대 경로), unsigned(css import) 순으로 import합니다.
- 각 Group 간 줄바꿈을 적용해야하며 Group 내부에서는 줄바꿈을 허용하지 않습니다.
- Group 내부의 순서는 영향을 주지 않습니다.
- 주석은 포함하지 않습니다.
- 절대 경로가 설정되어 있지 않은 경우 internal과 parent & siblings을 같은 Group에 포함합니다.

**Good** 👍

절대 경로를 사용할 경우

```jsx
// react & react-dom
import React from 'react'

// builtin
import fs from 'fs'

// external
import { BrowserRouter, Redirect, Route, Switch } from 'react-router-dom'

// internal
import Home from '#pages/Home'
import MyComponent from '#components/MyComponent'

// parent & siblings
import parent from '../utils/env'
import siblings from './innerFolder/sibling'

// unsigned import
import '../style.css'
```

상대 경로만 사용할 경우

```jsx
// react & react-dom
import React from 'react'

// builtin
import fs from 'fs'

// external
import { BrowserRouter, Redirect, Route, Switch } from 'react-router-dom'

// internal
import Home from '../../pages/Home'
import MyComponent from '../../components/MyComponent'
import parent from '../utils/env'
import siblings from './innerFolder/sibling'

// unsigned import
import '../style.css'
```

**Bad** 👎

```jsx
/* Group 간 줄바꿈이 적용되지 않은 경우 */
// react & react-dom
import React from 'react'
// builtin
import fs from 'fs'

/* Group 내 줄바꿈이 적용된 경우 */
// internal
import Home from '../../pages/Home'

import MyComponent from '../../components/MyComponent'

/* 순서가 맞지 않은 경우 */
// internal
import Home from '../../pages/Home'
// builtin
import fs from 'fs'
import siblings from './innerFolder/sibling'
```

## styled-components

### CSS order

- Declarations, Nested rules, At-Nested rules, custom-mixins/custom-functions 순으로 작성합니다.
    - **스타일 그룹 순서**
        - **Declarations**
            
            일반 css properties로 `속성 : 값`으로 된 코드만 해당됩니다.
            Group 순서는 다음과 같으며 Group 내부 순서 또한 명시된 순서대로 적용됩니다.
            
            - **Display Group** (position, display, flex, overflow …)
                
                ```jsx
                'content',
                'position',
                'top',
                'right',
                'bottom',
                'left',
                'z-index',
                'display',
                'vertical-align',
                'flex',
                'flex-grow',
                'flex-shrink',
                'flex-basis',
                'flex-direction',
                'flex-flow',
                'flex-wrap',
                'grid',
                'grid-area',
                'grid-template',
                'grid-template-areas',
                'grid-template-rows',
                'grid-template-columns',
                'grid-row',
                'grid-row-start',
                'grid-row-end',
                'grid-column',
                'grid-column-start',
                'grid-column-end',
                'grid-auto-rows',
                'grid-auto-columns',
                'grid-auto-flow',
                'grid-gap',
                'grid-row-gap',
                'grid-column-gap',
                'gap',
                'row-gap',
                'column-gap',
                'align-content',
                'align-items',
                'align-self',
                'justify-content',
                'justify-items',
                'justify-self',
                'order',
                'float',
                'clear',
                'object-fit',
                'overflow',
                'overflow-x',
                'overflow-y',
                'overflow-scrolling',
                'clip',
                ```
                
            - **Content Group** (width, margin, border …)
                
                ```jsx
                'box-sizing',
                'width',
                'min-width',
                'max-width',
                'height',
                'min-height',
                'max-height',
                'margin',
                'margin-top',
                'margin-right',
                'margin-bottom',
                'margin-left',
                'padding',
                'padding-top',
                'padding-right',
                'padding-bottom',
                'padding-left',
                'border',
                'border-spacing',
                'border-collapse',
                'border-width',
                'border-style',
                'border-color',
                'border-top',
                'border-top-width',
                'border-top-style',
                'border-top-color',
                'border-right',
                'border-right-width',
                'border-right-style',
                'border-right-color',
                'border-bottom',
                'border-bottom-width',
                'border-bottom-style',
                'border-bottom-color',
                'border-left',
                'border-left-width',
                'border-left-style',
                'border-left-color',
                'border-radius',
                'border-top-left-radius',
                'border-top-right-radius',
                'border-bottom-right-radius',
                'border-bottom-left-radius',
                'border-image',
                'border-image-source',
                'border-image-slice',
                'border-image-width',
                'border-image-outset',
                'border-image-repeat',
                'border-top-image',
                'border-right-image',
                'border-bottom-image',
                'border-left-image',
                'border-corner-image',
                'border-top-left-image',
                'border-top-right-image',
                'border-bottom-right-image',
                'border-bottom-left-image',
                
                ```
                
            - **Background Group** (background, outline, list-style …)
                
                ```jsx
                'background',
                'background-color',
                'background-image',
                'background-attachment',
                'background-position',
                'background-position-x',
                'background-position-y',
                'background-clip',
                'background-origin',
                'background-size',
                'background-repeat',
                'box-decoration-break',
                'box-shadow',
                'outline',
                'outline-width',
                'outline-style',
                'outline-color',
                'outline-offset',
                'table-layout',
                'caption-side',
                'empty-cells',
                'list-style',
                'list-style-position',
                'list-style-type',
                'list-style-image',
                ```
                
            - **Text Group** (color, font-, text-, word- …)
                
                ```jsx
                'color',
                'font',
                'font-weight',
                'font-style',
                'font-variant',
                'font-size-adjust',
                'font-stretch',
                'font-size',
                'font-family',
                'src',
                'line-height',
                'letter-spacing',
                'quotes',
                'counter-increment',
                'counter-reset',
                '-ms-writing-mode',
                'text-align',
                'text-align-last',
                'text-decoration',
                'text-emphasis',
                'text-emphasis-position',
                'text-emphasis-style',
                'text-emphasis-color',
                'text-indent',
                'text-justify',
                'text-outline',
                'text-transform',
                'text-wrap',
                'text-overflow',
                'text-overflow-ellipsis',
                'text-overflow-mode',
                'text-shadow',
                'white-space',
                'word-spacing',
                'word-wrap',
                'word-break',
                'overflow-wrap',
                'tab-size',
                'hyphens',
                'interpolation-mode',
                ```
                
            - **Visiblility Group** (opacity, visibility, cursor, pointer-events …)
                
                ```jsx
                'opacity',
                'visibility',
                'filter',
                'resize',
                'cursor',
                'pointer-events',
                'user-select',
                ```
                
            - **ETC Group** (column-, break-, page-, zoom, fill, stroke- …)
                
                ```jsx
                'unicode-bidi',
                'direction',
                'columns',
                'column-span',
                'column-width',
                'column-count',
                'column-fill',
                'column-gap',
                'column-rule',
                'column-rule-width',
                'column-rule-style',
                'column-rule-color',
                'break-before',
                'break-inside',
                'break-after',
                'page-break-before',
                'page-break-inside',
                'page-break-after',
                'orphans',
                'widows',
                'zoom',
                'max-zoom',
                'min-zoom',
                'user-zoom',
                'orientation',
                'fill',
                'stroke',
                'stroke-width',
                'stroke-linecap',
                ```
                
            - **Transition Group** (transition-, transform-, animation- …)
                
                ```jsx
                'transition',
                'transition-delay',
                'transition-timing-function',
                'transition-duration',
                'transition-property',
                'transform',
                'transform-origin',
                'animation',
                'animation-name',
                'animation-duration',
                'animation-play-state',
                'animation-timing-function',
                'animation-delay',
                'animation-iteration-count',
                'animation-direction',
                'animation-fill-mode',
                ```
                
        - **Nested rules**
            
            Nesting으로 tag를 추가하거나 selector를 사용한 경우에 해당합니다.
            
        - **At-Nested rules**
            
            Nesting된 media-query, keyframes 등의 경우에 해당합니다.
            
        - **custom-mixins**
            
            custom으로 정의된 mixin을 사용할 경우 해당합니다.
            
        - **custom-functions**
            
            custom으로 정의된 함수를 사용할 경우 해당합니다.
            
- Group 간, Block 간은 줄바꿈을 적용합니다.
- Group 내부에서는 줄바꿈을 적용하지 않습니다.

📌 stylelint 적용된 프로젝트일 경우

참고 사항)
declarations(일반 속성)만 사용한 styled component의 경우 autofix가 적용되지만
custom-mixins/function을 포함하여 사용한 styled component의 경우 autofix가 적용되지 않습니다.

⚠️ **stylelint 미적용된 프로젝트일 경우**

Declarations(일반 속성)은 최대한 순서에 맞게 적용합니다. (순서는 하나하나 정확하게 X)
속성 그룹은 **스타일 그룹 순서** 가이드에 따라 블럭으로 수동으로 나눕니다.

**Good** 👍

```jsx
const StyledComponent = styled.div`
  /* declarations - 일반 속성 */
  margin-top: 4px;

  color: red;

  /* rules - nested selector, pseudo selector */
  div {
    background-color: aliceblue;
  }

  &:hover {
    color: gray;
  }

  /* at-rules - @ selector */
  @keyframes myAnimation {
		/* animation */
  }

  /* custom-mixin */
  ${media.desktop`
	   display: block;
  `}

  /* custom-function */
  ${({ theme }) => theme.fonts.R50};
`
```

**Bad** 👎

```jsx
// Group 간 줄바꿈이 적용되지 않은 경우
const StyledComponent = styled.div`
  /* Content Group */
  margin-top: 4px;
  /* Text Group */
  color: red;
`

// Group 내 줄바꿈이 적용된 경우
const StyledComponent = styled.div`
  /* Text Group */
  color: red;

	font-size: 16px
`

// Group 간 순서 혹은 Group 내 순서가 맞지 않은 경우
const StyledComponent = styled.div`
  /* Text Group */
	font-size: 16px
  color: red;

  /* Content Group */
  margin-top: 4px;
`
```
