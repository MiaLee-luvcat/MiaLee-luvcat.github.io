---
published: true
title:  "(작성중)[Database] RDBMS와 NoSQL의 차이"
excerpt: ""

categories:
  - Database
tags:
  - [Database, RDBMS, MySQL, NoSQL]

toc: true
toc_sticky: true
 
date: 2022-04-20 16:14:00
last_modified_at: 2022-04-21 23:00:00
---

<br>

<center><img width="800" alt="sql-nosql" src="https://user-images.githubusercontent.com/87490361/164488263-3ec1945e-bf1e-489d-ae8b-04eb8f8a8768.jpeg"></center>  
<br>

## 이 글을 쓰게 된 이유  
나는 그동안 NoSQL을 단순히 개념 배우며 살짝 테스트 형식으로 써보기만 했지 실전으로 써본 적은 없다.  
다만 RDBMS는 확실하게, 당연하게 사용할 수밖에 없었는데도 불구하고...  
최근 면접에서 이 둘의 차이점이나 특징을 얘기 못하고 끝난 적 있었다...ㅠㅠ;  
그래서! 이왕 얘기 나온 김에 정리하면서 제대로 파악하고자 한다!  


## RDBMS?  
우선 둘의 차이점을 알기 전에 각각의 특징과 개념은 알아야 하지 않을까?  
RDBMS는 DBMS에서 Relational의 약자 R이 붙은 단어이다.  

### DBMS는?  
그렇다면 DBMS는 뭘까?  
사실 데이터베이스의 정의부터 파악해야겠지만, 우리는 이 글에서 RDBMS와 NoSQL의 차이점을 알고 싶은 것이니,  
기본 개념은 알고 있다는 전제하에 간단히만 다뤄보자.  
DBMS는 **D**ata**B**ase **M**anagement **S**ystem의 약자로, 데이터베이스 관리 시스템이다.  
다수의 사용자들이 데이터베이스 내의 데이터를 접근할 수 있도록 해주는 소프트웨어 도구의 집합인데, 유형과 종류가 매우 많다.  

유형으로는 **RDBMS**, **NoSQL DBMS**, IMDBMS, CDBMS가 있고,  
종류로는 대표적으로 Oracle, MySQL, MSSQL, MariaDB 등이 있다.  

### 그래서 RDBMS는?  

<center><img width="800" alt="database-schema" src="https://user-images.githubusercontent.com/87490361/164479997-9990ff3e-546c-4703-b413-e8e38a99950a.jpg"></center>  
<center>&#60;데이터베이스 스키마 그림&#62;</center>
<br>

앞서 말했든 R은 Relational의 약자로, RDBMS는 관계형 데이터 베이스 시스템이라고 할 수 있다.  
관계형 데이터 모델을 기초로 두고 모든 데이터를 2차원 테이블 형태로 표현하는 데이터베이스를 RDB라고 하며, 그를 다루는 시스템인 것이다.  
RDBMS에서의 저장 방식은 SQL에 의해 저장되고 있으며 정해진 스키마에 따라 데이터를 저장하게 된다.  
<br>

<center><img width="800" alt="database-schema" src="https://user-images.githubusercontent.com/87490361/164479997-9990ff3e-546c-4703-b413-e8e38a99950a.jpg"></center>  
<center>&#60;프로젝트 때 사용했던 스키마&#62;</center>  
<br>

위 그림과 같이 여러 테이블이 외래키(foreign key)를 이용하여 연결되어 있는 상황을 참고하면 된다.  
user 테이블의 id는 고유키이지만 post 테이블의 userId, comment 테이블의 userId가 외래키로 연결되어 있다.  

이렇게 테이블간의 관계에서 외래키를 이용한 테이블 사이 Join이 가능하다는 게 RDBMS의 가장 큰 특징이다.  


## NoSQL?  


<br>

<br>
