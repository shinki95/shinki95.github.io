---
layout:     post
title:      "Django Template Loader"
date:       2017-07-20 17:00:00
author:     "신윤기"
header-img: "img/post-bg-02.jpg"
---

# Django Template Loader
중요 Loader 2개
1. app_directories
2. filesystem
settings.py에서 `'APP_DIRS': True`이면 
APP directory에서 template를 찾음
`DIRS`는 프로젝트 전반의 template

template 디렉토리 밑에 앱 이름을 넣는 이유는
앱 이름은 프로젝트에서 겹칠 수 없음!
따라서 namespace개념으로 넣는 것!

템플릿은 꼭 html이 아니어도 됨. txt일 수도 있고
복잡한 문자열을 쉽게 해주는 것일뿐!

템플릿 엔진은 지정변수가 없다고 오류를 내지 않고 빈 문자열을 보여줌


