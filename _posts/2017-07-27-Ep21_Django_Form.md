---
layout:     post
title:      "Django_Form"
date:       2017-07-20 17:00:00
author:     "신윤기"
header-img: "img/post-bg-02.jpg"
---
cleaned_data를 저장하는 방법

1.
```python
post = Post()
post.title = form.cleaned_data['title']
post.content = form.cleaned_data['content']
post.save()
```
2.
```python
post = Post.objects.create(**form.cleaned_data)
```
5
