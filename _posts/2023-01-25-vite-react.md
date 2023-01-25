---
published: true
title:  "[React] Vite으로 React 시작하기(단순 명령어 정리)"  
excerpt: ""

categories:
  - React
tags:
  - [React, JavaScript, Vite]

toc: true
toc_sticky: true
 
date: 2023-01-25 22:30:00
last_modified_at: 2023-01-25 22:30:00
---

## Vite이 뭐길래  
프론트엔드에서 웹사이트 배포를 하기 위해 꼭 하는 과정이 무엇인지 아는가?  
바로 `build`다.  
`React`로 프로젝트를 배포하기 위해 `npm run build`를 한 번쯤은 했을 것이다.  
이 명령어로 빌드 폴더를 생성할 때 시간이 좀 걸리는데, 이때 걸리는 시간으로 맥북의 성능을 비교하기도 한다.(그 외에 다른 걸로도 비교하곤 한다.)  
[빌드로 맥북 성능 비교하는 영상 링크](https://youtube.com/shorts/N9aA3_ZAnJc?feature=share){:target="_blank"}

이 `build`를 조금이라도 빠르게 하는 방법 중 하나가 바로 `Vite`를 쓰는 것이다.  
실제 [Vite 공식 사이트](https://vitejs-kr.github.io/){:target="_blank"}의 소개를 보면 아래와 같은 얘기를 한다.  
즉 `build`에 최적화된 도구라고 할 수 있다.  

`build` 말고도 다른 기능들도 많으니 따로 공식 문서에 들어가 참고하자.  

<br>

> Vite(프랑스어로 "빠르다(Quick)"를 의미하며, 발음은 "veet"와 비슷한 /vit/ 입니다.)은 빠르고 간결한 모던 웹 프로젝트 개발 경험에 초점을 맞춰 탄생한 빌드 도구이며, 두 가지 컨셉을 중심으로 하고 있습니다.  
>
> 개발 시 네이티브 ES Module을 넘어 더욱 다양한 기능을 제공합니다. 가령, Hot Module Replacement (HMR)과 같은 것들 말이죠.  
>
>번들링 시, Rollup 기반의 다양한 빌드 커맨드를 사용할 수 있습니다. 이는 높은 수준으로 최적화된 정적(Static) 리소스들을 배포할 수 있게끔 하며, 미리 정의된 설정(Pre-configured)을 제공합니다. - Vite -  

<br>  

## 간단한 Vite 프로젝트 생성  

정말 단순히 터미널 명령어만 나열하겠다.  
`react`말고도 `vue` 등도 있으니 위에 링크로 남겨둔 공식 사이트를 확인하길 바란다.  

**yarn**  

```shell
# Mac - m1 Pro
# Mac에 yarn이 안 깔려있을 경우
npm install -g yarn

# vite project 시작(JavaScript)
yarn create vite [프로젝트명] --template react

# vite project 시작(TypeScript)
yarn create vite [프로젝트명] --template react-ts
```  

<br>

**npm**  

```shell
# Mac - m1 Pro
# npm 6.x(JavaScript)
npm create vite@latest [프로젝트명] --template react

# npm 7+, '--'를 반드시 붙일 것(JavaScript)
npm create vite@latest [프로젝트명] -- --template react

# TypeScript는 react-ts로 설정
```  

<br>

## 백엔드 개발자로서 Vite으로 프론트 프로젝트를 만든 이유  
원래 나는 Node.js Express 개발자로서 Vite에 크게 관심이 없었다.  
그런데 socket 부하 테스트를 하려는데 매우 많은 동시 연결 수가 필요했고, 그걸 Vite으로 만든 임시 프로젝트가 해결해줬다.  
Vite으로 웹 프로젝트를 만들어서 소켓 연결 세팅을 해두고 `npm run dev`로 웹사이트를 실행, 그리고 창을 킨 채 해당 프로젝트 터미널에서 `Cmd(⌘) + S`를 꾹 누르면 해당 컴퓨터의 한계만큼 동시 연결을 진행해준다.  

**처음 Vite으로 프로젝트 시작할 때의 터미널**  
<center><img width="402" alt="npm run dev" src="https://user-images.githubusercontent.com/87490361/214580645-db13702d-908e-49ee-8edc-1f0c39c003da.png"></center>

<br>

**프로젝트 창에 들어간 후 터미널에 `Cmd(⌘) + S`를 한 번 눌렀을 때**
<center><img width="601" alt="Cmd S" src="https://user-images.githubusercontent.com/87490361/214580652-87f1fcb2-7af2-4a37-b671-25a599bc1801.png"></center>

<br>

**`Cmd(⌘) + S`를 꾹 오래 눌렀을 때**
<center><img width="544" alt="Cmd S2" src="https://user-images.githubusercontent.com/87490361/214580656-930306d0-692f-4e14-a0cd-8638ebaab80a.png"></center>

<br>

## 기타 - 한마디  
Vite으로 서버 쪽도 여러모로 테스트 쪽으로 이득을 본 것 같아서 좋다. 역시 한쪽만 파기보다는 같이 일하게 되는 연관 파트의 지식도 계속 공부해야겠다.  

<br>

## 참고 문서  
[Vite](https://vitejs-kr.github.io/){:target="_blank"}  

<br>
<br>