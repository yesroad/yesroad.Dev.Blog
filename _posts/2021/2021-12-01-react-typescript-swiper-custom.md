---
title: "React + typescript 환경에서 swiper 커스텀하기"
date: 2021-12-01
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
![React + typescript 환경에서 swiper 커스텀하기](../images/2021/swiper.png)

> swiper 초기 세팅 

### Swiper 에서 커스텀을 위한 방법

---
> React에서는`useRef` 라는 Hook 이 있는데,
Swiper는 ref에 대한 type interface가 지정되어있지않아서 에러가 뜨게된다.

Swiper에 내장되어 있는 **onSwiper** 를 사용하여 커스텀이 가능하다.

- 예제 코드

```tsx
import { useState } from 'react';
import SwiperCore from 'swiper';

const Carousel = () => {
  const [isSwiper, setIsSwiper] = useState<SwiperCore>();

  const settings = useMemo<Swiper>(
    () => ({
      ...
      /** onSwiper 메소드를 사용하여 isSwiper에 swiper를 담는다. */
      onSwiper: (swiper) => {
        setIsSwiper(swiper);
      }}),
    []
  );

  return(
    <Swiper {...settings}>
      {children}
    </Swiper>
  )
}

```

- 사용하기에 앞서 `import SwiperCore from 'swiper';` 에서 SwiperCore 를 불러온 후 useState에 type을 `<SwiperCore>` 로 설정하여 준다.

### Swiper 커스텀 예제

---

- 위와 같이 `useState` 를 사용하여 swiper를 받아온 상태에서 작업한다.
- 재생 , 정지, (현재 인덱스 / 총 갯수) 표시 기능 구현

- `Swiper Components`
    
```tsx
const Carousel = ({
  ...
  children
  controller,
  autoplay,
}: CarouselProps) => {

  /** swiper값을 담음 */
  const [isSwiper, setIsSwiper] = useState<SwiperCore>();
  /** 자동재생 실행 여부 */
  const [isPlay, setIsPlay] = useState(Boolean(autoplay));
  /** 현재 슬라이드 인덱스 */
  const [currentIndex, setCurrentIndex] = useState(0);
  /** children의 갯수를 구함 */
  const totalIndex = useMemo(() => Children.count(children), [children]);

  const settings = useMemo<Swiper>(
    () => ({
      ...
      onSlideChange: (swiper) => setCurrentIndex(swiper.realIndex),
      onSwiper: (swiper) => {
        setIsSwiper(swiper);
      },
    }),
    [...],
     );

     // swiper 메소드를 사용하여 자동 재생
     const onPlay = useCallback(() => {
    isSwiper?.autoplay.start();
    setIsPlay(true);
  }, [isSwiper?.autoplay]);

  // swiper 메소드를 사용하여 정지
  const onPause = useCallback(() => {
    isSwiper?.autoplay.stop();
    setIsPlay(false);
  }, [isSwiper?.autoplay]);

      return (
        <Swiper {...settings}>
          {children}

          {controller && (
            <Controller
              currentIndex={currentIndex + 1}
              totalIndex={totalIndex}
              isPlay={isPlay}
              onToggle={() => (isPlay ? onPause() : onPlay())}
              />
          )}
      	</Swiper>
      );
};
```
    
- `Controller Components`
    
```tsx
    interface PagingProps {
      /** 총 슬라이드 인덱스 */
      totalIndex: number;
      /** 현재 슬라이드 인덱스 */
      currentIndex: number;
      /** autoplay 여부 */
      isPlay: boolean;
      /** 재생 / 정지 클릭 이벤트 */
      onToggle: () => void;
    }
    
    const Controller = ({
      totalIndex,
      currentIndex,
      onToggle,
    }: PagingProps) => {
    	return (
          <div>
            <button
              type="button"
              className="controller"
              onClick={onToggle}
              >
              {isPlay ? (
                정지
              ) : (
                재생
              )}
            </button>
            <div className="paging">
              <span>
                {currentIndex} / {totalIndex}
              </span>
            </div>
          </div>
    	);
    };
    
    export default Controller;
```