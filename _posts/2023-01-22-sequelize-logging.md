---
published: true
title:  "[Node.js & Sequelize] mysql 쿼리문 로그 없애기"  
excerpt: ""

categories:
  - Database
tags:
  - [Node.js, Database, mysql, Sequelize]

toc: true
toc_sticky: true
 
date: 2023-01-22 14:09:00
last_modified_at: 2023-01-22 14:09:00
---

## mysql 쿼리문이 로그로 떠요  
`Node.js`에서 `mysql`(넓게는 RDBMS)을 다루는 `OMR`로 `Sequelize`를 많이 사용할 것이다.  
처음 세팅하다 보면 config 파일에서 무언가를 적지 않았기에, 혹은 디폴트값 그대로 적었기에 뜨게 되는 로그가 있다.  
아래의 이미지들은 최근 개인 서버에 mysql을 sequelize로 세팅하고 실행한 뒤의 서버 로그이다.  
  
이 외에도 수많은 시퀄라이즈 함수가 실행될 때 mysql 쿼리문 로그가 서버에 같이 뜬다.   
쿼리문이 뜨는 건 실제 mysql 혹은 sequelize.query 쪽에서 참고할 때 좋지만, 로그 정리 폼이 정해져 있다면 이 쿼리문이 포맷을 해칠 수 있다.  

<br>

<center><img width="512" alt="단순 DB 연결 로그" src="https://user-images.githubusercontent.com/87490361/213901221-e775778a-4eb4-4d7f-ab6e-281d84c44e4d.png"></center>  
<center><b>[DB연결 확인 로그]</b></center>  

<br>

<center><img width="1144" alt="siri.user 모델 세팅 로그" src="https://user-images.githubusercontent.com/87490361/214002207-900d6015-1ada-4b13-a64e-85a3652382fd.png"></center>  
<center><b>[siri DB에서 user 모델 세팅 로그]</b></center>  

<br>


## 숨기는 법  

처음에 이 상황에 대해 소개할 때 하나 언급한 것이 있다.  

> 처음 세팅하다 보면 config 파일에서 무언가를 적지 않았기에, 혹은 디폴트값 그대로 적었기에 뜨게 되는 로그가 있다.  

sequelize에서 config.json(혹은 js) 파일을 세팅할 때 아래와 같은 옵션을 설정할 수 있다.  

`'logging': false`  
이 옵션을 추가하면 로그가 안 뜨고 원래 설정한 로그만 서버에 뜨게 된다.  

<br>

<center><img width="744" alt="config.js 설정" src="https://user-images.githubusercontent.com/87490361/213901713-7056737d-5766-4ae7-8d18-4b84ebbb6aa6.png"></center>


<br>


## 기타 - 한마디  
한창 개발 쪽으로 아무것도 모를 때 이 로그가 계속 뜨는 게 신경 쓰였는데, 생각보다 단순한 작업으로 바로 없앨 수 있어서 잘 찾아보면 다 방법이 있구나, 했던 기억이 있다.  

<br>
<br>