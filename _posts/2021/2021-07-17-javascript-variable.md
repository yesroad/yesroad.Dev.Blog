---
title: "Javascript - 변수(variable)"
date: 2021-07-17
tags:
  - javascript
keywords:
  - javascript
  - variable
  - var
  - let
  - const
---

### Variable

---


> 변수란 데이터를 저장 혹은 읽고 쓰기 위하여 저장하는 보관함을 뜻한다 <br/>
> 변수는 선언 단계 > 초기화 단계 > 할당 단계 에 걸쳐서 생성된다.

- 변수의 종류
    - var
    - let
    - const

### var의 위험성

---

> 💡 **var** 는 설계상 오류에 주의를 기울이지 않으면 심각한 문제가 발생할 수 있다.

- 함수 레벨 스코프
    - 전역 변수의 남발로 인하여 for 문 등의 초기화 식에서 사용한 변수를 외부 또는 전역에서 참조 할 수 있게된다.
- var 키워드 생략 허용
    - 의도하지 않은 변수의 전역화가 발생할 수 있다.
- 중복 선언 허용
    - var 은 재선언이 가능하므로, 의도하지 않게 변수값을 변경하여 에러를 발생 시킬 수 있다.
- 호이스팅
    - 호이스팅으로 인하여 변수를 선언하기 전에 참조가 가능하다.

### var

---

- `var` 는 호이스팅이 일어나며, 재선언 및 재할당이 가능하다.
- `var` 는 함수 스코프(Function scope) 를 따른다.

```jsx
var testVar = 1;
console.log(testVar); // 1

var testVar = 5;
console.log(testVar); // 5

var testVar = 10;
console.log(testVar); // 10
```

### let

---

- `let` 은 재할당은 가능하지만 재선언은 할 수 없다.
- `let` 은 블록 스코프(Block scope) 를 따른다.

```jsx
let testLet = '1' 
console.log(testLet) // testLet 1 선언

let testLet = '5'  // error ( 변수 'testConst'은 이미 선언 됨 )
console.log(testLet) // testLet 1 호출

testLet = '10' // 10으로 재할당 가능
console.log(testLet) // 10
```

### const

---

- `const` 는 재선언 및 재할당이 불가능하다.
- 변하지 않는 값을 뜻하는 `상수`를 생각하면 된다.
- `const` 는 블록 스코프(Block scope) 를 따른다.

```jsx
const testConst = '2'
console.log(testConst) // 2

const testConst = '4' // error ( 변수 'testConst'은 이미 선언 됨 )
console.log(testConst) 

testConst = '8'    
console.log(testConst) // error ( 상수(const) 에 재할당 불가 )
```