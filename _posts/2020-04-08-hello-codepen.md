---
layout: post
title:  "Jekyll에 codepen 첨부하기"
date:   2020-04-08 11:09:20 +0900
categories: etc
tags: codepen javascript css html
---
* content
{:toc}
## codepen 회원가입
* https://codepen.io/
  * 저는 [Log In with GitHub](https://codepen.io/auth/github)으로 로그인

* 코드 생성
  * 코드 작성 후 저장

## Jeykll 설정
### _includes/codepen.html 추가
> codepen.html
{% raw %}
```html
{% assign username = include.username %}
{% unless username %}
{% assign username = site.codepen_username %}
{% endunless %}
<p data-height="228" data-theme-id="0" data-slug-hash="{{ include.hash }}" data-default-tab="result" data-user="{{ username }}" class='codepen'>See the Pen <a href='https://codepen.io/{{ username }}/pen/{{ include.hash }}/'>{{ include.title }}</a> by {{ username }} (<a href='https://codepen.io/{{ username }}'>@{{ username }}</a>) on <a href='https://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>
```
{% endraw %}
### _config.yml에 codepen 계정 추가
```yaml
codepen_username: username
```

## 포스팅 작성
> 포스팅애 아래 처럼 추가하면 된다.
{% raw %}
``` html
{% include codepen.html hash="zYvOave" title="Enyo Template" %}
```
{% endraw %}
* `hash`: cdepen hash값
  * codepen 링크는 아래와 같은 형태로 구성
    * https://codepen.io/{{ username }}/pen/{{ hash }}
    * codepen의 `exrport`나 크를 카피하면 hash값을 알수 있다.
* `title`: 적당한 제목 입력.

### 샘플
{% include codepen.html hash="zYvOave" title="Hello Codepen" %}