---
published: true
title:  "[Artillery / Express] 499, 504 http, TimeOut(ETIMEDOUT) 에러가 나오는 이유"  
excerpt: ""

categories:
  - JavaScript
tags:
  - [JavaScript, Artillery, Node.js, Express, express-ipfilter, NginX, ELB, AWS]

toc: true
toc_sticky: true
 
date: 2023-02-06 23:20:00
last_modified_at: 2023-02-06 23:20:00
---

## 504 에러? ETIMEDOUT 에러?  
부하테스트에 특화된 Artillery 이용해서 `Node.js`의 `Express` 서버의 부하테스트( or 로드테스트 / AB테스트)를 한다?  
그런데 단순히 test 코드로 정해진 변수 값을 내보내는 REST API로 부하 테스트를 해본 건데 ETIMEDOUT이나 504 에러가 절반 가까이 차지한다?  

그렇다면 다음을 확인해 보세요.  
*(실제로 직접 경험하고 해결한 경우만 나열했으므로 또다른 원인이 있을 수 있습니다.)*  

<br>

### 1. express-ipfilter를 사용하는가?  

단순히 '사용한다'가 문제가 아니다. filter를 해야 하는 ip 요소가 많을수록 꽤 많은 처리 시간이 소요된다.  
필터해야 하는 ip 수가 많을수록 504 에러가 난다는 것을 확인했다.  
즉, 디도스 공격을 하는 IP를 수집하고 그걸 express-ipfilter에 매일 갱신하며 추가할 경우 n백 개가 되는 순간부터 1초당 1000개의 단순 value 내보내는 REST API마저 에러가 날 것이다.(원래 1초당 1500개도 문제없어야 한다.)  
나는 이 ip 필터 항목을 줄인 것만으로도 504 에러를 없앨 수 있었다.  

<br>

대부분의 디도스 공격이나 잘못된 요청들의 해외 IP들은 잘못된 경로(정의되지 않은 라우터)로 파고드니까 그 경로 자체로는 Express 서버에 접근할 수 없게 막아야 한다.(`NginX`나 AWS ELB의 `rule` 등)  

<br>

### 2. Artillery의 TimeOut 세팅을 했는가?  
Artillery에는 REST API에 한해서 timeout을 설정할 수 있다!  
이 timeout을 따로 설정해 두지 않으면 서버가 느리게, 혹은 너무 많은 요청으로 인해 답이 밀려서 몇십 초 후에 response를 보낸다면 Artillery는 기다리지도 않고 그저 검사를 끝낸 뒤 ETIMEDOUT이라고 집계하거나, 혹은 서버로부터 499반응을 내보냈다는 로그를 확인할 수 있을 것이다.  
부하테스트를 할 때는 넉넉하게 100초 이상은 두고 하길 바란다.  

* 예시 코드(원문은 아래 참고 문서를 가볼 것)  
```shell
config:
  target: "http://my.app"
  http:
    # Responses have to be sent within 10 seconds, or an `ETIMEDOUT` error gets raised.
    timeout: 10
```  


## 기타 - 한마디  
제발! 꼭! 공식 문서를 간단하게라도 훑어서 다루는 법을 잘 익힌 뒤에 써먹도록 하자.  

<br>

## 참고 문서  
[Artillery timeout 세팅](https://www.artillery.io/docs/guides/guides/http-reference#request-timeouts){:target="_blank"}


<br>
<br>