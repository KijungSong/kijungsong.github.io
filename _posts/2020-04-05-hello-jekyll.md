---
layout: post
title:  "hello Jekyll"
date:   2020-04-05 01:59:06 +0900
categories: jekyll
tags: jekyll github
---
* content
{:toc}

## GitHub Pages 생성

> username.github.io 형태의 Repository를 생성



## Jekyll 설치 및 실행

> Ruby 2.4 이상 버전 필요 (ruby 2.7 사용)
>
> mac의 경우 Command Line Tools 설치 필요

```bash
$ xcode-select --install
```

#### 설치

```bash
$ gem install jekyll bundler
```

#### 생성 및 초기화

```bash
$ jekyll new ./
$ bundle install
```

#### 실행

```bash
$ bundle exec jekyll serve
```



###  테마 적용

[jekyll-theme](https://github.com/topics/jekyll-theme)에서 맘에 드는 테마를 적용 하면됨

* [적용 테마](https://github.com/Gaohaoyang/gaohaoyang.github.io/tree/theme)



### 편집 및 POST 하기

#### 편집 IDE

IDE들에 플러그인으로 markdown 플러그인들을 사용하여 편집을 실시간으로 볼수 있고

[Typora](https://typora.io/)와 같은 markdown 편집기를 사용해도 된다.

#### Post 작성

Post  작성 후 `_posts` 폴더에 아래 형식으로 저장하면 됨

> YEAR-MONTH-DAY-title.MARKUP

ex) `2020-04-05-hello-jekyll.md`

#### Post 올리기

 `_posts`에 추가 한 파일을 git에 push하면 끝.
 
 {% plantuml %}
 [First] - [Second]
 {% endplantuml %}