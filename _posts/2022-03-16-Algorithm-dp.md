---
published: true
title:  "[JavaScript] DP : 짐 나르기"
excerpt: ""

categories:
  - Algorithm
tags:
  - [Couplet, Algorithm, JavaScript, DP]

toc: true
toc_sticky: true
 
date: 2022-03-16 16:00:30
last_modified_at: 2022-03-16 16:00:30
---

# 문제  
자신이 감옥에 간 사이 연인이었던 줄리아를 앤디에게 빼앗겨 화가 난 조지는 브레드, 맷과 함께 앤디 소유의 카지노 지하에 있는 금고를 털기로 합니다. 온갖 트랩을 뚫고 드디어 금고에 진입한 조지와 일행들. 조지는 이와중에 감옥에서 틈틈이 공부한 알고리즘을 이용해 target 금액을 훔칠 수 있는 방법의 경우의 수를 계산하기 시작합니다.  

예를 들어 $50 을 훔칠 때 $10, $20, $50 이 있다면 다음과 같이 4 가지 방법으로 $50을 훔칠 수 있습니다.  

* $50 한 장을 훔친다  
* $20 두 장, $10 한 장을 훔친다  
* $20 한 장, $10 세 장을 훔친다  
* $10 다섯 장을 훔친다  

훔치고 싶은 target 금액과 금고에 있는 돈의 종류 type 을 입력받아, 조지가 target 을 훔칠 수 있는 방법의 수를 리턴하세요.  

## 입력  
### 인자 1: target  
* `Number` 타입의 100,000 이하의 자연수  

### 인자 2: type  
* `Number` 타입을 요소로 갖는 100 이하의 자연수를 담은 배열  

## 출력  
* `Number` 타입을 리턴해야 합니다.  
* 조지가 target을 훔칠 수 있는 방법의 수를 숫자로 반환합니다.  

## 주의사항  
* 모든 화폐는 무한하게 있다고 가정합니다.  

## 입출력 예시  
```js
let output = ocean(50, [10, 20, 50]);
console.log(output); // 4

let output = ocean(100, [10, 20, 50]);
console.log(output); // 10

let output = ocean(30, [5, 6, 7]);
console.log(output); // 4
```
<br>

## Hint!  
해당 문제는 `동전 교환 알고리즘 (Coin Change)`을 활용하여 풀 수 있습니다.  
검색해 보시고, 연구해 보세요!  


# 풀이  
힌트에 나온 `동전 교환 알고리즘 (Coin Change)`은 이미 내가 최근에 풀어봤던 문제의 해결과정 및 답을 말한다.  
[풀었던 글 링크](https://siri-syl.github.io/algorithm/Algorithm-Greedy/)  
여기서 간단히 말하자면, 원하는 금액에 맞게 일정 종류의 동전들을 이용해서 주되, 그 동전의 개수를 최소화하는 방법을 뜻한다.  



## 로직
### siri(작성자).ver  


<br>

### 기술 코드  
위에서 말한 `동전 교환 알고리즘 (Coin Change)`을 토대로 그 파트 코드를 미리 알아두고 가면 좋다.  

```js
// 위에서 말한 글에서 푼 답을 가져왔습니다.
function partTimeJob(k) {
  // k=거스름돈

  let stack = [500, 100, 50, 10, 5, 1];
  let count = 0;
  let k2= k;

  for(let i=0; i<stack.length; i++){
    let temp = parseInt(k2/stack[i]);
    count += temp;
    k2 = k2 % stack[i];
  }

  return count;
}
```

<br>

## 해답 코드  

```js
function ocean(target, type) {
  // 거스름돈 1원, 2원, 3원 등등에 대한 경우의 수를 구한 뒤
  // 큰 거스름돈에 대해 구한다.
  
  let bag = [1];

  for(let i = 1; i <= target; i++) 
    bag[i] = 0;

  for(let i = 0; i < type.length; i++) {
    for(let j = 1; j <= target; j++)
      if(type[i] <= j)
        bag[j] += bag[j-type[i]];
  }
  return bag[target];
}
```  
<br>

## 기타 - 한마디  
개인적으로 Greedy 알고리즘의 심화문제라고 생각한다. 실제로 코드스테이츠 코플릿 리스트에서도 Advanced라고 적혀 있었으니 맞는 듯하다.  

<br>
<br>