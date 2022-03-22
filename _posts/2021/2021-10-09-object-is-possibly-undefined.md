---
title: "Object is possibly 'undefined'. (TS2532)"
date: 2021-10-09
tags:
  - React
  - Typescript
  - error
keywords:
  - react
  - typescript
  - javascript
  - tsS2532
  - error
---

> Object is possibly 'undefined'. (개체가 'undefined'인 것 같습니다.)

### 에러가 나는 이유
---

- TS가 판단하기에 객체가 비어 있을 수도 있을수도 있는데, 해당 객체의 내부 값을 사용하려고 하기때문이다.

### 예시

---

- 작업시 해당 에러가 발생했던 상황과 비슷한 예시 코드입니다.
- `ul.main > li` 클릭시 **idx** 에 **index**를 담아서 `ul.sub > li` 에  `subItemList` 값이 있을시 해당 값을 보여주려고 하였는데 에러가 발생

```tsx

(...생략)
  
  const items: itemProps[] = [
    {
      item: '메인 1번',
      subItemList: [
        {
          item: '서브 1번',
        },
        {
          item: '서브 1번',
        }
      ],
    },
    {
      item: '메인 2번',
    },
  ];

  const [idx, setIdx] = useState(0);

  const onClick = (idx: number) => {
    return setIdx(idx)
  }
  
  return (
    <>
    <ul className="main">
      {items.map((item, index) => {
        return(
          <li key={index} onClick={() => onClick(idx)}>
            {item}
          </li> 
        )
      })}
    </ul>
    <ul className="sub">
      {/* 에러가 발생했던 코드 */}
        {items[idx].subItemList.map((item, index) => {
          return(
            <li key={index} onClick={() => onClick(idx)}>
              {item}
            </li> 
          )
        })}
      </ul>    
  </>
}
```

### 해결방법

---

- **옵셔널 체이닝(optional chaining)**
    - 이 문법은 **ES2020**에 등장한 문법으로 오래된 브라우저들은 `polyfills` 가 필요할 수 있다.
    - ts가 값이 없을수도 있다고 판단한 `subItemList` 뒤에 `?.` 을 추가
    - 참조된 값이 null 또는 undefined 이더라도 에러가 발생하지 않고 undefined를 리턴한다

```tsx
  <ul className="sub">
    {/* 옵셔널 체이닝 추가 코드 */}
    {items[idx].subItemList?.map((item, index) => {
      return(
        <li key={index} onClick={() => onClick(idx)}>
          {item}
        </li> 
      )
    })}
  </ul> 
```



### 결론
---

ts가 값이 없을수도 있다고 판단한 경우에는 옵셔널체이닝 `(?.)` 을 사용하여 해당 값이 null 또는 undefined 이더라도 에러가 발생하지 않고 정상적으로 출력되는것을 확인할수있다.