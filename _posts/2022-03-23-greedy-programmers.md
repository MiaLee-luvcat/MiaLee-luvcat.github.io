---
published: true
title:  "[JavaScript] 프로그래머스 탐욕법(Greedy) - 체육복"
excerpt: ""

categories:
  - Programmers
tags:
  - [Programmers, Algorithm, JavaScript, Greedy]

toc: true
toc_sticky: true
 
date: 2022-03-23 20:43:00
last_modified_at: 2022-03-23 20:43:30
---

## 문제 설명  
점심시간에 도둑이 들어, 일부 학생이 체육복을 도난당했습니다. 다행히 여벌 체육복이 있는 학생이 이들에게 체육복을 빌려주려 합니다. 학생들의 번호는 체격 순으로 매겨져 있어, 바로 앞번호의 학생이나 바로 뒷번호의 학생에게만 체육복을 빌려줄 수 있습니다. 예를 들어, 4번 학생은 3번 학생이나 5번 학생에게만 체육복을 빌려줄 수 있습니다. 체육복이 없으면 수업을 들을 수 없기 때문에 체육복을 적절히 빌려 최대한 많은 학생이 체육수업을 들어야 합니다.  

전체 학생의 수 n, 체육복을 도난당한 학생들의 번호가 담긴 배열 lost, 여벌의 체육복을 가져온 학생들의 번호가 담긴 배열 reserve가 매개변수로 주어질 때, 체육수업을 들을 수 있는 학생의 최댓값을 return 하도록 solution 함수를 작성해주세요.  

## 제한 사항
* 전체 학생의 수는 2명 이상 30명 이하입니다.  
* 체육복을 도난당한 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.  
* 여벌의 체육복을 가져온 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.  
* 여벌 체육복이 있는 학생만 다른 학생에게 체육복을 빌려줄 수 있습니다.  
* 여벌 체육복을 가져온 학생이 체육복을 도난당했을 수 있습니다. 이때 이 학생은 체육복을 하나만 도난당했다고 가정하며, 남은 체육복이 하나이기에 다른 학생에게는 체육복을 빌려줄 수 없습니다.  


## 입출력 예  

| n | lost  | reserve | return |
|---|-------|---------|--------|
| 5 | [2,4] | [1,3,5] | 5      |
| 5 | [2,4] | [3]     | 4      |
| 3 | [3]   | [1]     | 2      |  

### 입출력 예 설명  
예제 #1  
1번 학생이 2번 학생에게 체육복을 빌려주고, 3번 학생이나 5번 학생이 4번 학생에게 체육복을 빌려주면 학생 5명이 체육수업을 들을 수 있습니다.  

예제 #2  
3번 학생이 2번 학생이나 4번 학생에게 체육복을 빌려주면 학생 4명이 체육수업을 들을 수 있습니다.  
<br>

