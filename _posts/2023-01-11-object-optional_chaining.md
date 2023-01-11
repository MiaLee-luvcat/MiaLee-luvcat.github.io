---
published: true
title:  "[JavaScript] Object Optional chaining(?.) 객체 물음표 문법을 활용해라"  
excerpt: ""

categories:
  - JavaScript
tags:
  - [JavaScript, Object, Optional chaining]

toc: true
toc_sticky: true
 
date: 2023-01-11 23:50:00
last_modified_at: 2023-01-11 23:50:00
---

## Object의 Key나 Value 불러오다가 에러나면...  
JavaScript를 다루다 보면 Object(객체) 관련한 처리에서 에러를 자주 겪게 된다.  
나만 해도 JavaScript 자체를 3년 이상 쓰면서 객체 관련해서 이 오류를 제일 많이 겪었던 것 같다.  

> `Uncaught TypeError: Cannot read properties of undefined`  

바로 타입에러...!  

당연히 올바른 객체가 나올 줄 알고 함수를 다 짜놨더니 잘못돼서 에러가 나는 것이다...  
예시로는 아래 같은 상황들이다.  

<br>


```js
const func = () => {
  const obj = {}
  console.log(obj.user) // A

  return obj.user.name //B
}

func()
// A: console >> 'undefined'
// B: Error
```  
<br>

## 물음표를 적극 활용하자!  

[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining){:target="_blank"} 글을 우선 봐도 된다.  

물음표? 라고 하니 뭔가 싶겠지만, 정확한 네이밍은 `Optional chaining`이라고 한다.  
특정 키, 값을 객체로부터 가져오기 위해 마침표(.)를 쓸 것이다.  
그 앞에 물음표(?)를 붙이면, 실제로 불러올 수 없는 상황이더라도 식 자체는 돌아가게 해준다.  
아무것도 없는 곳에서 물건을 찾는다고 하면 에러를 내뱉던 걸 '없어요'라고 알려주는 친절한 거라고 생각하면 편하다.  

다만 존재하지 않는 곳에 찍은 거라면 리턴값은 `undefined`가 나올 것을 염두에 두어야 한다.  
또한 뭐가 잘못된지도 모르고 넘어가게 되는 경우도 있으므로 무분별한 사용도 자제해야 한다.  

그래도 다루게 될 객체가 너무나도 유연하다면, 혹은 테스트로 다루는 거라면 이 문법을 적극 활용하자.  

<br>

```js
const func = () => {
  const obj = {}
  console.log(obj.user) // A

  return obj.user?.name //B
}

func()
// A: console >> 'undefined'
// B: console >> 'undefined'
```  
<br>


## 기타 - 한마디  
이 문법을 쓰지 않더라도 충분히 에러처리를 할 수는 있지만, 코드를 한 줄이라도 줄이기 위해 쓰는 것 정도는 괜찮다고 본다.  

<br>
<br>