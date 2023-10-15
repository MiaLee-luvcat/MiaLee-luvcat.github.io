---
published: true
title:  "[JavaScript] 재귀함수 - fibonacci"
excerpt: ""

categories:
  - Algorithm
tags:
  - [Couplet, Algorithm, JavaScript, 재귀함수, Recursion, fibonacci]

toc: true
toc_sticky: true
 
date: 2022-03-20 23:32:30
last_modified_at: 2022-03-20 23:32:30
---

# 문제  
수(`num`)를 입력받아 피보나치 수열의 `num`번째 요소를 리턴해야 합니다.  

0번째 피보나치 수는 0이고, 1번째 피보나치 수는 1입니다. 그 다음 2번째 피보나치 수부터는 바로 직전의 두 피보나치 수의 합으로 정의합니다.  
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, ...  


## 입력
### 인자 1 : num
* `number` 타입의 num (num은 0 이상 15 이하의 정수)  

## 출력  
* `number` 타입을 리턴해야 합니다. (num 번째 피보나치 수)  

## 주의 사항  
* 함수 **`fibonacci`**는 재귀함수의 형태로 작성합니다.  
* 반복문(`for`, `while`) 사용은 금지됩니다.  
* 피보나치 수열은 0번부터 시작합니다.  

## 입출력 예시  
```js
let output = fibonacci(5);
console.log(output); // --> 5

output = fibonacci(9);
console.log(output); // --> 34
```
<br>

# 풀이  
## 로직  

이 문제는 주의사항에 적힌 대로 `for`, `while`을 쓸 수 없으며 재귀함수를 이용하여 풀게 된다.  
재귀함수 내용은 [이 글](https://mialee-luvcat.github.io/til/til-recursion/){:target="_blank"}에서 확인할 수 있다!  

우선 문제를 최대한 쪼개고 쪼개서 가장 간단한 계산식에 이르게 한다.  
여기서는 피보나치 수열이 0, 1, 1, 2, ... 이기에 세 번째 수가 오려면 첫 번째와 두 번째 수를 더하고,  
네 번째 수가 오려면 두 번째와 세 번째 수를 더해야 한다.  
즉 (n - 2) + (n - 1) 이 된다.  

또한 위 계산식을 풀려면 최소 첫 번째 수와 두 번째 수를 알아야 하는데, 이미 0과 1임을 안다.  

그렇기에 아래와 같이 풀 수 있다.  

<br>

## 해답 코드
```js
function fibonacci(num) {
  // 별도의 최적화 기법(memoization)은 금지됩니다.

  if(num===0) return 0;
  if(num===1) return 1;

  return fibonacci(num - 2) + fibonacci(num - 1);
}
```

## 기타 - 한마디  
이 문제는 매우 쉽지만 다음에 다른 방법으로 풀 예정이기에 정리해 봤다.  
또한 재귀함수 자체도 한번 글을 쓰고자 한다.  

<br>
<br>