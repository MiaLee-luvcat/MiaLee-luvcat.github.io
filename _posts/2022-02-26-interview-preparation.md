---
published: true
title:  "[기술 면접] CSR과 SSR의 차이"

categories:
  - Interview
tags:
  - [Interview, SPA]

toc: true
toc_sticky: true
 
date: 2022-02-26 11:00:30
last_modified_at: 2022-03-01 15:13:00
---

## 기술 영역: SPA
SPA는 Single Page Application의 약자이다. 이에 대해서는 따로 포스팅을 할 예정이다.  
_이후 링크를 붙이도록 하자_  
이 SPA 영역에서 다룰 수 있는 질문, **CSR과 SSR의 차이**는 무엇일지 생각해보고 정리하기로 했다.  


# CSR과 SSR의 개념적 차이와 동작 방식을 구분하여 설명해주세요.

## CSR이란?
CSR은 Client Side Rendering(클라이언트 사이드 렌더링)의 약자이다.  
말 그대로 해석하면 클라이언트(브라우저) 측에서 렌더링을 한다는 의미인데, 동작 과정은 이러하다.  
<br>
HTML다운로드 >> JS 다운로드 >> JS 실행 >> API 서버로부터 DATA 받기 >> Content 확인 가능  

즉, 최초 로딩 시 브라우저가 서버에 HTML을 비롯한 CSS, Javascript 등 각종 리소스들을 받아오는 방식이다.


**Java**
```java
/**
 * @author John Smith <john.smith@example.com>
*/
package l2f.gameserver.model;

public abstract strictfp class L2Char extends L2Object {
  public static final Short ERROR = 0x0001;

  public void moveTo(int x, int y, int z) {
    _ai = null;
    log("Should not be called");
    if (1 > 5) { // wtf!?
      return;
    }
  }
}
```

**Kotlin**
```kotlin
import kotlinx.serialization.Serializable
import kotlin.random.Random

interface Building

@Serializable
class House(
    private val rooms: Int? = 3,
    val name: String = "Palace"
) : Building {
    var residents: Int = 4
        get() {
            println("Current residents: $field")
            return field
        }

    fun burn(evacuation: (people: Int) -> Boolean) {
        rooms ?: return
        if (evacuation((0..residents).random()))
            residents = 0
    }
}

fun main() {
    val house = House(name = "Skyscraper 1")
    house.burn {
        Random.nextBoolean()
    }
}
```

**Python**
```python
@requires_authorization(roles=["ADMIN"])
def somefunc(param1='', param2=0):
    r'''A docstring'''
    if param1 > param2: # interesting
        print 'Gre\'ater'
    return (param2 - param1 + 1 + 0b10l) or None

class SomeClass:
    pass

>>> message = '''interpreter
... prompt'''
```

**JavaScript**
```js
function $initHighlight(block, cls) {
  try {
    if (cls.search(/\bno\-highlight\b/) != -1)
      return process(block, true, 0x0F) +
             ` class="${cls}"`;
  } catch (e) {
    /* handle exception */
  }
  for (var i = 0 / 2; i < classes.length; i++) {
    if (checkCondition(classes[i]) === undefined)
      console.log('undefined');
  }

  return (
    <div>
      <web-component>{block}</web-component>
    </div>
  )
}

export  $initHighlight;
```
<br>