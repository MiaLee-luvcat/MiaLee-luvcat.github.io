---
published: true
title:  "[TIL] 클라이언트 빌드와 배포 & Section 2 HA"
excerpt: "[배포] 클라이언트 빌드와 배포 & 첫 HA 후기"

categories:
  - TIL
tags:
  - [배포, 빌드, SSR, CSR, TIL, HA]

toc: true
toc_sticky: true
 
date: 2021-09-28 20:00:00
last_modified_at: 2023-03-23 13:00:00
---

## 들어가기 전에
오늘은 섹션 2 HA 시작하는 날! 이지만...  
동시에 빌드와 배포를 배운 날이기도 하다.  
코플릿 형태의 ha를 보기 전에 솔로 공부부터 해야 하는 형태..  
그냥 공부나 더 열심히 하고 싶은 마음은 굴뚝 같지만, 공부에 스킵이라는 건 없기에, 나름 시간 내에 열심히 보려고 했던 기억이 난다. 심지어 과제도 있었다!  


# [배포] 클라이언트 빌드와 배포  
## 소개  
### Achievement Goals  
* 정적 웹사이트와 동적 웹사이트가 어떻게 다른지 이해할 수 있다.  
* 빌드가 무엇인지 이해할 수 있다.  
* 정적 웹사이트 형태로 만들어지는 현대의 웹 앱이 왜 빌드 과정을 필요로 하는지 알 수 있다.  
* 정적 웹사이트를 배포할 수 있다.  
* 정적 웹사이트 배포 시 발생하는 문제를 이해하고 해결할 수 있다.  
* Landing Page라 불리는 정적 웹사이트에서 사용하는 다양한 프론트엔드 기술들을 스스로 찾아볼 수 있다.  

## 빌드  
### SSR과 CSR  

**SSR vs CSR**
SSR(Server Side Rendering)과 CSR(Client Side Rendering)의 차이점을 설명할 것이다. 웹 개발에서 이 두 가지의 차이점을 아는 것은 매우 중요하다. 먼저 SSR과 CSR의 정의와 차이점을 설명하겠다.  
<br>

**What is SSR ?**  
<center><img width="735" alt="SSR" src="https://user-images.githubusercontent.com/87490361/157177565-89037180-3a35-47d9-96d1-ddee6b30d2bc.png"></center>  
<br>  

SSR은 Server Side Rendering의 줄임말이다. 웹 페이지를 브라우저에서 렌더링하는 대신에, 서버에서 렌더링한다.  
브라우저가 서버의 URI로 GET 요청을 보내면, 서버는 정해진 웹 페이지 파일을 브라우저로 전송한다. 그리고 서버의 웹 페이지가 브라우저에 도착하면 완전히 렌더링된다.  
서버에서 웹 페이지를 브라우저로 보내기 전에, 서버에서 완전히 렌더링했기 때문에 Server Side Rendering이라고 한다.  
웹 페이지의 내용에 데이터베이스의 데이터가 필요한 경우, 서버는 데이터베이스의 데이터를 불러온 다음 웹 페이지를 완전히 렌더링 된 페이지로 변환한 후에 브라우저에 응답으로 보낸다.  

웹 페이지를 살펴보던 사용자가, 브라우저의 다른 경로로 이동하면 어떻게 될까?  
브라우저가 다른 경로로 이동할 때마다 서버는 이 작업을 다시 수행합니다.  
<br>

**What is CSR ?**  
<center><img width="735" alt="CSR" src="https://user-images.githubusercontent.com/87490361/157175683-1445c672-4141-47a3-b818-46c60e24f73b.png"></center>  
<br>  

CSR은 Client Side Rendering을 의미한다. 일반적으로 CSR은 SSR의 반대로 여겨진다.  
SSR이 서버 측에서 페이지를 렌더링한다면, CSR은 클라이언트에서 페이지를 렌더링한다.  
웹 개발에서 사용하는 대표적인 클라이언트는 웹 브라우저다. 브라우저의 요청을 서버로 보내면 서버는 웹 페이지를 렌더링하는 대신, 웹 페이지의 골격이 될 단일 페이지를 클라이언트에 보낸다.  
이때 서버는 웹 페이지와 함께 JavaScript 파일을 보낸다. 클라이언트가 웹 페이지를 받으면, 웹 페이지와 함께 전달된 JavaScript 파일은 브라우저에서 웹 페이지를 완전히 렌더링 된 페이지로 바꾼다.  

웹 페이지에 필요한 내용이 데이터베이스에 저장된 데이터인 경우에는 어떻게 해야 할까?  
브라우저는 데이터베이스에 저장된 데이터를 가져와서 웹 페이지에 렌더링을 해야 한다. 이를 위해 API가 사용된다.  
웹 페이지를 렌더링하는 데에 필요한 데이터를 API 요청으로 해소한다.  

마지막으로, 브라우저가 다른 경로로 이동하면 어떻게 될까?  
CSR에서는 SSR과 다르게, 서버가 웹 페이지를 다시 보내지 않는다.  
브라우저는 브라우저가 요청한 경로에 따라 페이지를 다시 렌더링합니다. 이때 보이는 웹 페이지의 파일은 맨 처음 서버로부터 전달받은 웹 페이지 파일과 동일한 파일이다.  
<br>

**The Difference**  
CSR과 SSR의 주요 차이점은 페이지가 렌더링되는 위치다.  
SSR은 서버에서 페이지를 렌더링하고, CSR은 브라우저(클라이언트)에서 페이지를 렌더링한다. 브라우저는 사용자가 다른 경로를 요청할 때마다 페이지를 새로고침 하지 않고, 동적으로 라우팅을 관리한다.  
<br>

