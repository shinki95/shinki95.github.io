---
layout:     post
title:      "User_Authentication_2"
date:       2017-07-20 17:00:00
author:     "신윤기"
header-img: "img/post-bg-02.jpg"
---
.gitignore에 들어갈 것
db.sqlite3
__pycache__
media
.vscode

accounts앱에서는 절대 namespace를 쓰지 않는다
auth.user를 가져다 쓰기 때문!

password는 field로 받는 것이 아니라 .setpassword()로 받아야 한다
```python
<form action="" method="post">
    {% csrf_token %}
    <table>
        {{ form.as_table }}
    </table>
    
</form>
```
form에 항상 들어가야함!
템플릿에서 로그인 처리할 때!

{% if not user.is_authenticated %}
(인증이 되어 있지 않다면!)


login 하고 다음 페이지 연결시키고 싶을 때
(request도 context에 있어서 모든 template에 항상 넘어감)
`<li><a href="{% url "login" %}?next={{ request.path }}">로그인</a></li>`