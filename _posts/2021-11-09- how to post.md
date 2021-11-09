---
title: '[github blog] how to post'
description: 로컬에서 github blog에 포스팅 하는 방법
categories: 
  - github blog
tags: [github blog, posting]
toc : true
# author_profile: false
---

> 이 글은 [테디노트 유튜브](https://youtu.be/--MMmHbSH9k)의 깃헙(Github) 블로그 만들기 시리즈를 따라하면서 정리한 글입니다.

# Github blog 포스팅 방법



## 준비물

1. typora - 마크다운 파일이 웹에서 어떻게 보이는지 바로 시각적으로 보여주기 때문에, 쓰고 고치는  것이 편리함.
2. github desktop 
3. visual studio code



## 방법 (포스팅 방법)

1. github desktop에서 github.io 레포지토리(깃헙 블로그 레포)를 clone 한다.
2. 로컬 환경에 clone 한 github.io 레포지토리 폴더를 visual studio code에서 연다.
3. `_config.yml` 등 코드를 수정하고 저장하는 경우, visual studio code를 이용한다.
4. 블로그에 글을 포스팅하는 경우, typora를 사용한다.
   1. typora를 열어 로컬에 clone한 github.io 폴더를 연다.
   2. `_posts` 폴더에 `yyyy-mm-dd 제목.md` 이름의 파일을 추가해서 `yaml(글 제목, 카테고리 설정) + 마크다운(글 내용) 형식`으로 글을 작성한다. 
   3. 저장! 
5. github desktop에 들어가보면 변경된 사항이 있다고 알림이 떠있을 것.
6. 이 때 commit 내용을 입력하고 `commit`을 누른다.
7. commit 후 `push origin`을 누르면 github 레포지토리에 커밋사항이 등록되고
8. 조금만 기다리면 github blog에 내가 포스팅한 글이 올라온다.

