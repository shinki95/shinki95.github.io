---
layout:     post
title:      "URL Reverse"
date:       2017-07-20 17:00:00
author:     "신윤기"
header-img: "img/post-bg-02.jpg"
---

# URL Reverse 
Url 패턴이 변경되어도 거기서 호출되는 함수는 변하지 않는다!
따라서 함수로부터 거꾸로 url 패턴을 계산해내자!

```python
#urls.py
url(r'^(?P<id>\d+)/$', views.post_detail, name='post_detail'),

#post_detail.html
<<<<<<< HEAD
=======
# <a href="{% url "post_detail" post.id %}">
>>>>>>> refs/remotes/origin/gh-pages
```

## <a href="{% url "post_detail" post.id %}">
name을 지정하면 그 뷰함수를 만드는 url로 연결시키고 id를 인자로 받으니 post.id를 넘겨준다.


url name이 같을 수 있으니 
include할 때 namespace를 'blog'와 같이 지정
include에 대한 namespace를 지정!

이렇게 namespace를 지정한 이후에는 템플릿에서
{% url "namespace: name" %}이런 식으로 지정해야 함.


```python
reverse('blog:post_list')
reverse('blog:post_detail', args=[10])
reverse('blog:post_detail', kwargs={'id' :10})
```
reverse의 경우에는 이와 같이 쓰면 되는데
resolve_url은 이보다 간단하다

```python
from django.shortcuts import resolve_url
resolve_url('blog:post_list')
resolve_url('blog:post_detail', 10)
resolve_url('blog:post_detail', id=10)
```


*내부적으로 reserve함수를 수행*


뜬금없이
`reverse('/hello/')`를 넣으면 예외가 발생하지만
`resolve_url('/hello/')`를 넣으면 `'/hello/'`를 리턴해준다.


redirect는 내부적으로 resolve_url을 수행

## 최상위 url에서 redirect 설정

```python
#askdjango/urls.py
def root(request):
    return redirect('blog:post_list')

urlpatterns = [
    url(r'^$', root, name='root')
]
```
와 같이 지정

이러면 http 302응답이 와서 post_list로 연결이 된다!

혹은 
`url(r'^$', lambda r: redirect('blog:post_list), name='root'),`
와 같이 쓸 수도 있다.

*(따로 view함수를 구현할 필요없이 redirect함수만 만드는 것이므로)*


**get_absolute_url 구현**

```python
post = Post.objects.first()
reverse('blog:post_detail', args=[post.id]) 

#혹은
resolve_url('blog:post_detail',post.id)
```

이렇게 일일히 접근해야했는데
model에서 
```python
def get_absolute_url(self):
        return reverse('blog:post_detail',args=[self.id])
```
이와 같이 정의내리면 한번에 접근 가능하다!

`resolve_url(post)`로도 가능
해당 post인스턴스의 디테일을 볼 수 있는 url을 연결!  
*인스턴스를 통해 해결하자!*



