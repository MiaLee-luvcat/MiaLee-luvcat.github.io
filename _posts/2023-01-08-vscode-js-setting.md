---
published: true
title:  "[VSCode] javascript 자동정렬 command(⌘) + K + F 명령어 안 먹힐 때 - Mac 기준"
excerpt: ""

categories:
  - Visual Studio Code
tags:
  - [Visual Studio Code]

toc: true
toc_sticky: true
 
date: 2023-01-08 18:01:00
last_modified_at: 2023-01-08 18:01:00
---

<br>

## 이 글을 쓰게 된 이유  
개인 맥북을 포맷한 뒤 다시 시작하는데 자동정렬이 안 돼서 5분 정도 애를 먹었다.  
VSCode에서 익스텐션으로 Prettier나 Beautify를 안 쓰고 나처럼 `command(⌘) + K + F`로 특정 부분만 코드정렬을 하는 사람을 위한 글이므로 참고 바란다.  

<br>

## VSCode에서 Extensions 안 쓰고 자동정렬 하는 방법  
VSCode로 javascript를 다루는 사람이라면 알아둬야 할 단축키 중 하나!  
> `command(⌘) + K + F`  

내가 드래그앤드롭 같은 블록을 지정한 부분에 한해서 저 단축키를 쓰면 내 세팅에 맞춰 자동정렬이 된다.  

<br>

### 예시
**VSCode 기본 세팅 공백 4칸**  
<center><img width="592" alt="기본 공백 4칸" src="https://user-images.githubusercontent.com/87490361/211190953-faf217d1-5eec-4bbb-8289-288b2a429851.png"></center>  

<br>

**VSCode 공백 2칸으로 바꿨을 때**  
신경 쓰이는 세로줄..  
<center><img width="590" alt="기본 공백 2칸 변경 - 1" src="https://user-images.githubusercontent.com/87490361/211190959-867e9101-eb72-45bb-82eb-185a4b692fd3.png"></center>  

<br>

**`command(⌘) + A`(전부 선택) 이후 `command(⌘) + K + F`(자동정렬)**  
편안..
<center><img width="579" alt="기본 공백 2칸 변경 - 2" src="https://user-images.githubusercontent.com/87490361/211191142-b9956cf6-d7b9-4e2d-a24e-9c258174e1ac.png"></center>  

<br>

## 자동정렬 단축키가 안 먹혀요  
> The key combination (⌘K, ⌘F) is not a command.
<center><img width="414" alt="커맨드 에러 " src="https://user-images.githubusercontent.com/87490361/211191481-cb509905-9dc3-4a77-bacf-5f78fdef6fde.png"></center>  

<br>

오늘 내가 겪은 일이다.  
결론부터 말하면 `setting.json`을 확인해봐야 하며, 부가적으로는 `javascript` 언어 파일 기준이라는 것을 염두에 두자.  

<br>

### 해결 방법  
1. `command(⌘) + Shift(⇧) + P`를 입력한다.  
2. `setting.json`을 검색 후 `Open User Settings`를 선택한다.  
3. `"javascript.format.enable"`가 `false`로 되어 있다면 `true`로 바꾼다.  

<br>

**`command(⌘) + Shift(⇧) + P`**  
<center><img width="863" alt="open user settings" src="https://user-images.githubusercontent.com/87490361/211192125-d03994a8-4561-43e4-837e-5ecb8cb9f757.png"></center>

<br>

**`"javascript.format.enable"` 확인**  
<center><img width="530" alt="false" src="https://user-images.githubusercontent.com/87490361/211192124-5212f91d-7a5e-41c5-aba5-45f86fde9ee8.png"></center>

<br>

**`"javascript.format.enable": true`로 변경**  
<center><img width="461" alt="true" src="https://user-images.githubusercontent.com/87490361/211192126-de5db2c3-cad7-42f6-8ce1-8e61fb2b00e4.png"></center>

<br>  
<br>  