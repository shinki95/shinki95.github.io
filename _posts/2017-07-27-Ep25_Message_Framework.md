---
layout:     post
title:      "Message_Framework"
date:       2017-07-20 17:00:00
author:     "신윤기"
header-img: "img/post-bg-02.jpg"
---

1. Message를 등록(view에서 저장되기 전에)
2. Message를 소비(template에서 주로 이루어짐), 최상위에 적용이 좋다!
3. message는 템플릿으로 안넘겨도 된다.
context processors.py 에 message가 있다 
request 인자를 받으면 사전을 받음
모든 템플릿에서 쓰는 변수 목록들을 매번 view에서 하나하나 지정하는 것이 아니라 자동으로 그 값이 지정이 되도록 하는 것!

