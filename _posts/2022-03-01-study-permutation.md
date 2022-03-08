---
published: true
title:  "[JavaScript] 순열 Permutation"
excerpt: ""

categories:
  - Algorithm
tags:
  - [Algorithm, JavaScript, Permutation]

toc: true
toc_sticky: true
 
date: 2022-03-01 20:06:30
last_modified_at: 2022-03-01 20:06:30
---

# 순열의 개념
순열을 알려면 조합도 알아야 하는데, 이는 다음에 포스팅하도록 하겠다.  
_이후 링크를 붙이도록 하자_  

서로 다른 n개의 물건 중에서 r개를 택하여 한 줄로 배열하는 것을 순열이라 하고, r개 택한 종류가 같다고 해도 배열된 순서가 다르다면 이 또한 하나의 경우의 수로 따진다.  
조합은 순서에 상관없이 선택한 것이라면, 순열은 순서를 따진다는 것이 차이점이다.  
이러한 순열의 경우의 수를 구하는 것을 수학에서는 nPr로 나타낸다.  
이러한 수학 공식을 이용하면 코드로도 쉽게 나타낼 수 있다.  

수학에서는 nPr을 구하라고 하면 다음과 같다.  
>$$
_nP_r = \frac{n!}{(n-r)!} = \frac{n \times (n-1) \times (n-2) \times \cdots \times 1}{(n-r) \times (n-r-1) \times (n-r-2) \times \cdots \times 1}
 = n \times \cdots \times (n-r+1)
$$

다만 위와 같은 상황은 '경우의 수'를 구할 수 있을 뿐 순열의 종류를 구하진 않는다.  
그래서 원리를 이해하고 그 상황을 이용하여 알고리즘을 구성하고자 한다.  

## 순열 예시
```js
Input: [1, 2, 3] 중 3개 고르기
Output: [
  [ 1, 2, 3 ], [ 1, 3, 2 ],
  [ 2, 1, 3 ], [ 2, 3, 1 ],
  [ 3, 1, 2 ], [ 3, 2, 1 ],
]

Input: [1,2,3,4] 중 3개 고르기
Output: [
  [ 1, 2, 3 ], [ 1, 2, 4 ],
  [ 1, 3, 2 ], [ 1, 3, 4 ],
  [ 1, 4, 2 ], [ 1, 4, 3 ],
  [ 2, 1, 3 ], [ 2, 1, 4 ],
  [ 2, 3, 1 ], [ 2, 3, 4 ],
  [ 2, 4, 1 ], [ 2, 4, 3 ],
  [ 3, 1, 2 ], [ 3, 1, 4 ],
  [ 3, 2, 1 ], [ 3, 2, 4 ],
  [ 3, 4, 1 ], [ 3, 4, 2 ],
  [ 4, 1, 2 ], [ 4, 1, 3 ],
  [ 4, 2, 1 ], [ 4, 2, 3 ],
  [ 4, 3, 1 ], [ 4, 3, 2 ] 
  ]
```

# 순열 알고리즘 로직    

[1,2,3] 중 2개를 골라 나열하라고 한다면 어떻게 풀어야 할까?  

우선 [1,2,3] 중 한 개를 골라낸다면 [1], [2], [3] 세 가지라고 할 수 있다.  
이후 남은 두 가지([2,3], [1,3], [1,2]) 중에서 또 하나를 골라야 한다.  그러면 각각 두 가지씩 고를 수 있을 것이다.  

감이 왔다면 아! 하게 될 것이다.  
순열은 재귀함수로 풀 수 있고, 그 재귀함수는 n개 중 1개 고르는 상황을 반복하면 된다.  
언제까지? r개가 골라질 때까지!  

```js
// [1,2,3,4] 중 n개를 골라 순열을 나타내야 하는 상황이라면?
// 정의한 재귀함수를 permutation(순열)이라고 하자.
1(fixed) => permutation([2, 3, 4]) => 2(fixed) => permutation([3, 4]) => ...
2(fixed) => permutation([1, 3, 4]) => 1(fixed) => permutation([3, 4]) => ...
3(fixed) => permutation([1, 2, 4]) => 1(fixed) => permutation([2, 4]) => ...
4(fixed) => permutation([1, 2, 3]) => 1(fixed) => permutation([2, 3]) => ...
```


## 순열 코드
```js
const permutation = function (arr, selectNumber) {
    // arr = n개의 요소가 들은 배열
    // selectNumber = 골라야 하는 개수 >> nPr에서의 r

    const result = [];
    // 순열을 담을 답 배열

    if (selectNumber === 1) return arr.map((el) => [el]); 
    // 1개만 선택하는 거라면 그냥 arr의 원소 개수를 담아서 내보내면 된다.
    // 또한 이 재귀함수의 마지막 상황으로 볼 수 있다.

    arr.forEach((fixed, index, origin) => {
      // fixed = 처리하는 요소(보통 element로 씀)
      // index = 처리하는 요소의 인덱스값
      // origin = forEach를 호출한 배열 = arr

      const rest = [...origin.slice(0, index), ...origin.slice(index+1)] 
      // 해당 fixed를 제외한 나머지 배열 
      const permu = permutation(rest, selectNumber - 1); 
      // 나머지에 대해서 재귀함수를 이용해 순열을 구한다.
      const attached = permu.map((el) => [fixed, ...el]); 
      // 돌아온 순열에 fixed 값을 붙인다.
      result.push(...attached); 
      // 답을 집어넣을 result 배열에 spread로 push
    });

    return result;
}
```

이로서 순열을 구하는 방법을 알았다!  
다음엔 이를 이용한 코딩 문제도 풀어보고자 한다.  
<br>

