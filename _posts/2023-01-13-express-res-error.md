---
published: true
title:  "[Node.js & Express] Error : [ERR_HTTP_HEADERS_SENT]: Cannot set headers after they are sent to the client"  
excerpt: ""

categories:
  - JavaScript
tags:
  - [JavaScript, Node.js, Express, error.log]

toc: true
toc_sticky: true
 
date: 2023-01-13 20:19:00
last_modified_at: 2023-01-13 20:19:00
---

## 에러가 났다.  
Node.js를 쓴다? 거기에 Express로 서버를 다룬다?  
그러면 가끔 접할 수 있는 에러가 있다.  

> `Error [ERR_HTTP_HEADERS_SENT]: Cannot set headers after they are sent to the client`  

이게 무슨 에러인가, 대체 뭐가 문제인가, 클라이언트와 헤더는 서버와 무슨 상관인가 등...  
여러 가지 고민을 해보지만 막상 저 문장만 보고는 뭐가 문제인지 명확히 인지할 수 없었다.  

그런데 전체 에러 문구를 보다 보면 코드의 어디가 문제인지 알려주긴 해서 그 부분을 보면 아! 하게 된다.  

<br>

```js
Error [ERR_HTTP_HEADERS_SENT]: Cannot set headers after they are sent to the client
    at new NodeError (node:internal/errors:372:5)
    at ServerResponse.setHeader (node:_http_outgoing:576:11)
    at ServerResponse.header (/root/project/node_modules/express/lib/response.js:794:10)
    at ServerResponse.json (/root/project/node_modules/express/lib/response.js:275:10)
    at menu (/root/project/index.js:number1:number2) // << 여기!!
    at process.processTicksAndRejections (node:internal/process/task_queues:95:5) {
  code: 'ERR_HTTP_HEADERS_SENT'
}
```  
<br>

'여기!!'라고 한 부분의 실제 코드는 아래와 비슷한 구조다.  

```js
const api = (req, res) => {
  if(req == '조건') res.status(200).json({ message: '조건' })

  return res.status(200).json({ message: '리턴' }) // << 에러가 난 부분
}
```

<br>

## 해결법  

아주 단순한 에러였다.  
response(`res`)를 두 번 써서 일어나버린 에러!  
위 코드에서 처음 `if`문을 썼을 때 `return`으로 함수를 나가지 않아서 그 아래의 `return`문에 들어서게 된 것이다.  
이미 api를 호출한 클라이언트에게 `{ message: '조건' }`를 `res`로 줬는데 왜 또 주냐는 것.  

그래서 아래처럼 `return`을 추가하면 에러가 헤결된다.  


<br>

```js
const api = (req, res) => {
  if(req == '조건') return res.status(200).json({ message: '조건' })

  return res.status(200).json({ message: '리턴' })
}
```

<br>


## 기타 - 한마디  
`return`을 단순히 값을 내보내기 위한 거라고 생각하지 말고, 그 루프에서 벗어난다는 것을 인지하고 잘 사용하도록 하자.  

<br>
<br>