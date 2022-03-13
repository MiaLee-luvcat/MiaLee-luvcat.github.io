---
published: true
title:  "[JavaScript] Greedy : 짐 나르기"
excerpt: ""

categories:
  - Algorithm
tags:
  - [Couplet, Algorithm, JavaScript, Greedy]

toc: true
toc_sticky: true
 
date: 2022-03-13 20:11:30
last_modified_at: 2022-03-13 20:11:30
---

# 문제  
김코딩과 박해커는 사무실 이사를 위해 짐을 미리 싸 둔 뒤, 짐을 넣을 박스를 사왔다. 박스를 사오고 보니 각 이사짐의 무게는 들쭉날쭉한 반면, 박스는 너무 작아서 한번에 최대 2개의 짐 밖에 넣을 수 없었고 무게 제한도 있었다.  

예를 들어, 짐의 무게가 `[70kg, 50kg, 80kg, 50kg]`이고 박스의 무게 제한이 100kg이라면 2번째 짐과 4번째 짐은 같이 넣을 수 있지만 1번째 짐과 3번째 짐의 무게의 합은 150kg이므로 박스의 무게 제한을 초과하여 같이 넣을 수 없다.  

박스를 최대한 적게 사용하여 모든 짐을 옮기려고 합니다.  

짐의 무게를 담은 배열 stuff와 박스의 무게 제한 limit가 매개변수로 주어질 때, 모든 짐을 옮기기 위해 필요한 박스 개수의 최소값을 return 하도록 movingStuff 함수를 작성하세요.  




## 입력
### 인자 1: stuff  
* `Number` 타입의 40 이상 240 이하의 자연수를 담은 배열  
  * ex) `[70, 50, 80, 50]`  

### 인자 2: limited
*`Number` 타입의 40 이상 240 이하의 자연수  

## 출력  
* `Number` 타입을 리턴해야 합니다.  
* 모든 짐을 옮기기 위해 필요한 박스 개수의 최솟값을 숫자로 반환합니다.  

## 주의사항  
* 옮겨야 할 짐의 개수는 1개 이상 50,000개 이하입니다.
* 박스의 무게 제한은 항상 짐의 무게 중 최대값보다 크게 주어지므로 짐을 나르지 못하는 경우는 없습니다.

## 입출력 예시  
```js
let output = movingStuff([70, 50, 80, 50], 100);
console.log(output); // 3

let output = movingStuff([60, 80, 120, 90, 130], 140);
console.log(output); // 4
```
<br>

# 풀이  
## 로직  
작성 중  



<br>

## 해답 코드
```js
function movingStuff(stuff, limit) {
  // TODO: 여기에 코드를 작성합니다.
  let temp = stuff.slice(); // 짐 배열 복사
  temp.sort((a,b) => a-b); // 작은 것부터 큰 순으로 정렬
  let count=0; // 박수 개수

  while(temp.length !== 0){ // 짐을 쓴 건 없앨 예정이라 이렇게 조건을 줌
    if(temp[temp.length-1] + temp[0] > limit && temp.length > 1){
      // 가장 무거운 것과 가장 가벼운 것의 합이 한계를 초과하면서 짐이 2개 이상일 경우
      // 가장 무거운 건 그 무엇과도 조합할 수 없으니 먼저 뺀다.
      count++;
      temp.pop();
    }
    else if(temp[temp.length-1] + temp[0] <= limit && temp.length > 1) {
      // 가장 무거운 것과 가장 가벼운 것의 합이 한계를 넘지 않으면서 2개가 맞을 경우
      // 둘을 각각 빼고 카운트한다
      count++;
      temp.pop();
      temp.shift();
    }
    else{
      // 그 외엔 1개뿐이니까 걍 뺀다
      count++;
      temp.pop();
    }
  }

  return count;
}
```

## 기타 - 한마디  
 작성 중  

<br>
<br>