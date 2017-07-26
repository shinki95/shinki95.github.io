---
layout:     post
title:      "Django Template"
date:       2017-07-20 17:00:00
author:     "신윤기"
header-img: "img/post-bg-02.jpg"
---

# "Django Template" #
템플릿 상속을 위해서는 자식 템플릿 코드의 최상단에 반드시 이 코드를 작성할 것 
```
{% extends "부모템플릿경로" %}
```

자식템플릿은 부모템플릿이 설정한 block안에서만 재정의 가능


상속은 2단계로 하는 것을 추천!


프로젝트 layout
앱 별 layout

프로젝트 layout은 settings 있는 디렉토리에 만드는 것 추천
ex)
askdjango/askdjango/tempaltes/layout.html

프로젝트.layout >> 앱.layout >> 개별 템플릿

최상위 템플릿 만들고 나서는 settings.py에 설정해놓야함

```python
#settings.py
TEMPLATES =[
    'DIRS': [
        os.path.join(BASE_DIR, '프로젝트명', '최상위 템플릿 디렉토리)
    ]
]
