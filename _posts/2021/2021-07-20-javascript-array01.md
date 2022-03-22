---
title: "Javascript - 배열(array) 1편"
date: 2021-07-20
tags:
  - javascript
  - Array
keywords:
  - Array
  - length
  - indexOf
  - sort
  - reverse
  - toString
  - join
  - concat
  - some
  - merge
  - every
---
> Array, length, indexOf, sort, reverse, toString, join, concat, some, every

### Array

---

- JavaScript Array 전역 객체는 배열을 생성할 때 사용하는 객체입니다
- 배열의 순번은 0 부터 시작을 한다.

### 배열 생성 방법

---

1. 대괄호 ([ ])를 사용하여 만드는 방법
2. Array() 생성자 함수를 사용하여 배열을 생성하는 방법

```jsx
  // []를 사용하여 생성
  const array = [1, 2, 3, 4, 5]

  // []를 사용하여 생성시 배열 크기를 지정하는 방법
  // 콤마(,)의 갯수만큼 배열의 크기를 할당
  const size = [,,,,,]
  size.length // 5

  // Array() 생성자 함수를 사용하여 생성
  const array = new Array(1, 2, 3, 4, 5);

  // Array() 를 사용하여 생성시 배열 크기를 지정하는 방법
  // () 안에 원하는 크기를 입력
  const size = new Array(5)
  size.length // 5
```

### array[]

---

- 배열의 n번째 인덱스에 접근 하기 위하여 사용

```jsx
  const array = ['A', 'B', 'C', 'D', 'E'];

  array[0] // A
```

### length

---

- 배열의 총 갯수를 반환 한다.

```jsx
  const array = ['A', 'B', 'C', 'D', 'E'];

  array.length // 5
```

### indexOf

---

- 배열 내부 항목에서 해당 인덱스 찾기 위하여 사용
    - 배열에 해당 항목이 존재하지 않을 경우 -1 을 반환

```jsx
  const array = ['A', 'B', 'C', 'D', 'E'];

  array.indexOf('C') // 2
  array.indexOf('F') // -1
```

### sort

---

- 배열의 항목을 알파벳, 또는 지정된 함수에 따른 순서로 정렬 하기 위하여 사용

```jsx
  const array = [15, 12, 9, 10, 5, 3, 1, 2]

  // 지정된 함수가 없으면 오름차순, 유니코드 문자 순서로 정렬된다.
  array.sort() // [ 1, 10, 12, 15, 2, 3, 5, 9 ] 

  // 오름차순 정렬
  array.sort((a, b) => a - b) // [ 1, 2, 3, 5, 9, 10, 12, 15 ]

  // 내림차순 정렬
  array.sort((a, b) => b - a ) // [ 15, 12, 10, 9, 5, 3, 2, 1 ]
```

### reverse

---

- 배열의 순서를 반대로 바꿔주기 위하여 사용

```jsx
  const array = ['A', 'B', 'C', 'D', 'E'];

  array.reverse(); // ['E', 'D', 'C', 'B', 'A']
```

### toString

---

- 배열을 문자열로 바꾸어 리턴

```jsx
  const array = ['A', 'B', 'C', 'D', 'E'];

  array.toString() // "A, B, C, D, E"
```

### join

---

- 배열 원소 전부를 하나의 문자열로 합친다
    - value : 배열의 각 요소를 구분할 문자열

```jsx
  const array = ['A', 'B', 'C', 'D', 'E'];

  array.join() // A, B, C, D, E
  array.join('-') // A-B-C-D-E
  array.join('/') // A/B/C/D/E
```

### slice(begin, end)

---

- 배열 요소의 begin부터 end까지(end는 미포함)에 대한 새로운 배열 객체로 리턴
    - 전달받은 값이 - 일경우 마지막 요소부터 시작

```jsx
  const array = ['A', 'B', 'C', 'D', 'E'];

  array.slice(0,3) // ['A', 'B' , 'C']

  array.slice(-2); // ['D', 'E']
```

### concat

---

- 다수의 배열을 합치고 병합된 배열의 사본을 리턴

```jsx
  const array01 = ['A', 'B', 'C'];
  const array02 = ['D', 'E']
  const array03 = ['F', 'G']

  array01.concat(array02) // ['A', 'B' , 'C', 'D', 'E']
  array01.concat(array02, array03) // ['A', 'B' , 'C', 'D', 'E', 'F', 'G']
```

### some

---

- 지정된 함수의 결과가 true일 때까지 배열의 각 원소를 반복
    - item : 현재 배열의 요소
    - index : 현재 배열 요소의 위치

```jsx
  const array = [1, 2, 3, 4, 5];

  array.some((item, index) => {
      console.log(`${index} 번 ${item}`) // 2번까지 돌고 true 를 리턴
      return item % 2 === 0; // true
  })
```

### every(item, index)

---

- 배열의 모든 요소가 특정 조건을 만족하는지 확인
    - item : 현재 배열의 요소
    - index : 현재 배열 요소의 위치

```jsx
  const array = [1, 2, 3, 4, 5];

  array.every((item, index) => {
      console.log(`${index} 번 ${item}`) // 1번 부터 false 를 리턴
      return item % 2 === 0; // false
  })
```

[배열(Array) 2편 - unshift, push, shift, pop, splice, forEach, map, filter, reduce](https://yesroad.dev/javascript-array02/)