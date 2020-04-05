---
layout: post
title:  "zsh - MacOS 재부팅시 ~/.bash_profile 미적용"
date: 2020-04-06 00:02:05 +0900
categories: jekyll
tags: macos zsh .bash_profile .zshrc
---
* content
{:toc}

### 이슈
MacOS에서 `zsh` shell을 사용하면 재부팅시 `.bash_profile`에 적용된 환경 변수가 적용이 안된다.
간단히 설명하자만 `zsh`는 기존 `~/.bash_profile`의 설정값을 따르지 않고 `~/.zshrc`의 설정을 따른다.

### 해결 방안
다양한 해결 방법이 있지만 하나만 적어보면,
`~/.zshrc`하단에 `source ./bash_profile`을 추가하면 된다.
