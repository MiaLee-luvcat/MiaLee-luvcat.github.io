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
last_modified_at: 2022-02-27 10:36:00
---

# 면접 질문과 답을 정리하는 글을 써보고자 하는데

## 태그가 잘 정리되는지부터 확인해보자.


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