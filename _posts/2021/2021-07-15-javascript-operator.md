---
title: "Javascript - 연산자 (operator)"
date: 2021-07-15
tags:
  - javscript
keywords:
  - javscript
  - operator
  - arithmetic 
  - increment
  - decrement
  - assignment
  - comparison
  - logical
---
### 연산자(operator)

- 연산자란 프로그래밍에서 쓰이는 기호들이며, 연산자의 종류에는 산술, 증감, 비교, 대입, 삼항, 논리 등이 있습니다.

### 산술 연산자 ( Arithmetic Operator )

---

- 값을 피연산자로 받아 하나의 숫자값을 반환
    
```jsx
const i = 10;
const j = 4;

console.log(i + j) // 10 + 4 = 14;
console.log(i - j) // 10 - 4 = 6;
console.log(i * j) // 10 * 4 = 40;
console.log(i / j) // 10 / 4 = 2.5;
console.log(i % j) // 2 ( 나눈 나머지 값 )
```
    

### 증감 연산자 ( increment and decrement operator )

---

- 값을 피연산자로 받아 하나의 숫자값을 반환
    - 연산자 뒤에 ++ (접미사) 이 붙으면 증가하기 전의 값을 반환
    - 연산자 앞에 ++ (접두사) 이 붙으면 증가한 후의 값을 반환
    - 연산자 뒤에 -- (접미사) 이 붙으면 감소하기 전의 값을 반환
    - 연산자 앞에 -- (접두사) 이 붙으면 감소한 후의 값을 반환
    
```jsx
const i = 1;

console.log(i++) // 1
console.log(++i) // 2
console.log(i--) // 1
console.log(--i) // 0
```
    

### 대입 연산자 ( Assignment Operator )

---

- 변수에 값을 대입할 때 사용하는 이항 연산자
    
```jsx
let i = 10

// 왼쪽 피연산자에 오른쪽 피연산자의 값을 대입
console.log(i -= 4) // 6 ( a = i - 4 )
console.log(i += 4) // 14 ( b = i + 4 )
console.log(i *= 4) // 40 ( c = i * 4 )
console.log(i /= 4) // 2.5 ( d = i / 4 )
console.log(i %= 4) // 2 ( e % 4 = 2 )
```
    

### 비교 연산자( Comparison Operator )

- 피연산자들을 비교하고 비교에 따라 논리 값을 반환 ( true / false )
    
```jsx
const i = 10;
const j = 4;

console.log(i == j) // 동등 false (값이 같으면 true)
console.log(i != j) // 부등 true (값이 다르면 true)
console.log(i === j) // 일치 false (값과 타입이 같으면 true)
console.log(i !== j) // 불일치 true (값과 타입이 다르면 true)
console.log(i > j) // ~ 보다 큰 true
console.log(i >= j) // ~ 보다 크거나 같은 true
console.log(i < j) // ~ 보다 작은 false
console.log(i <= j) // ~ 보다 작거나 같은 false
```
    

### 논리 연산자 ( Logical Operator )

---

- 주어진 논리식을 판단하여, 참(true) or 거짓(false) 를 리턴
    - && : 모두 true 일 경우 true 를 리턴 ( 논리 AND 연산 )
    - || : 하나라도 true 일 경우 true 를 리턴 ( 논리 OR 연산 )
    - ! : 결과가 true 이면 false, false 이면 ture 를 리턴 (논리 NOT 연산)
    
```jsx
const i = true;
const x = false;

console.log(i && i) // true
console.log(i && x) // false

console.log(i || i) // true
console.log(i || x) // true
console.log(x || x) // false

console.log(!i) // false
console.log(!x) // true
```