---
layout: post
title:  "javascript ES5 class"
date:   2020-04-19 04:18:30 +0900
categories: javascript
tags: javascript es5 class object
---
* content
{:toc}
ES6부터는 `class 키워드`가 추가가 되면서 Java와 유사하게 Class를 선언하여 사용할 수 있게 되었지만 ES6 이전에도 `prototype 객체`를 사용하여 클래스와 유사하게 사용을 할 수 있다.
다만 자유도가 너무 있다보니 비슷(?)하면서도 다양한 방식으로 사용이 가능하다.
정답이 있진 않지만 그중에서 가장 보편적인 방법을 사용하는 것에 옳다고 본다. 하지만 다양한 사용 방식에 대해 이해를 하면 보다 효율적인 코딩이 되지 않을까 싶어 정리해본다.
> `스코프`와 `프로토타입`에 대한 이해는 javascript의 기초이다. 다만 다른 언어들과 차이점들이 있어 쉽게 잊혀지는 것 같다. 아래 내용이 햇갈린다면 복습이 필요하다.

## ES5에서의 클래스
### 클래스 선언
> 방법 1
> 생성자 함수를 통해 객체의 필드 값을 초기화 하고 prototype에 메서드를 정의

```js
var Animal = function (name) {
    this.name = name
}

Animal.prototype.getName = function() {
    return this.name;
}

var animal = new Animal('mung');
console.log(animal.getName());
```

> 방법 2
> 객체에 메서드를 추가하고 필드는 클로저로 구현하여 은닉화 하여 사용하는 방법

```js
var Animal = function (name) {
    var name = name;

    this.getName = function() {
        return name;
    };
}

var animal = new Animal('mung');
console.log(animal.getName());
```

> 방법 3
> 2번 방식이랑 유사(클로저를 사용하는 점에서) 하지만 new 키워드를 안쓰고 함수 호출의 리턴 값으로 객체를 리턴

```js
var Animal = function (name) {
    var name = name;

    var getName = function() {
        return name;
    };
    return {
        getName,
        test: this
    }
}

var animal = Animal('mung');
console.log(animal.getName());

/*
Animal 클래스는 return 값으로 객체를 리턴하기 때문에 결과물은 같긴하다.

생성자 함수의 return 값
 - 객체를 return 한다면, this 대신 객체가 반환됩니다.
 - 기본자료형을 return 한다면, return문이 무시되고 this가 리턴.
*/
var animal2 = new Animal('mung');
console.log(animal2.getName());
```

방법 1 vs 방법 2,3 의 가장 큰 차이는 `prototype 사용 여부`와 `은닉화`이다.
#### prototype 사용여부의 차이
`방법 1의 경우 정석적인? prototype을 통한 상속을 구현`하였다.
이를 통해 Dog 객첼르 100개 생성한다고 했을 `Animal의 메서드가 정의된 prototype 객체는 하나만 존재`하게 된다.
하지만 `2,3번의 경우는 생성할 때마다 this에 모든 메서드를 추가하고 있어 메서드들을 중복 생성`한다.
#### 은닉화란 
OOP에서는 내부 변수나 메서드들을 `은닉화`하여 외부에 숨기고 외부에서의 접근은 공개된 멤버나 메서드를 하여 제공을 한다.
javascript에서도 class의 키워드가 추가되면서 기존 OOP로 개발하던 사람들은 은닉화를 하기를 바란다.
하지만 javascript에서는 접근 한정자가 없으며 객체의 필드나 메서드들은 외부에서 자유롭게 접근이 가능하다.
이를 위해 변수나 메서드들의 네이밍을 통해 은닉화를 처리하거나 하는 등의 다양한 편법들이 나왔지만 그중 은닉화를 위한 가장 좋은 방법은 `클로저`를 사용하는 것이라고 생각한다.
하지만 `클로저를 통한 은닉화는 치명적인 단점`이 존재하는데 바로 테스트를 작성하기 어렵다는 것이다.
처음 javascript를 접했을 때에는 최대한 은닉화를 다른 사람들이 실수로 내부 변수 등을 조작을 못하도록 막는게 최선이라고 생각하여 은닉화에 중점을 두었지만 테스트 작성에 어려움으로 인하여 지금은 은닉화를 안 하고 대신 `탄탄한 테스트 코드를 작성하는 방향`으로 작성하길 선호하고 있다.
다만 레거시가 테스트가 어려운 코드의 경우 은닉화를 통해 강제성을 주는 것도 나쁘지 않다고 생각한다.
말이 샜는데 `위 방법 중에 1번 방법을 선호` 한다.
다면 요즘엔 ES6 작성 (class 키워드 사용)` 후 babel을 통해 transcompile을 하여 사용하므로 위 방법을 사용 할 일은 없어 보인다.

### 클래스 상속
방법 1이 가장 많이 쓰이는 방법이며 방법 2,3은 쓰이는 방법인가 싶다..
클래스 선언 방법으로 소개를 한 방법들에 대해 상속을 한다면 어떻게 할까 고민하면서 작성한 내용으로 아래와 같이 쓰이면 나름 상속은 구현이 될거 같다.

Animal 클래스를 상속받은 Dog 클래스를 예시로 든다.
> 방법 1의 상속

```js
// Animal 클래스 정의
var Animal = function (name) {
    this.name = name
}
Animal.prototype.getName = function() {
    return this.name;
}

// Dog 클래스 정의
var Dog = function (name, age) {
    Animal.call(this, name); // 부모 생성자 호출.
    this.age = age;
}
Dog.prototype = new Animal(); // 프로토 타입 프로퍼티에 부모 객체 설정
Dog.prototype.getAge = function() { // Dog 클래스 메서드 정의
    return this.age;
}


var dog = new Dog('mung', 5);
console.log(dog.getName());
console.log(dog.getAge());
```

> 방법 2의 상속

```js
// Animal 클래스 정의
var Animal = function (name) {
    var name = name;

    this.getName = function() {
        return name;
    };
}

// Dog 클래스 정의
var Dog = function (name, age) {
    Animal.call(this, name); // 부모 생성자 호출.

    var age = age;
    this.getAge = function() {
        return age;
    };
}

var dog = new Dog('mung', 5);
console.log(dog.getName());
console.log(dog.getAge());
```

> 방법 3의 상속

```js
var Animal = function (name) {
    var name = name;

    var getName = function() {
        return name;
    };
    return {
        getName
    }
}
// Dog 클래스 정의
var Dog = function (name, age) {
    var animal = Animal.call(this, name); // 부모 생성자 호출.

    var age = age;
    var getAge = function() {
        return age;
    }
    return Object.assign(
            animal,
            {
                getAge
            }
    );
}

var dog = Dog('mung', 5);
console.log(dog.getName());
console.log(dog.getAge());

// 클래스 선언의 방법 3 주석코드에 설명한 것처럼 new 키워드를 붙여도 결과 값은 같긴하다.
var dog2 = new Dog('mung2', 3);
console.log(dog2.getName());
console.log(dog2.getAge());
```

클래스 상속의 경우도 방법 1 vs 방법 2,3 의 가장 큰 차이는 `prototype 사용 여부`와 `은닉화`로 보면 될 거 같다.