**Use SSR**  
[SEO(Search Engine Optimization)](https://en.wikipedia.org/wiki/Search_engine_optimization){:target="_blank"}가 우선 순위인 경우, 일반적으로 SSR(Server Side Rendering)을 사용한다.  
웹 페이지의 첫 화면 렌더링이 빠르게 필요한 경우에도, 단일 파일의 용량이 작은 SSR이 적합하다.  
웹 페이지가 사용자와 상호작용이 적은 경우, SSR 을 활용할 수 있습니다.  
<br>

**Use CSR**  
SEO 가 우선순위가 아닌 경우, CSR을 이용할 수 있다.  
사이트에 풍부한 상호 작용이 있는 경우, CSR 은 빠른 라우팅으로 강력한 사용자 경험을 제공한다.  
웹 애플리케이션을 제작하는 경우, CSR을 이용해 더 나은 사용자 경험(빠른 동적 렌더링 등)을 제공할 수 있다.  
<br>

### SSR 예시  
**네이버 블로그**
네이버 블로그는 2020년에 SSR 방식을 도입했다.  
여러 가지 이유가 있겠지만 대표적인 이유는 SSR이 검색엔진 최적화(Search Engine Optimization, SEO)에 유리한 이점이 있기 때문이다.  
블로그 같은 경우는 특히 검색엔진에 최대한 노출되는 게 유리하고, 다른 웹사이트에 비해 사용자와 상호작용이 많지 않기 때문에 SSR이 합리적인 선택이 될 수 있다.  
<center><img width="1000" alt="네이버 블로그 SEO" src="https://user-images.githubusercontent.com/87490361/159660337-58cbdb12-d18d-4b45-9c62-db93468bf5b1.png"></center>  
<br>
개발자 관련 포스팅을 한 네이버 블로그의 네트워크 탭을 보시면 html 파일에 내용이 똑같이 담긴 상태인 것을 볼 수 있다.  
따라서 구글, 네이버 같은 검색엔진 크롤러가 html에 접근하여 쉽게 내용을 가져갈 수 있다.  
<br>  

**The NewYork Times**
뉴욕 타임스 홈페이지도 SSR 방식을 사용하고 있다.  
SSR의 대표적인 단점인 많은 사용자가 클릭할 때마다 전체 웹사이트를 다시 서버에서 받아오기 때문에 발생하는 서버 과부하 이슈가 있음에도 불구하고, CSR에 비해 초기 로딩 속도가 빠르기 때문에 구독자가 신문기사를 빠르게 읽을 수 있다는 장점이 있다.  
그뿐만 아니라 해당 신문사의 기사가 검색엔진에 노출되는 것이 중요하기 때문에 SEO(Search Engine Optimization)에 유리한 SSR을 이용하고 있다.  
<center><img width="1000" alt="뉴욕타임즈 네트워크" src="https://user-images.githubusercontent.com/87490361/159660716-44ef1f4d-589d-4585-ba5d-b8ff5e3cfacd.png"></center>  
<br>
위의 예시를 보면, todayspaper라는 완성된 html 파일을 받아와서 렌더링한다. 그 html 파일 안에 해당 내용이 그대로 담겨 있는 상태이기 때문에 검색엔진 크롤러가 내용을 수집하기 용이하다.  
<br>

### CSR 예시  
**아고다**
아고다뿐만 아니라 많은 예약 사이트들은 CSR을 사용하고 있다.  
SSR에서는 서버에서 렌더링을 해야 하기 때문에 상호작용(interaction)이 많아질수록 서버에 부담이 많은 반면에, CSR에서는 서버가 클라이언트에 필요한 데이터만 넘겨주기 때문에 부담이 적다. 그리고 SPA(Single Page Application)를 기반으로 화면의 일부만 받아온 데이터로 변경해 주기 때문에 빠른 렌더링으로 User Experience(사용자 경험)에 유리하다.  

최근까지 아래 예시처럼 html이 빈 페이지이기 때문에 검색엔진 최적화(SEO)를 하기에는 SSR에 비해 불리하다는 특징이 있었으나, 구글에서 이러한 부분을 보완하기 위해 삽입된 자바스크립트 코드를 분석, 실행시켜 크롤링을 하고 있다.  
그러나 검색엔진 최적화가 꼭 필요한 서비스라면 조금 더 최적화에 유리한 SSR을 사용하는 것을 권장하고 있다.  
<center><img width="1000" alt="아고다 네트워크" src="https://user-images.githubusercontent.com/87490361/159687207-f4256127-060a-47d0-9370-e3907c2f699a.png"></center>  
<br>

### SSR과 CSR 코드 예시  
**SSR 코드 예시**  
Open Sandbox 버튼을 클릭해서 **새로고침**을 해보자.  

<center><img width="500" alt="스크린샷" src="https://user-images.githubusercontent.com/87490361/159690320-b195eeab-10cd-47d4-8c5c-674392ecc8d8.png"></center>  
<br>
<iframe src="https://codesandbox.io/embed/ssr-example-kllxh?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="SSR example"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>
<br>

**CSR 코드 예시**  
Open Sandbox 버튼을 클릭해서 **새로고침**을 해보자.  

<center><img width="500" alt="스크린샷" src="https://user-images.githubusercontent.com/87490361/159690320-b195eeab-10cd-47d4-8c5c-674392ecc8d8.png"></center>  
<br>
<iframe src="https://codesandbox.io/embed/csr-example-pqi5t?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="CSR example"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

<br/>
<br/>