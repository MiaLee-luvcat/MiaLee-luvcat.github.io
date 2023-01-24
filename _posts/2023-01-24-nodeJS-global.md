---
published: true
title:  "[Node.js] module이 아닌 전역 변수로 활용하는 법 = global variable"  
excerpt: ""

categories:
  - JavaScript
tags:
  - [JavaScript, Node.js, global variable]

toc: true
toc_sticky: true
 
date: 2023-01-24 21:36:00
last_modified_at: 2023-01-24 21:36:00
---

## 여기서도 저기서도 쓰이는 변수? 전역 변수를 활용하자  
Node.js에서 여러 데이터를 다루다 보면 특정 변수를 다른 곳에서도 사용하고 싶을 때가 있을 것이다.  
처음엔 `module.exports`로 이곳저곳으로 함수 등을 빼서 사용했겠지만, 너무 잦은 사용임과 동시에 단순 변수일 경우 이 기능조차 애매모호하다.  
그럴 때 사용할 수 있는 방법이 Node.js에서 활용되는 global variable, 즉 글로벌 변수(=전역 변수)다.  

> 전역 변수는 어떤 변수 영역 내에서도 접근할 수 있는 변수를 의미하는 전산학 용어이다. -위키백과-  

<br>

### 사용법  

```js
// index.js
let a = 1
global.a = a
global.b = a

// app.js
// a, b 선언 없음
console.log(a) // 1
console.log(b) // 1
a = 2 // 새로운 할당도 됨. 다른 곳에서 a를 불러오면 2로 불러와짐.
```  

<br>

### 주의사항  
이 global 선언은 자주 쓰면 안 된다. 마구 남발하며 사용했다간 어떤 변수를 이용했는지 헷갈릴 수 있어서 `var` 선언과 비슷한 문제가 발생될 가능성이 있다.  
사용한다 해도 한 곳에서 선언 및 초기화를 정리해 두는 것이 좋고, 까먹고 또 중복사용될 만한 변수로 선언해서는 안 된다.  
예시로 나는 global 선언을 하는 변수명 앞부분에 반드시 `global`을 붙이곤 했다.  
* globalA
* globalTime
* globalUserName

<br>

## 기타 - 한마디  
이 방법 말고도 node-cache 라이브러리 같은 것을 이용해도 괜찮지만, 소수의 변수를 설정한다는 전제하에선 이런 방법도 꽤 유용하다.  

<br>

## 참고 문서  
[전역변수 위키백과](https://ko.wikipedia.org/wiki/%EC%A0%84%EC%97%AD_%EB%B3%80%EC%88%98){:target="_blank"}  

<br>
<br>