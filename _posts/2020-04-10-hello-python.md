---
layout: post
title:  python 기초 문법
date:   2020-04-10 10:06:20 +0900
categories: python
tags: python
---
* content
{:toc}

대학교 프로그래밍 입문언어라는 python에 대한 기본적은 내용 간략히 정리.
자세한 내용은 [공식 홈페이지의 레퍼런스](https://www.python.org/doc/) 참고하자.

## Python이란
> 파이썬은 1991년 프로그래머인 `귀도 반 로섬`이 발표한 고급 프로그래밍 언어로, `플랫폼에 독립적`이며 `인터프리터식`, `객체지향적`, `동적 타이핑 대화형 언어`이다.

## 설치
> macOS에는 기본적으로 설치되어 있으며 필요시 [공식 홈페이지](https://www.python.org/downloads/)에서 다운 받아 설치.

## 기초 문법
> 파이썬에서 `블록`은 `콜론(:)`으로 시작하여 동일한 `들여쓰기 구간`을 의미함
> 클래스나 함수 선언 조건문 반복문 등을 사용할때 콜론(:)과 들여쓰기 블록 구분

### 변수
> 자료형 없이 변수 선언
> 함수나 메서드 닽이 `블록`내에서는 `지역변수`로 선언되는데 변수명 앞에 `global`을 붙이면 전역변수가 된다.

```python
age = 20
name = 'song'

print(age) # 20 출력
print(name) #'song'출력
```
### 함수
> `def 함수명(파라미터):` 형태로 선언

```python
def add(a,b):  # 함수정의 끝에 : 을 입력해줘야한다.
    return a+b # 함수 안의 내용은 탭으로 띄워줘야한다. 안 띄우면 indented block 예외가 예외발샐

print(add(2,3)) #5출력
```
#### 람다

> `lambda 인자 : 표현식` 형태로 사용
>  파라미터로 익명함수 전달하는 용도같은로 보임 (개인적인 생각임)
```python
add = lambda x,y : x + y
add(3,5) # 8출력

(lambda x,y : x + y)(2,3) #5 출력 이렇게 즉시실행함수? 방식으로도 사용 가능.
```
### 조건문
#### if문
```python
a = 10
b = 5

if a > b:
    print('a > b')
elif a == b:
    print('a == b')
else:
    print('a < b'
```
### 반복문
#### while
```python
a = 10
while a <= 10:
    print(a)
    a = a + 1
```
#### for
```python
numlist = [1,2,3]
for num in numlist:
    print(num)
```

### 클래스
### 클래스 선언
```python
class Animal:
    def __init__(self, name, age): # 생성자
        self.name = name
        self.age = age
    
    def getName(self):  # 메소드 선언
        return self.name

ani = Animal('happy', 5)
ani.getName() # 'happy' 출력
```
### 상속
```python
class Animal:
    def __init__(self, name, age): # 생성자
        self.name = name
        self.age = age
    
    def getName(self):  # 메소드 선언
        return self.name

class Dog(Animal): # Animal 상속
    def speak(self):
        print('멍멍')

dog = new Dog('happy', 3)
dog.getName() # 'happy' 출력
dog.speak()  # '멍멍' 출력
```

### 모듈
#### 모듈 가져오기
```python
import 모듈  # 모듈.변수 or 모듈.함수 형태로 호출
from 모듈 import 변수 or 함수  # 필요한 변수나 함수만 가져오기
from 모듈 import * # 모듈의 모든 변수나 함수를 전부가져와서 모듈명 없이 사용가능하나 기존의 변수나 함수가 모듈의 것으로 덮어씌여질수 있음
del 모듈 # 모듈 지우기
reload(모듈) # 모듈 다시 불러오기
```
#### 많이 쓰이는 모듈
* sys
 * 파이썬 인터프리터를 제어
* os
  * 운영체제(OS : Operating System)를 제어

### 예외처리
```python
try:
    실행 코드
except [ 처리할 예외명 [ as 에러 메시지 변수 ]]:
    예외가 발생 했을 때 실행할 코드
[ else: ]
    예외가 발생 안했을 때 실행할 코드
[ finally: ]
    예외가 발생하든 안하든 실행할 코드
```
> 예제
```python
def division(a,b):
    res = 0
    try:
        res = a/b
    except:
        print('예외 발생')
    return res

division(2, 0) # '예외 발생' 출력
```