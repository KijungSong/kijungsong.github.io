---
layout: post
title:  "Javascript 단위 테스트(Unit Test) (jasmine, jest)"
date:   2020-04-15 23:47:06 +0900
categories: test
tags: javascript test tdd jasmine karma jest
---
* content
{:toc}

## 테스트 코드의 필요성
개발을 하다보면 요구사항들이 바뀌는 일이 빈번하다. 기존 코드에 대한 검증 및 새로운 코드에 의한 사이드이펙트에 대한 걱정은 많은 시간을 소요시킬 뿐이 아니라 이는 적지 않은 정신력을 소모하게 만든다.
이러한 문제들을 대해서 은탄환이 될 수 있는 것이 바로 테스트 코드이다.
탄탄한 테스트 코드는 그 자체로 스펙이 되며 스펙의 변화에 애자일하게 대응할 수 있으며 새로운 코드에 대한 확신을가질 수 있게 도와준다.
javascript에도 다양한 테스트 라이브러리가 존재하며 그중 `jasmine`과 `jest`에 대해서 간략하게 정리해보았다.

## 테스트의 종류
### 단위 테스트
단위 테스트(Unit Test)란 가장 최소단위의 테스트로 보통 모듈 단위로 테스트를 한다.
### 통합 테스트
통합 테스트(Integration Test)란 단위 테스트 보다 넓은 범위의 테스트로 보통 2개 이상의 모듈을 연결한 상태로 진행하는 테스트를 말함
### E2E 테스트
E2E 테스트(End To End Test) 종단(Endpoint) 간 테스트로 사용자 입장에서 하는 테스트를 말함 UI(User Inerface) 테스트라고 불리기도한다.


## 테스트 더블
> 단위 테스트 패턴으로, 테스트하기 곤란한 컴포넌트를 대체하여 테스트하는 것
> 특정한 동작을 흉내만 낼 뿐이지만 테스트 하기에는 적합하다.
> 다음 가지를 통칭하여 테스트 더블이라고 함

* **더미(dummy):** 파라미터로 사용되며 실제 사용되지는 않는다.
* **스텁(sturb)**: 더미를 개선하여 실제 동작하게끔 만든 것. 리턴값을 하드 코딩한다
* **스파이(spy)**: 스텁과 유사. 내부적으로 기록을 남기는 추가 기능. 특정 메서드가 호출되었는지 등의 상황을 감시한다.
* **페이크(fake)**: 스텁에서 발전한 실제 코드. 운영에서는 사용할수 없음
* **목(mock)**: 더미, 스텁, 스파이를 혼합한 형태

## 테스트 프레임워크
> 테스트를 모듈을 가져오기 위해 `ES6 문법을 사용하기 위해서는 babel 설정이 필요` 여기서는 다루지 않음.

### jasmine

> [공식 페이지](https://jasmine.github.io/)
> * 브라우저 실행 환경의 프레임워크
>   * 테스트 러너로 karma를 사용
>   * 공홈에서 확인해보니 nodejs 실행 환경에서도 실행 가능.

#### JASMINE 시작하기 - NODE.JS 환경
Add Jasmine to your package.json
```bash
npm install --save-dev jasmine
```

Initialize Jasmine in your project
```bash
npx jasmine init
```

Set jasmine as your test script in your package.json
```json
{
  "scripts": {
    "test": "jasmine"
  }
}
```

Run your tests
```bash
npm run test
```

#### 테스크 코드 구조
개인적으로 아래와 같은 형태로 테스트를 구성하는 것을 선호한다

기본 테스트 파일명: `*[sS]pec.js`

```js
describe('A모듈 테스트', () => {

    beforeEach(() => {
        // 각 테스트 전에 실행
    });
    
    afterEach(() => {
        // 각 테스트 이후에 실행
    });
    
    describe('A모듈.a메서드 테스트', () => {
        it('a메서드 테스트 1', () => {
            // ...
        });
    
        it('a메서드 테스트 2', () => {
            // ...
        };
    })
});
```

### jest
> [공식 페이지](https://jestjs.io/)
> * 페이스북에서 만든 테스트 프레임워크
> * nodejs 실행 환경의 테스트 프레임워크
> * 테스트러너를 포함한 프레임워크로 별도의 테스트러너가 없어도 된다.

#### JSET 시작하기 - NODE.JS 환경
Add Jest to your package.json
```bash
npm install --save-dev jest
```

Set jest as your test script in your package.json
```json
{
  "scripts": {
    "test": "jest"
  }
}
```

Run your tests
```bash
npm run test
```

#### 테스크 코드 구조
개인적으로 아래와 같은 형태로 테스트를 구성하는 것을 선호한다
jasmine과 동일하게 구성 가능하며 `it` 메서드 대신 `test`를 사용해도 된다.

기본 테스트 파일명: `*.test.js`

```js
describe('A모듈 테스트', () => {

    beforeEach(() => {
        // 각 테스트 전에 실행
    });
    
    afterEach(() => {
        // 각 테스트 이후에 실행
    });
    
    describe('A모듈.a메서드 테스트', () => {
        it('a메서드 테스트 1', () => {
            // ...
        });
    
        it('a메서드 테스트 2', () => {
            // ...
        };
    })
});
```