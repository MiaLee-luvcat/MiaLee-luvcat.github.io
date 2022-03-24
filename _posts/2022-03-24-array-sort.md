---
published: true
title:  "[JavaScript] Array.prototype.sort()에 대한 고찰"
excerpt: ""

categories:
  - TIL
tags:
  - [TIL, sort, JavaScript, 고차함수, higher-order function]

toc: true
toc_sticky: true
 
date: 2022-03-24 14:28:00
last_modified_at: 2022-03-24 14:28:00
---

# sort란 뭘까?
단순히 영어 단어 sort의 뜻을 찾아보면 '분류하다', '구분하다', '(문제 등을) 정리(해결)하다'를 볼 수 있을 것이다.  
이 의미를 그대로 컴퓨터 프로그래밍에 접하면 어떤 기능을 가진 메소드일지 예상이 가능할 것이다.  
JavaScript에서의 sort 메서드는 보통 Array.prototype.sort()로 통용되며 말 그대로 배열 전용 메서드로 쓰인다.  
sort를 언제 어떻게 쓰냐에 대해서 아주 간단한 예시를 들면,  
`['a','b','c']` 순서여야 할 배열이 `['a','c','b']`로 되어 있다면 `['a','c','b'].sort()`를 썼을 때 `['a','b','c']`로 된다는 것을 들 수 있다.  
영어 단어 뜻 그대로 '분류, 정리하다'이다.  

## sort를 접한 과거  
나는 이 sort 함수를 처음 접한 게 대략 2021년 8월 10일로, **고차함수**를 처음 배웠을 때 지나가듯 접했었다.  
당시 실제 코플릿을 풀 때 쓰인 건 `filter`, `map`, `reduce`여서, '그 외의 Array 내장 고차함수들은 TIL로 생각해 봐라'라는 말에 다음에 해 봐야지 하고 넘어가 버렸었다... ^^;  
그래서! 막상 자주 쓰이는 함수이다 보니 이김에 제대로 고찰해 보기로 했다!  

[참고 문서 MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/sort){:target="_blank"}  

## Array.prototype.sort()  
`sort()` 메서드는 배열의 요소를 적절한 위치에 정렬한 후 그 배열을 반환한다.  
특별하게 정렬 기준을 정하지 않았을 때, 반환되는 정렬은 stable(안정적인) sort가 아닐 수 있다.  
기본 정렬 순서는 문자열의 유니코드 코드 포인트를 따른다.  
정렬 속도와 복잡도는 각 구현방식에 따라 다를 수 있습니다.  

**예시 - mdn.ver**  
<iframe class="interactive is-js-height" style="width: 100%;" height="450" src="https://interactive-examples.mdn.mozilla.net/pages/js/array-sort.html" title="MDN Web Docs Interactive Example" loading="lazy"></iframe>
<br>

