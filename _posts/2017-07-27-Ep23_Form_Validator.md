---
layout:     post
title:      "Django_Model_Form"
date:       2017-07-20 17:00:00
author:     "신윤기"
header-img: "img/post-bg-02.jpg"
---
1. modelform 을 사용하면 field 변경 시 form field를 번거롭게 수정하지 않아도 된다

2. commit False를 언제 사용하는가?
```python
if form.is_valid():
    post = form.save()
    post.ip = request.META('REMOTE_ADDR')
    post.save()
```
이렇게 하면 post를 저장하고 ip 추가해 다시 저장하는 꼴이 되니까 위에는 `post = form.save(commit=False)`로 하고 한 번만 저장하는 것이 좋다!!!


3. Form을 끝까지 써주세요!
* form은 내부적으로 값을 변경할 수 있다!
request.POST로 접근하면 request.POST가 form에서 변경되었을 수도 있다. 따라서
form.is_valid를 통과했을 때는 raw data를 가져올 것이 아니라
`form.cleaned_data`로 호출해서 가져올 것을 추천!

4. post_edit만들기

