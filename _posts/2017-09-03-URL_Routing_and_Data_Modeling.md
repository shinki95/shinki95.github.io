---
layout:     post
title:      "HTML Form"
date:       2017-07-20 17:00:00
author:     "신윤기"
header-img: "img/post-bg-02.jpg"
---
# Django 모델링 기초
 첫 모임에 앞서 DB scheme, url routing을 공부해오기로 했다.


첫 번째 참고한 레퍼런스는 http://blog.hannal.com/2008/6/04_2-python_django_lecture/
였다.

1. Django에서 모델은 앱 단위로 존재하는데 이 모델을 DBMS에 연결하여 관리하는 체계 단위는 프로젝트이다.

2. DBMS란, 데이터의 집합을 만들고, 저장관리 및 기능을 제공하는 응용프로그램으로 인터페이스 제공, 관계표현, 백업 회복 등의 기능을 할 수 있다. 우리가 흔히 DB라 말하는 MYSQL, MariaDB, Postgresql, MongoDB 등이 그것들이다. 추후에 이에 대해 다룰 것이다.

3. 프로젝트 단위로 DBMS에 연결하기에 프로젝트 설정인 settings.py에 DBMS 접근 정보를 써넣는다. Django에서 Default로는 sqlite3가 설정되어 있다. 

4. Askdjango 강의에서 각 프로젝트가 하나의 엑셀문서를 담당하고, 모델들이 worksheet, 필드들이 테이블로 매칭된다고 했던 것을 기억하면 된다.

5. 기획한 단계에서의 모델의 원시 형태는 다음과 같다

>
```python
class Entries(models.Model):
    id = 0
    Title = ''
    Content = ''
    created = ''
    Category = 0
    Tags = ''
    Comments = 0
```

여기서 Category라는 개념을 살펴보자
하나의 글은 하나의 Category에 속하게 된다.
하나의 Category에는 여러 개의 글들이 속해 있다. 이는 **MANY TO ONE** 관계를 뜻한다.
이를 Django에서는 **ForeignKey**로 정의한다.

Tags의 경우에는 하나의 글이 여러 개의 Tags에 속해 있을 수 있고 하나의 Tags에 여러개의 글이 속하게 된다. 이는 **MANY TO MANY** 관계를 뜻한다. 이를 Django에서는 **ManyToManyField**로 정의한다.  
 이러한 ManyToMany의 관계의 경우 서로 연결 되는 두 필드들의 관계를 나타내는 새로운 테이블을 따로 관리한다.  

# 쇼핑몰 모델 구축하기 
위에서 살펴본 내용을 바탕으로 우리가 만들 쇼핑몰에 들어가야하는 모델을 생각해보자  
다음 레퍼런스를 참고했다  
*Setting up a Complete Django E-commerce store in 30 minutes*  
*Django by Example : Creating an Online Shop Project | packtpub.com*

1. Product Catalog
```python

class Category(models.Model):
    name = models.CharField(max_length=200)
    slug = models.SlugField(max_length=200)

    class Meta:
        ordering = ('name')
        verbose_name = 'category'
        verbose_name_plural = 'categories'

    def __str__(self):
        return self.name 

class Product(models.Model):
    category = models.ForeignKey(Category, related_name='products')
    name = models.Charfiled(max_length=255)
    slug = models.SlugField(max_length=150)
    image = models.ImageField(uplaod_to='products/%Y/%m/%d', blank=True)
    decription = models.TextField(blank=True)
    stock = models.PositiveIntegerField()
    description = models.TextField()
    available = models.BooleanField(default=True)
    created = models.DateTimeField(auto_now_add=True)
    updated = models.DateTimeField(auto_now=True)

    class Meta:
        ordering = ('-created',)
```




  *slug란 무엇인가?*

