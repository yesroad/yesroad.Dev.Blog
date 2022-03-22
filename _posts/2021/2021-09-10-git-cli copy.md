---
title: "React Typescript 환경에서 Slick 사용하기"
date: 2021-09-10
tags:
  - react
  - typescript
  - slick
  - slider
keywords:
  - react
  - typescript
  - slick
  - slider
---

## Slick

리액트 프로젝트에서 슬라이더를 쉽게 구현할수 있도록 도와주는 모듈.

> [npm React Slick](https://www.npmjs.com/package/react-slick)<br/> 
> [React Slick 홈페이지](https://react-slick.neostack.com/)<br/>
> [슬라이드 종류](https://react-slick.neostack.com/docs/example/simple-slider)

### 설치

1. creact react app typescript 설치
```jsx
  $ npx create-react-app react-ts-slick --template typescript
```


2. slick slider 설치
```jsx
  $ npm i react-slick @types/react-slick slick-carousel
```

- `react-slick` : react 에서 사용 가능한 slick 슬라이드
- `@types/react-slick` : typescript 에서 slick 를 사용하기위한 type interface가 정의되어있다.
- `slick-carousel` : slick 에서 사용할 css 를 import 하기위함

```jsx
  // Import css files
  import "slick-carousel/slick/slick.css";
  import "slick-carousel/slick/slick-theme.css"
```
---
### 기본 구조

> styled-component 를 사용하여 작업하였다.

1. `src/slider/Slick.tsx`

```jsx
import { useMemo } from 'react';
import styled from 'styled-components';
import Slider, { Settings } from 'react-slick';

import 'slick-carousel/slick/slick.css';
import 'slick-carousel/slick/slick-theme.css';

const SlideWrapper = styled.section`
  position: relative;
`;

interface sliderProps {
  /** 슬라이더 아이템 요소 */
  children: React.ReactNode;
  /** 커스텀 클래스 */
  className?: string;
  /** 자동재생 (속도 설정시 number 타입으로) */
  autoplay?: boolean | number;
  /** 슬라이더 속도 */
  speed?: number;
  /** 반복 여부 */
  loop?: boolean;
}

function Slick({
  children,
  className,
  autoplay = true,
  speed = 300,
  loop = true,
}: sliderProps) {
  const settings = useMemo<Settings>(
    () => ({
      dots: true,
      infinite: loop,
      speed: speed,
      slidesToShow: 1,
      autoplay: Boolean(autoplay),
      autoplaySpeed: typeof autoplay === 'boolean' ? 3000 : autoplay,
    }),
    [autoplay, loop, speed],
  );
  return (
    <SlideWrapper className={className}>
      <Slider {...settings}>{children}</Slider>
    </SlideWrapper>
  );
}

export default Slick;

```

- 추후에 다른곳에서도 슬라이더를 사용할수 있으므로, 슬라이더 아이템 영역은 `children` 을 사용하여 다른 컴포넌트에서 받아올 수 있게 작성
- 상단 import 부분 `import Slider, { Settings } from 'react-slick';` 에서 불러온 Settings 에 slick 옵션에 대한 type interface 가 정의되어있다.
- `const settings = {}` 항목에 Settings 를받아서 옵션값을 설정

2. `src/components/Item.tsx`

```jsx
import styled from 'styled-components'
import Slick from '../Slider';

interface itemsProps {
  item: string,
  name: string
}

const SliderItem = styled.div`
  width: 100%;
  img{
    max-width: 100%;
    height: auto;
  }
`;

const items:itemsProps[] = [
  {
    item: 'http://placehold.it/1200x400',
    name: '이미지01'
  },
  {
    item: 'http://placehold.it/1200x400/ff0000',
    name: '이미지02'
  },
  {
    item: 'http://placehold.it/1200x400/00ffff',
    name: '이미지03'
  },    
]

function Item() {
  return (
    <Slick>
      {items.map((item, index) => (
        <SliderItem key={index}>
          <img src={item.item} alt={item.name} />
        </SliderItem>
      ))}
    </Slick>
  );
}

export default Item;
```

- `Item` 컴포넌트에서는 `Slick.tsx` 를 import 하여 `<slick>` 내부에 아이템 리스트를 작성하여준다.
- `Slick.tsx` 에서 정의한 `sliderProps` 중 변경이 필요할시 `Slick.tsx` 에 props 를 전달하여 해당 옵션값을 변경할수 있다. `ex) <Slick autoplay={false} >`
---
<br/>

### 참고사이트

Slick 을 사용하여 작업시 필요한 옵션 및 메소드에 대한 정보는 아래 사이트에 정리가 잘 되어있어, 추가적인 설정이 필요한 경우에는 아래 문서를참고하는게 빠르고 정확하다.

[Slick API](https://react-slick.neostack.com/docs/api)