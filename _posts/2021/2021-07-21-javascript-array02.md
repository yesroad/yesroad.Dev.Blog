---
title: "Javascript - 배열(array) 2편"
date: 2021-07-21
tags:
  - javascript
  - Array
keywords:
  - Array
  - unshift
  - push
  - shift
  - pop
  - splice
  - forEach
  - map
  - filter
  - merge
  - reduce
---

[배열(Array) 1편 - Array, length, indexOf, sort, reverse, toString, join, concat, some, every](https://yesroad.dev/javascript-array01/)

<br/>

> unshift, push, shift, pop, splice, forEach, map, filter, reduce

### unshift

---

- 배열의 맨앞에 새로운 항목을 추가

```jsx
  const array = ['A', 'B', 'C', 'D', 'E'];

  array.unshift(0); // [0, 'A', 'B', 'C', 'D', 'E']
```

### push

---

- 배열의 마지막에 새로운 항목을 추가

```jsx
  const array = ['A', 'B', 'C', 'D', 'E'];

  array.push(7); // ['A', 'B', 'C', 'D', 'E', 7]
```

### shift

---

- 배열의 맨앞에있는 항목을 제거

```jsx
  const array = ['A', 'B', 'C', 'D', 'E'];

  array.shift(); // ['B', 'C', 'D', 'E']
```

### pop

---

- 배열의 마지막에있는 항목을 제거

```jsx
  const array = ['A', 'B', 'C', 'D', 'E'];

  array.pop(); // ['A', 'B', 'C', 'D',]
```

### splice(start, count, item1, item2 ...)

---

- 기존 요소를 삭제 또는 교체하거나 새 요소를 추가
    - start : 시작할 요소의 인덱스
    - count : 제거할 요소의 갯수
    - item1, item2 ... : 배열에 추가할 요소 ( 지정하지 않을시 추가 없이 제거만 실행 )

```jsx
  const array = ['A', 'B', 'C', 'D', 'E'];

  array.splice(2, 1) // ['A', 'B', 'D', 'E']
  array.splice(0, 2) // ['C', 'D', 'E']
  array.splice(3, 0, 'F') // ['A', 'B' ,'C', 'F', 'D', 'E']
```

### forEach(item, intex)

---

- 배열의 각 요소를 한 번씩 실행
    - item : 실행할 배열의 요소
    - index : 배열의 순번

```jsx
  const array = ['A', 'B', 'C', 'D', 'E'];

  array.forEach((item) => 
    console.log(item) // A B C D
  );
```

### map(item, index)

---

- 배열의 각 원소를 지정된 함수로 실행하여 새로운 배열을 리턴
    - item : 실행할 배열의 요소

```jsx
  const array = [1, 2, 3, 4];

  // 함수 표현식으로 선언
  const arrayMap = array.map((item) => 
      item * 2
  )

  arrayMap // [2, 4, 6, 8]
```

### filter(item)

---

- 배열의 각 원소를 지정된 함수로 실행하며 true 인 원소들로 새로운 배열을 리턴
    - item : 처리할 배열의 요소

```jsx
  const array = [1, 2, 3, 4, 5, 6];

  // 함수 표현식으로 선언
  const arrayFilter = array.filter((item) => 
      item %2 === 0
  )

  arrayFilter // [2, 4, 6]
```

### reduce(prevItem, currentItem, index)

---

- 배열의 각 원소를 지정된 함수로 실행하며 true 인 원소들로 새로운 배열을 리턴
    - prevItem : 이전 콜백 함수에서 리턴한 값
    - currentItem : 현재 배열 요소의 값

```jsx
  const array = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

  // 함수 표현식으로 선언
  const arrayReduce = array.reduce((prevItem, currentItem) => 
      prevItem + currentItem
  )

  arrayReduce // 55
```