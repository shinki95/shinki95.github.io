---
layout:     post
title:      "Model Relationshop Fields"
date:       2017-07-20 17:00:00
author:     "신윤기"
header-img: "img/post-bg-02.jpg"
---

# Model Relationshop Fields #

> 정규화: 중복을 최소화 하는 프로세스

*항상 하는 것이 좋은 것은 아니다(query향상을 위해 안 할 때도 있음)*

## ForeignKey ##
Ex) 포스팅과 댓글
:ForeignKey 사용!
Comment worksheet에 맨 뒤에 post_id 컬럼이 있다고 생각하자!
기존에 있는 컬럼을 그대로 *외부*로 가져다 쓴다고 생각하면 될 것!

ForeignKey를 사용하게 되면 field명_id의 field가 생성이 된다!

## ManytoMany ##
Ex) 포스팅과 태그
:ManytoMany 사용!
name에 unique옵션(Tag에 같은 이름 쓰이지 않게 하도록!)

Relation 할 때 지정하는 모델 필드는
class 이름으로도 가능하지만 문자열로도 가능!
class로 지정하면 앞에 정의되어 있지 않으면 없다고 된다.
다른 앱에 있을 경우에는 'app이름.Tag'와 같은 방식으로 문자열 지정 가능

admin에 Tag 등록하고 나면 뜬다
Model가서 `__str__`지정해서 이름 뜨게 하는 것까지!

ManyToManyField는 
post 워크시트, tag워크시트 + 2개가 연결된 시트가 하나 더생김

ManyToManyField는 Post나 Tag 두 곳에 다 써도 되지만
Post에 쓰는 것이 권장!
Tag에 두게 되면 Tag가 Post에 강하게 엮이게 됨(`ManytoMayField('Post')`)
Tag를 만약 Post말고 다른 Article같은 모델에 적용시킬 수도 있기 때문에(활용성이 더 커짐)


## OnetoOneField ##
Ex) User와 Profie
Admin에서 Login 기능 바로 되었는데 그 이유는 login기능을 auth앱을 통해 지원하기 때문
account라는 앱을 생성


