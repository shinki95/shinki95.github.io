---
layout:     post
title:      "Custom_Widget"
date:       2017-07-20 17:00:00
author:     "신윤기"
header-img: "img/post-bg-02.jpg"
---

1. project 폴더 밑에 widgets 만들고 init.py 파일 만들기
(`naver_map_point_widget.py`라는 python 파일이기에 init을 만들줘야함)

2. forms.py에서 widget 다시 설정!

3. admin에서는 widget이 안보인다.
admin에서는 model로부터 직접 modelform을 생성해서 쓰지 우리가 만든 form을 안쓴다(@admin.register확인하면 됨)

4. widget.py에 있는 html을 
widget.html로 옮기기(문자열을 따로 받아내자)
그렇다면 render을 써야하나?
render는 httpresponse의 인스턴스를 return
render to string을 통해 문자열을 반환해야함

5. settings을 가져올 때!
askdjango/settings.py로 가져오면 안된다. 
from django.conf import settings로 가져와야
django/conf/global_settings.py + askdjango/settings.py를 둘 다 가져옴

6. html에서 javascript선언
import할 때 clientID를 필히 지정할 것!

7. 만약 form field 다수에서 widget을 쓰고 싶다면
한 템플릿 안에서 id 는 unique해야함
따라서 각 필드 별 id를 따로 설정하는 것을 권장