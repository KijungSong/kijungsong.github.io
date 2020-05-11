---
layout: post
title:  "javascript 은닉화된 클로저 메서드의 테스트"
date:   2020-04-30 04:18:30 +0900
categories: javascript
tags: javascript test tdd
---
* content
{:toc}
> javascript에서 은닉화를 위해 클로저를 사용한다.
>
> typescript를 사용하면 손쉽게 적용 및 테스트가 가능하지만 Vanilla 스크립트로 작성시에는 테스트가 어려운 단점이 있다.
>
> 클로저를 테스트 하는 방법에 대한 개인적인 고민을 정리해 보았다.



자바스크립트 객체의 은닉화된 메서드들의 테스트 방법

아래와 같이 은닉화도니 메서드가 있다
```js
// Animal 클래스 정의
var Animal = function (name) {
    var name = name;
    
    var privateGetName = function() {
      return name
    }

    var getName = function() {
        return privateGetName();
    };

    return {
        getName
    }
}

var animal = Animal('good');
console.log(animal.getName());  // good
console.log(animal.privateGetName());  // Uncaught TypeError: animal.privateGetName is not a function
```

일반적인 방법으로는 테스트가 불가능하다. 은닉화를 쓰지 말고 네이밍으로 구분하여 서로 믿고 코딩 해야하는 건가라는 생각도 하며 이런 저런 방법을 생각한 결과 아래 방법을 쓰면 괜찮을거 같다.

```js
// Animal 클래스 정의
var Animal = function (name, isTestMode = false) {
    var res; 
    var name = name;
    
    var privateGetName = function() {
      return name
    }

    var getName = function() {
        return privateGetName();
    };
    
    res = {
        getName
    };
    
    // 테스트 모드일 경우에만 프라이빗 메서드를 추가해준다.
    if (window.isTestMode) {
        Object.assign(
            res,
            {
                privateGetName
            }
        )
    }
    return res;
}

var animal = Animal('good');
console.log(animal.getName());  // good
console.log(animal.privateGetName());  // good
```

여기서 좀 더 개선할 방법이 없을까..?

생각한 방법 중의 하나는 arguments를 사용하는 것이 아닌  window 전역 객체에 테스트 라이브러리가 존재 여부를 확인하는 방법이다.
또는 window에 `isTestMode`와 같은 약속된 변수를 추가하여 테스트 모드 여부를 판단하는 것도 좋아 보인다.

