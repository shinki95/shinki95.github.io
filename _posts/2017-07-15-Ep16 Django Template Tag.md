---
layout:     post
title:      "Django Template Tag"
date:       2017-07-20 17:00:00
author:     "신윤기"
header-img: "img/post-bg-02.jpg"
---

# Django Template Tag #
1. {% extend "base.html" %}
"base.html"이 positional,keyword 인자를 넘기는 것이라 생각
```python
def mysum(x,y):
    return x + y
#위치기반
mysum(1,2)

#키워드기반
mysnum(x=1,y=2)
```
장고 템플릿에서는 {}와 ""로 인자를 넘긴다

2. example
people['Tom'] >> {{ people.Tom }}
person.say_hello() >> {{ person.sayhello }}

템플릿 엔진에서는 다 {{ . }}으로 접근한다!

3. Django Template Tag
{% %}로 쓰인다!
템플릿 주석에서 한 줄 주석은
{# #}으로 쓰면 된다!

주석에서 HTML이나 JavaScript 주석을 쓰면 안된다!
서버에서 다 작동한 다음에 보이는 것만 막는 것
불필요한 렌더링이 생김!

4. {% csrf_token %} 항상 쓸 것!
빈 폼을 줄 때 token값을 함께 준다!
따라서 포스트 요청이 들어올 때 그 token 값이 함께 있으면
받아들임!

5. if changed
어떠한 부분이 변경되었는지를 판단
```python
{% for date in days %}
    {% ifchanged %}<h3>{{ date|date: "F" }}</h3>{% endifchanged %}
{% endfor %}
# 변수 값으로 판단
{% for date in days %}
    {% ifchanged date.date %}
        {{ date.date }}
    {% endifchanged %}
    {% ifchanged date.hour date.date %}
        {{ date.hour }}
    {% endifchagned %}
{% endfor %}
```

# Django Template Filter
`{{ var|filter3:인자|filter4 }}`
이와 같을 경우
var가 첫 번째 인자
인자가 두 번째 인자로 filter3에 들어가고
이것을 다 통과한 값이 filter4에 들어감


