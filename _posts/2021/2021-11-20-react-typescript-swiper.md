---
title: "React Typescript 환경에서 Swiper 사용하기"
date: 2021-11-20
tags:
  - react
  - typescript
  - swiper
  - slider
keywords:
  - react
  - typescript
  - slick
  - slider
---
![React Typescript 환경에서 Swiper 사용하기](../images/2021/swiper.png)
### Swiper

---

리액트 프로젝트에서 슬라이더를 쉽게 구현할수 있도록 도와주는 모듈.

> [React Swiper 사용법](https://swiperjs.com/react)<br/> 
> [Swiper Demos](https://swiperjs.com/demos)<br/>
> [npm React Swiper](https://www.npmjs.com/package/swiper)

### 설치

---

> swiper 는 추가 패키지 설치 없이 typescript 지원이 된다.

1. creact react app typescript 설치

```jsx
$ npx create-react-app react-ts-swiper --template typescript
```

1. slick slider 설치

```jsx
$ npm i swiper
```

- `swiper`  : react 에서 사용 가능한 Swiper 슬라이드

### 기본 구조

---

- `import { Swiper, SwiperSlide } from 'swiper/react'` 를 import해서 사용 해야한다.
- autoplay, Pagination, navigation 등 을 사용하기 위해서는 [SwiperCore](https://swiperjs.com/swiper-api#custom-build) 에서 불러온 후 `SwiperCore.use([])` 에 등록을해줘야 사용 가능하다.

1. `src/slider/Swiper.tsx` 
    
```tsx
    import { Children, useCallback, useMemo } from 'react';
    import { Swiper } from 'swiper/react';
    import SwiperCore, { Pagination, Autoplay } from 'swiper';
    
    /** SwiperCore 사용 */
    SwiperCore.use([Pagination, Autoplay]);
    
    interface CarouselProps {
    	children: React.ReactNode;
    	indicator: boolean;
    }
    
    const Carousel = ({
    	item,
    	indicator
    }: CarouselProps) => {;
    
    	/** Swiper option 설정 */
    	/** on 메소드를 사용하지 않으면 useMemo<SwiperOptions>로 대체 가능 */
    const settings = useMemo<Swiper>(
      () => ({
          spaceBetween: 10,
          autoplay: {
            delay: 4000
          },
          pagination: indicator && {
            clickable: true,
          },
      }),
      [indicator]
    );
    
    return (
   	/** Swiper에 option값을 받아와서 적용 */
        <Swiper {...settings}>
          {children}
        </Swiper>
      );
    };
    
    export default Carousel;
```
    
- 재사용성을 고려하여 슬라이드 아이템은 자식 컴포넌트로 넘겨받을것이기에 `children` 으로 설정해준다.
- 상단 import 부분 `import { Swiper } from 'swiper/react';` 파일 안에 swiper 옵션에 대한 type interface 가 정의되어있다.
    - `on method` 없이 옵션값만 사용할 경우 `SwiperOptions` 를 사용할 수 도 있다.
- `const settings = {}` 항목에 `Swiper 또는 SwiperOptions` 을 넘겨받아서 옵션값을 설정

1.  `Item Components`
    
```tsx
    import { SwiperSlide } from 'swiper/react';
    
    interface itemsProps {
      item: string,
      name: string
    }
    
    const items:itemsProps[] = [
      {
        item: 'http://placehold.it/1200x400',
        name: '이미지01'
      },
    	...   
    ]
    
    const Item = () => {
      return (
        <Swiper>
          {items.map((item, index) => (
            <SwiperSlide key={index}>
              <img src={item.item} alt={item.name} />
            </SwiperSlide>
          ))}
        </Swiper>
      );
    }
    
    export default Item;
```    
- 아이템 리스트는 `import { SwiperSlide } from 'swiper/react';` 를 불러와서 `SwiperSlide` 로 감싸서 사용해야만한다.

---
<br/>

### 참고사이트

Swiper 을 사용하여 작업시 필요한 옵션 및 메소드에 대한 정보는 아래 사이트에 정리가 잘 되어있어, 추가적인 설정이 필요한 경우에는 아래 문서를참고하는게 빠르고 정확하다.

[Swiper APi](https://swiperjs.com/swiper-api)

---
[react + typescript 환경에서 swiper 커스텀](https://yesroad.dev/react-typescript-swiper-coustom/)