**예시 - 작성자.ver**
<iframe height="300" style="width: 100%;" scrolling="no" title="arr.sort();" src="https://codepen.io/siri-syl/embed/LYexpNV?default-tab=js%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/siri-syl/pen/LYexpNV">
  arr.sort();</a> by siri-syl (<a href="https://codepen.io/siri-syl">@siri-syl</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>
<br>

## 구문  
> arr.sort([compareFunction])  

### 매개변수  
`compareFunction` (Optional)  
정렬 순서를 정의하는 함수. 생략하면 배열은 각 요소의 문자열 변환에 따라 각 문자의 유니 코드 코드 포인트 값에 따라 정렬된다.  
옵셔널 변수인만큼 아까 위의 예시처럼 비워둬도 된다.  
<br>

### 반환 값  
정렬한 배열. **원 배열이 정렬되는 것에 유의.(중요)** 복사본이 만들어지는 것이 아니다.  
그래서 위 예시에서도 확인할 수 있듯이 그 원배열을 다시 불러들였는데도 정렬된 배열이 나옴을 볼 수 있다.  
만약 원 배열을 건드리고 싶지 않다면 스프레드나 slice 등으로 복사하고 쓰는 게 좋다.(=깊은 복사!)  

### compareFunction  
그렇다면 `compareFunction`은 어떻게 써야 할까? 바로 쓰기 전에 알아둬야 할 점이 있다.  
보통 요소를 a, b로 나누고 시작하는데, a가 특정 요소, b가 a를 제외한 요소이다.  
둘을 `compareFunction`에 맞춰 비교한 뒤 정렬하는 거라고 생각하면 된다.  
예시를 바로 보여주겠다.  

```js
function compare(a, b) {
  if (a is less than b by some ordering criterion) {
    return -1;
  }
  if (a is greater than b by the ordering criterion) {
    return 1;
  }
  // a must be equal to b
  return 0;
}
```
결론적으로 반환(return)값이 -(음수)일 경우 a가 앞,  
반환값이 +(양수)일 경우 b가 앞,  
반환값이 0일 경우 변화 없음.  
으로 정렬된다고 생각하면 된다.  

그래서 아래에 오름차순으로 정렬한다면 어떻게 될까에 대해 예시를 뒀다.  
<br> 

**숫자 오름차순 정렬**
<iframe height="300" style="width: 100%;" scrolling="no" title="arr.sort오름차순" src="https://codepen.io/siri-syl/embed/YzYNWaZ?default-tab=js%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/siri-syl/pen/YzYNWaZ">
  arr.sort오름차순</a> by siri-syl (<a href="https://codepen.io/siri-syl">@siri-syl</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>
<br>

위에 맞춰 만약 내림차순을 원한다면 `compareFunction`를 `b - a`로 하면 된다.  


### 객체 요소 정렬  
배열의 요소로 객체가 넣어지는 경우가 있음을 알 것이다.  
이 객체들을 정렬할 수도 있다...!  
바로 예시를 보자.  

```js
var items = [
  { name: 'Edward', value: 21 },
  { name: 'Sharpe', value: 37 },
  { name: 'And', value: 45 },
  { name: 'The', value: -12 },
  { name: 'Magnetic', value: 13 },
  { name: 'Zeros', value: 37 }
];

// value 기준으로 정렬
items.sort(function (a, b) {
  if (a.value > b.value) {
    return 1;
  }
  if (a.value < b.value) {
    return -1;
  }
  // a must be equal to b
  return 0;
});

// name 기준으로 정렬
items.sort(function(a, b) {
  var nameA = a.name.toUpperCase(); // ignore upper and lowercase
  var nameB = b.name.toUpperCase(); // ignore upper and lowercase
  if (nameA < nameB) {
    return -1;
  }
  if (nameA > nameB) {
    return 1;
  }

  // 이름이 같을 경우
  return 0;
});
```  
<br>  

## map을 이용한 정렬  
sort는 만능 정렬법이 아니다.  
특히 나처럼 코드스테이츠 같은 테스트를 위한 코드문제를 자주 접하는 과정을 겪은 사람들은 sort를 썼다가 시간초과를 자주 겪을 것이다.  
sort에도 수많은 방법이 있고, 알고리즘 문제로도 자주 나오는데 이건 추후 얘기하기로 하고...  
당장 새로운 알고리즘을 공부하고 사용하기 힘들 경우엔 아래의 방법을 응용해보자.  

아무튼 `compareFunction`은 배열 내의 요소마다 여러 번 호출될 수 있고, 그렇기 때문에 높은 오버헤드가 발생할 수도 있다.  
`compareFunction`이 복잡해지고, 정렬할 요소가 많아질 경우 `map`을 사용한 정렬을 고려해 보는 것이 좋다.  
이 방법은 임시 배열을 하나 만들어서 여기에 실제 정렬에 사용할 값만을 뽑아서 넣어서 이를 정렬하고, 그 결과를 이용해서 실제 정렬을 한다.  

```js
// 소트 할 배열
var list = ['Delta', 'alpha', 'CHARLIE', 'bravo'];

// 임시 배열은 위치 및 정렬 값이있는 객체를 보유
var mapped = list.map(function(el, i) {
  return { index: i, value: el.toLowerCase() };
})

// 축소 치를 포함한 매핑 된 배열의 소트
mapped.sort(function(a, b) {
  return +(a.value > b.value) || +(a.value === b.value) - 1;
});

// 결과 순서를 위한 컨테이너
var result = mapped.map(function(el){
  return list[el.index];
});
```  
<br>

## 기타 - 한마디  
다음엔 sort에 대한 여러 알고리즘 문제를 풀어봐야겠다 :D

<br>
<br>