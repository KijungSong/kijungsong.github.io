---
layout: post
title:  "jekyll plantuml"
date: 2020-04-05 23:45:06 +0900
categories: jekyll
tags: jekyll uml plantuml
---
* content
{:toc}

[jekyll-plnatuml](https://github.com/yegor256/jekyll-plantuml) 플러그인 사용.

## 사전 준비
1. graphviz 설치
```bash
$brew install graphviz
```
2. palntuml 설치
```bash
$brew install palntuml
```

## jekyll-plnatuml 플러그인 설치
1. jekyll-plantuml install
```bash
$gem install jekyll-plantuml
```
2. `_config.yml`에 gems 배열에 `jekyll-plantuml` 추가
```yml
gems: [jekyll-paginate, jekyll-plantuml]
```
3. `GemFile`에 `gem "jekyll-plantuml"` 추가

## 샘플 코드 작성 후 실행
1. jekyll 실행
```bash
$jekyll s
```

## 이슈..
local에서는 정상 동작하지만 `github pages`에서 `jekyll-palntulm`을 지원을 안해서 빌드 실패가 된다.
우선 차선책으로 uml을 image로 올려서 사용 예정.