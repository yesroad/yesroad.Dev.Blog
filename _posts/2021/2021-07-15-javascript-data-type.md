---
title: "Javascript - 데이터 타입(Data Type)"
date: 2021-07-15
tags:
  - javscript
keywords:
  - javscript
  - data
  - number
  - string
  - boolean
  - null
  - undefined
  - symbol
  - object
  - array
  - typeof
  - NaN
---

### DataType
---
> 데이터 타입이란 프로그래밍 언어에서 사용할 수 있는 데이터 (숫자, 문자열, 불리언 등)의 종류를 말한다.

1. **원시타입 (Primitive value)**
    - number
    - string
    - boolean
    - undefined
    - null
    - symbol (es6 추가 스펙)
2. **객체 타입 (object / reference type)**
    - Array
    - Object
    - Function
    - ...
    

### Number

---

> 우리가 일반적으로 알고 있는 숫자와 동일하며, 덧셈(+) , 뺄셈(-), 곱셈(*), 나눗셈(/) 등의 연산을 할 수 있다.
    
```jsx
// 숫자(number)
const num = 1 
const num02 = 1.2
```
    

- **문자열을 숫자로 변경하는 방법도 존재한다**
    - parseInt (정수 변환)
    
```jsx
// parseInt ( 문자 -> 숫자 (정수) 변환 )
console.log(parseInt('12')) // 12
console.log(parseInt('3.14')) // 3
console.log(parseInt('3.14 문자')) // 3
console.log(parseInt('문자 3.14')) // NaN ( 문자열이 앞에 있으면 NaN )
```
    
- parseFloat (소수 변환)
    
```jsx
// parseFloat ( 문자 -> 숫자 (소수) 변환 )
console.log(parseFloat('12')) // 12
console.log(parseFloat('3.14')) // 3.14
console.log(parseFloat('3.14 문자')) // 3.14
console.log(parseFloat('문자 3.14')) // NaN ( 문자열이 앞에 있으면 NaN )
```
    

### String

---

> '' 혹은 "" 를 사용하여 내용을 감싸서 문자열로 표시한다.
    
```jsx
// 문자(string)
const string = '2' 
const string02 = "문자"
```
    

### Boolean

---

> 논리적인 요소를 나타내며 true / false 를 반환한다.
    
```jsx
// 논리 true or false (boolean)
const boolean = true; 
const boolean02 = false;
```
    

### null

---

> 존재하지 않는 값을 나타낸다
    
```jsx
// 존재하지않음(null)
const Null = null; 
```
    

### undefined

---

> 값이 할당되지 않았을 경우를 나타낸다
    
```jsx
// 비어있는값(undefined)
const Undefined = undefined;
```
    

### Symbol

---

> 심볼은 ES6에서 새롭게 추가된 타입이다. 심볼은 주로 이름의 충돌 위험이 없는 유일한 객체의 프로퍼티 키를 만들기 위해 사용한다.
    
```jsx
// es6 부터 사용
const symbol = Symbol(); 
```
    

### Object

---

> 자바스크립트의 객체(object)는 키(key)과 값(value)으로 구성된 프로퍼티(Property)들의 집합이다.
    
```jsx
// 객체(object)
const object = {firstName: 'first, lastName: 'last'} 
```
    

### Array

---

> 배열은 [ ]로 감싸서 나타내며, 배열 안에는 무엇이든지(배열, 함수, 객체 등) 들어갈 수 있다.
    
```jsx
// 배열(array)
const array = [1, 'second', {}, [], function(){}]
```
    

### typeOf

---

> javascript 데이터 타입을 찾기 위한 함수
    
```jsx
console.log(typeof 1) // number
console.log(typeof 'strong') // string
console.log(typeof []) // object(array) 베열도 객체로 본다.
console.log(typeof {}) // object
console.log(typeof true) // boolean
console.log(typeof null) // object(null) 존재하지않는 null 값도 javascript 에서는 객체로 본다.
console.log(typeof undefined) // undefined
```
    

### undefined 와 null

---

> 기존값들을 undefined 및 null 을 사용하여 비어있는 값으로 만들 수 있다.
    
```jsx
console.log(typeof undefined) // undefined
console.log(typeof null) // object
console.log(null === undefined) // false
console.log(null == undefined) // true
```
    

### NaN ( Not a Number )

---

> NaN 은 잘못된 입력으로 인해 계산을 할 수 없음을 나타내는 기호이다.

```jsx
console.log(NaN == undefined); // false
console.log(NaN == null); // false
console.log(undefined == null); // true
console.log(NaN === NaN); // false
console.log(NaN !== NaN); // true
console.log(isNaN(NaN)) // true ( 전달된 값이 NaN 인지 아닌지 검사 );
```