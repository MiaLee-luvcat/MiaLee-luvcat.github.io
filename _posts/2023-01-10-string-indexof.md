---
published: true
title:  "[JavaScript] String.prototype.indexOf()에 대한 고찰"
excerpt: ""

categories:
  - JavaScript
tags:
  - [JavaScript, String, indexOf]

toc: true
toc_sticky: true
 
date: 2023-01-10 23:43:00
last_modified_at: 2023-01-10 23:43:00
---

## indexOf가 뭘까?
JavaScript에서 `String`(문자열) 타입을 다루다 보면 '자르기'를 위해 `slice`를 쓰게 되는 경우가 종종 있을 것이다.  
그런데 `slice`는 어디서부터 어디까지 끊겠다는 절대적 위치로 끊는 거다 보니 여러 데이터를 반복적으로 처리할 땐 규칙이 있다는 전제하에 사용할 수 있다.  
그렇다면 이런 경우엔 어떡해야 할까?  

> `A`와 `B`가 순서대로 포함된, 그러나 어느 위치에 들어갈지는 랜덤인 `String` 타입 데이터 100개를 처리해야 하는데 A 앞에서 한 번 끊고 B 뒤에서 한 번 끊어야 한다.  

위 상황에서 입력 데이터는 대략 이런 느낌이라고 생각하면 된다.  
* `123AcdB1g`
* `1A23Bd`
* `12345ABssss`

이런 상황에서 A가 몇 번째 위치인지, B가 몇 번째 위치인지 모두 `for`문에 `if`문까지 쓰며 훑는 걸 생각할 수도 있지만, `indexOf`를 사용하는 방법도 있다.  

[MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/indexOf){:target="_blank"}에서는 간단하게 이런 예시들이 있다.  

```js
const paragraph = 'The quick brown fox jumps over the lazy dog. If the dog barked, was it really lazy?';

const searchTerm = 'dog';
const indexOfFirst = paragraph.indexOf(searchTerm);

console.log(`The index of the first "${searchTerm}" from the beginning is ${indexOfFirst}`);
// expected output: "The index of the first "dog" from the beginning is 40"

console.log(`The index of the 2nd "${searchTerm}" is ${paragraph.indexOf(searchTerm, (indexOfFirst + 1))}`);
// expected output: "The index of the 2nd "dog" is 52"
```

<br>

한마디로 하자면 `indexOf`는 특정 문자열의 위치를 알려주는 아주 유용한 메소드다.  
단, 찾으려는 동일한 문자열이 두 곳 이상에 있다고 해도 첫 번째로 발견된 위치만 알려준다.  
그래서 특정 번째의 위치를 알고 싶다면 두 번째 인자를 이용하면 된다.  
자세한 내용은 아래의 구문을 보자.  

## 구문  
> `str.indexOf(searchValue[, fromIndex])`

### 매개변수  
**`searchValue`**  
찾고자 하는 값을 넣는다. 문자열에서 찾는 것이므로 마찬가지로 `String` 형태여야 한다.  

<br>

**`fromIndex` (Optional)**  
어디서부터 찾을지 정한다.  
이는 `Number`형태이면서 0 혹은 자연수여야 의미가 있으며, 음수나 유리, 혹은 다른 타입의 값이 들어가도 특별히 오류가 나지는 않는다.  
의미 없는 값 ex) `-1`, `'string'`, `0.5` ...  

<br>

### 반환 값  
fronIndex(default = 0)부터 처음으로 발견한 위치 인덱스(=숫자)를 리턴한다.  
없으면 `-1`을 리턴한다.  


### 추가 예제(MDN)  

```js
'Blue Whale'.indexOf('Blue');     // returns  0
'Blue Whale'.indexOf('Blute');    // returns -1
'Blue Whale'.indexOf('Whale', 0); // returns  5
'Blue Whale'.indexOf('Whale', 5); // returns  5
'Blue Whale'.indexOf('Whale', 7); // returns -1
'Blue Whale'.indexOf('');         // returns  0
'Blue Whale'.indexOf('', 9);      // returns  9
'Blue Whale'.indexOf('', 10);     // returns 10
'Blue Whale'.indexOf('', 11);     // returns 10
```
 
<br> 

### 참고 사항  
* 대소문자를 구별한다.  
  * `'Blue Whale'.indexOf('blue'); // returns -1`  

<br>

### if? test
* 만약 빈 문자열(`''`)을 사용하면 어떻게 될까?  
  * `''.indexOf()`에서 문제없이 작동하며 빈 문자열을 찾는다 했을 때 `0`을 리턴한다.  
  * `'string'.indexOf('')`에서도 문제없이 작동하며 `0`을 리턴한다.  
* 만약 undefined로 사용하면 어떻게 될까?  
  * `undefined.indexOf()`는 당연히 타입 에러가 뜬다.  
  * `'string'.indexOf(undefined)`는 작동하며 `-1`을 리턴한다.  


## 기타 - 한마디  
개발자로 취업하고 스트링 데이터를 가공할 일이 생겼는데 이 메소드를 제대로 다룬 건 그때가 처음이었다.  
그래서 블로깅할 메모 목록에 이것이 있었고, 그래서 이 글을 쓰게 됐다. :D  

<br>
<br>