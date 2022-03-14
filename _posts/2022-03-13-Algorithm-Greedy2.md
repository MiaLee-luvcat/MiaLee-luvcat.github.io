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
다가가는 방식에 따라 풀이 코드가 다 다를 것이라 예상된다. 이미 내가 푼 답과 코드스테이츠에서 준 레퍼런스의 코드의 성격이 좀 다르기도 했다.  

## 로직
### siri(작성자).ver  
나는 가장 무거운 것과 가장 가벼운 것을 먼저 한 박스에 담는다는 가정을 해 보았다.  
이 문제의 주제가 Greedy인만큼, 가장 적합하면서 효율적인 방법을 생각해야 한다. 그렇기에 가장 가벼운 짐을 어중간한 무게의 짐과 합쳐서 상자에 넣을 게 아니라, 최대한 두 개씩은 다 들어가게끔 하기 위해 가장 무거운 것과 가벼운 것을 먼저 대조시킨 것이다.  
상자 안에 여러 개의 짐을 넣을 수 있다면 상황은 달라지지만, **한 상자에 짐 2개씩**만 넣는다는 편한 조건으로 인해 이렇게 풀 수 있었다.  

1. 입력받은 stuff 배열값을 오름차순으로 sort한다.  
2. stuff의 length가 0이 될 때까지 while문을 돌린다.(조건 : stuff.length != 0)
3. 만약 가장 무거운 것(sutff[stuff.length-1])과 가벼운 것(sutff[0])을 합쳤을 때 limit 값보다 높다면, 무거운 것은 다른 어떠한 짐과도 같이 넣을 수 없다는 것을 알 수 있다. 단 이 조건은 sutff.length 값이 1보다 크다는 것 또한 and문으로 작성해야 한다.  
4. 이 경우 무거운 것을 하나의 상자에 넣는다 하고 상자 개수를 카운트 +1, 그리고 해당 짐은 stuff 배열에서 제외시킨다.(pop을 사용)(처음 count 변수를 선언/할당할 땐 0)  
5. 만약 3번 전자 상황에서 limit 값보다 작거나 같다면, 상자 개수를 카운트 +1, 각 짐들은 sutff 배열에서 제외시킨다.(pop, shift 사용) 이 또한 stff.length 값이 1보다 크다는 것을 and문으로 작성해야 한다.  
6. 만약 sutff.length = 1일 경우 상주 개수를 카운트 +1, 짐은 sutff 배열에서 제외시킨다.(pop or shift 사용)  

<br>

### reference.ver  
레퍼런스 버전에서 다가간 방법은 stuff 배열 자체 값을 수정하기보다는 index 값을 이용하는 방식을 이용했다. 또한 그냥 상자 수를 카운트하기보다는 2개가 들어간 상자 개수만 세서 기본 짐 개수에서 빼는 방식임이 내 방법과 꽤나 달랐다.  
그래서 오름차순으로 sort하는 것까지는 같지만, 가장 가벼운 짐과 무거운 짐 index값을 복사하며 while문 조건이 가벼운 짐 index가 무거운 짐 index보다 작다면 계속 반복시키게 했다.  

1. 입력받은 stuff 배열값을 오름차순으로 sort한다.  
2. index 0 값과 index stuff.length-1 값을 각 변수에 할당시킨다. (leftIdx, rightIdx)  
3. leftIdx 값이 rightIdx 갑보다 크거나 같을 때까지 while문을 돌린다. (조건 : leftIdx < rightIdx)  
4. 만약 stuff[leftIdx]값과 stuff[rightIdx]값의 합이 lift 값보다 작거나 같을 경우 leftIdx 값은 ++, rightIdx 값은 --한다. 또한 두 개의 짐이 들어갔다는 뜻의 twoStuff 값을 ++한다. (처음 선언/할당할 때 twoStuff 기본 값은 0)  
5. 4번의 if문 조건이 안 맞는 경우 가장 무거운 쪽(rightIdx) 하나만 들어갈 수 있다는 것이 되니 else문을 만들어서 rightIdx값만 --한다. twoStuff와는 상관없다.  
6. while문이 끝나면 stuff.length에 twoStuff 값을 뺀 걸 return한다.  

<br>

## 해답 코드  
### siri(작성자).ver  
```js
function movingStuff(stuff, limit) {
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
<br>

### reference.ver
```js  
function movingStuff(stuff, limit) {
  let twoStuff = 0;
  // 짐을 무게순으로 오름차순 정렬
  let sortedStuff = stuff.sort((a, b) => a - b);
  // 가장 가벼운 짐의 인덱스
  let leftIdx = 0;
  // 가장 무거운 짐의 인덱스
  let rightIdx = sortedStuff.length - 1;
  while(leftIdx < rightIdx) {
      // 가장 가벼운 짐과 무거운 짐의 합이 limit 보다 작거나 같으면 2개를 한번에 나를 수 있다
      if(sortedStuff[leftIdx] + sortedStuff[rightIdx] <= limit) {
      // 다음 짐을 확인하기 위해 가장 가벼운 짐과 무거운 짐을 가리키는 인덱스를 옮겨주고
      // 한번에 2개 옮길 수 있는 개수를 +1 해준다   
          leftIdx++;
          rightIdx--;
          twoStuff++;
      } else {
          // 위 조건에 맞지 않는 경우는 한번에 한 개만 나를 수 있는 경우이기 때문에
          // 가장 무거운 짐의 인덱스만 옮겨준다
              rightIdx--;
      }
  }
  // 전체 짐의 개수에서 한번에 2개를 나를 수 있는 경우를 빼 주면 총 필요한 박스의 개수를 구할 수 있다
  return stuff.length - twoStuff;
}
```  
<br>

### siri(작성자)-upgrade.ver  
레퍼런스.ver을 참고하여 if문을 줄여보았다.  

```js
function movingStuff(stuff, limit) {
  let temp = stuff.slice();
  temp.sort((a,b) => a-b); 
  let twoCount=0; // 두 개의 짐이 들어갈 박수 개수

  while(temp.length > 1){ // 처음부터 2개를 합성할 수 있나를 볼 것이기에 1개 이상을 조건으로 둔다.  
    if(temp[temp.length-1] + temp[0] <= limit){
      twoCount++;
      temp.pop();
      temp.shift();
    }
    else {
      // 위 if문이 만족되지 않으면 2개가 들어가지 못한단 것이 되니 무거운 것을 뺀다.
      temp.pop();
    }
  }

  return stuff.length - twoCount;
}
```  
<br>

## 기타 - 한마디  
레퍼런스 없이 푼 것도 뿌듯했는데 레퍼런스를 참고해서 어레인지 업그레이드 시킨 코드도 생각할 수 있다는 것이 좋은 시간이었다.   
다음엔 다른 알고리즘 문제도 풀어보자.  

<br>
<br>