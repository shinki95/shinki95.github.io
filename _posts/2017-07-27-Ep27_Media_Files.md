---
layout:     post
title:      "Media_Files"
date:       2017-07-20 17:00:00
author:     "신윤기"
header-img: "img/post-bg-02.jpg"
---
1. static이랑 똑같이 설정 진행하는데
ImageField 사용 시에느 pillow를 꼭 설치할 것

2. media는 static과 달리 개발서버에서 지원을 안해줌!
따라서 urlpatterns에 추가해야 함!

```python
#askdjango/urls.py
from django.conf import settings
from django.conf.urls.static import static

urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT) #-> static으로 시작하면! settings.MEDIA_URL로 연결하고 MEDIA_ROOT에 있는 파일들을 보여주겠다

```

