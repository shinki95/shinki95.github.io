---
layout:     post
title:      "Static_Files"
date:       2017-07-20 17:00:00
author:     "신윤기"
header-img: "img/post-bg-02.jpg"
---
1. load static 템플릿 상단에 써주고
2. { href=static }이렇게 써줄 것
3.
```python
#settings.py 
STATIC_URL = '/static/'
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'askdjango', 'static')
]
```
4. url같은데에 static 없는데 어떻게 view에서 보여주는 것이지?
settings.DEBUG = True로 지원받고 있는 것
실제로는 따로 static server를 둠!

5. /static/ -> settings.STATIC_URL
 http://localhost:8000/static/style.css => style.css => askdjango/static/style.css

 http://localhost:8000/static/blog/style.css => blog/style.css => blog/static/blog/style.css

 static 파일이 있을 후보 디렉토리 목록
 1) blog/static/blog/style.css => settings.STATIC_ROOT/blog/style.css
 2) askdjango/static/style.css => settings.STATIC_ROOT/style.css

6. 
`STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')`
이거 써주고 
`python manage.py collect statifiles` 실행