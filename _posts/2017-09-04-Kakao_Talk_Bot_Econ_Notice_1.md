---
layout:     post
title:      "HTML Form"
date:       2017-07-20 17:00:00
author:     "신윤기"
header-img: "img/post-bg-02.jpg"
---
# Django 모델링 기초
# 카카오톡 경제학부 공지봇 만들기 #

파이썬 공부 및 개인적 필요를 위해 카카오톡을 이용한 공지봇 만들기에 도전했다.

기획한 내용은 다음과 같다.

1. 경제학부 공지페이지의 글 및 링크를 크롤링
2. 카카오톡에서 아무 메세지나 입력하면 글 및 링크를 알려줌



이를 위한 개발은 크게 3단계로 구분된다.

1. 공지페이지 크롤링하기
2. 옐로우 페이지 API 적용
3. 서버 배포하기



## 공지페이지 크롤링하기

*Askdjango 웹크롤링 강의 중 "네이버 웹툰 목록 크롤링하기"를 참고했다.*

`python manage.py startproject econ_notice`

`python manage.py createapp bots`



```python
#econ_notice/bots/functions.py

import json
from bs4 import BeautifulSoup
import requests
from urllib.parse import urljoin

def notice_search():
    list_url = "http://econ.snu.ac.kr/announcement/notice"
    response = requests.get("http://econ.snu.ac.kr/announcement/notice")
    response.encoding=None
    for tag in soup.select('tr > td.title.left'):
        tag_a = tag.find('a')
        link = urljoin(list_url, tag_a['href'])
        title = tag_a.text
        print(title, link)
```



위와 같은 코드를 통해 공지목록을 크롤링 할 수 있다. 