# 풀이  
## 로직  
탐욕법 알고리즘에 대해서는 이전에도 푼 적이 몇 번 있다.  
[최소한의 동전 개수 구하기](https://mialee-luvcat.github.io/algorithm/Algorithm-Greedy/){:target="_blank"}  
[짐 나르기](https://mialee-luvcat.github.io/algorithm/Algorithm-Greedy2/){:target="_blank"}  

가장 적절한 방법을 찾아서 진행하는 탐욕법.  
나는 이번 문제에서 `lost`와 `reserve`의 학생들 배열에 주목했다. 왜냐면 한 학생이 동시에 들어갈 수 있기 때문이다.  
그래서 '여벌이 있는데 잃어버린 학생은 다른 학생에게 나눠줄 수 없다'는 것을 염두에 둔 채 풀어야 한다.  
그렇기에 첫 번째로 해야 할 것은 '여벌이 없는데 도난당한 학생'과 '여벌이 있으면서 도난당하지 않은 학생'을 먼저 알아둔 채 시작하기로 했다.  
이를 알기 위해 filter 고차함수를 쓰면 편하다.  

다음으론 빌려받지 못해서 체육시간에 참여하지 못하는 학생을 구할 것이다.  
이렇게 하면 전체 학생 수 n에다가 참여하지 못하는 학생을 빼서 return하면 된다.  
이 방법은 어찌 보면 교집합, 차집합 같은 집합 개념에서 따왔다고 할 수 있다.  

1. realLost와 realReserve를 filter를 이용하여 선언/할당한다.  
2. 빌려받지 못한 학생 배열 noBorrow를 filter를 이용하여 구한다.  
3. 전체 학생 수 n에서 noBorrow.length를 빼서 return한다.  

<br>

## 해답 코드 - 첫 번째
```js
function solution(n, lost, reserve) {
    
    // 도난당한 후 체육복이 0벌인 학생
    let realLost = rlost.filter(el => !rreserve.includes(el));
    
    // 도난 사건 이후에도 체육복 여벌이 있는 학생
    let realReserve = rreserve.filter(el => !rlost.includes(el));
    
    // 여벌을 빌려받지 못하여 체육 시간에 참가하지 못하는 학생 배열
    let noBorrow = realLost.filter((lost) => {
        // 여벌이 있는 학생이 옆 번호인지 절댓값으로 확인한다.
        let lend = realReserve.find(saver => Math.abs(saver-lost) === 1);
        
        // 여벌을 빌려받지 못했다면 lend 값이 undefined인 것을 이용하여
        // 빌려받지 못했다면 그대로 리턴한다.
        if(!lend) return lost;
        
        // 위의 if문을 스루했다면 빌려받은 것이므로
        // 해당 여벌옷 가졌던 학생을 realReserve에서 제외시킨다.
        realReserve = realReserve.filter(el => el !== lend);
    });
    
    return n - noBorrow.length;
}
```
<br>

이 코드를 제출하고 채점해 보면 테스트 18번이 실패로 뜬다...  
그래서 왜 그런가 하고 다른 분들의 경우를 살펴 보니, lost와 reserve를 sort한 뒤에 돌려보면 된대서 혹시나? 하고 sort부터 진행해봤더니 정말 됐다...   
테스트 케이스에서 lost와 reserve의 번호가 오름차순이 아니었나 보다.  
어찌 보면 이것도 당연히 신경 써야 했는데, 내가 제대로 생각하지 못했다 ㅠㅠ

그래서! sort로 진행한 상황도 보여주겠다.  

## 해답 코드 - 전체 케이스 통과.ver
```js
function solution(n, lost, reserve) {
    // 우선 lost와 reserve를 sort하여 오름차순으로 재정렬한다.
    let rlost = lost.sort((a,b) => {
        return a - b;
    });
    let rreserve = reserve.sort((a,b) => {
        return a - b;
    });
    
    // 도난당한 후 체육복이 0벌인 학생
    let realLost = rlost.filter(el => !rreserve.includes(el));
    
    // 도난 사건 이후에도 체육복 여벌이 있는 학생
    let realReserve = rreserve.filter(el => !rlost.includes(el));
    
    // 여벌을 빌려받지 못하여 체육 시간에 참가하지 못하는 학생 배열
    let noBorrow = realLost.filter((lost) => {
        // 여벌이 있는 학생이 옆 번호인지 절댓값으로 확인한다.
        let lend = realReserve.find(saver => Math.abs(saver-lost) === 1);
        
        // 여벌을 빌려받지 못했다면 lend 값이 undefined인 것을 이용하여
        // 빌려받지 못했다면 그대로 리턴한다.
        if(!lend) return lost;
        
        // 위의 if문을 스루했다면 빌려받은 것이므로
        // 해당 여벌옷 가졌던 학생을 realReserve에서 제외시킨다.
        realReserve = realReserve.filter(el => el !== lend);
    });
    
    return n - noBorrow.length;
}
```


## 기타 - 한마디  
프로그래머스 문제들은 처음 마련되었을 때 한 번 풀고 말 것이 아니라, 계속 생각하고 시간을 두고 또 풀어보고 해야 한다.  
테스트 케이스가 계속 추가되고, 내가 예상치 못한 입력에 대해 처리하지 못하기도 하기 때문이다.  
언젠가 한번 더 풀어봐야겠다.  

<br>
<br>