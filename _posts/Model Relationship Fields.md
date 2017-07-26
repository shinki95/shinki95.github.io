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
user_id라는 필드가 생성이 됨!
외래키와 생성되는 필드명은 같으나 유일성에서 차이!
외래키는 한 명의 유저에게 여러 포스팅이 존재!
원투원은 한 명의 유저에게 한 개의 프로필만 존재!(query에 unique옵션이 추가가 됨)

## 접근

`comment.post` = `Post.objects.get(id=comment.post_id)`
comment의 외래키로 지정되어 있는 post 속성을 통해서 알 수도 있고
외래키 지정에 따라 생성된 post_id의 필드를 통해 Post에서 object를 가져오는 방법도 있다.

relation 되어 있는 해당필드를 호출할 때 query가 수행된다
항상 relation 불러오는 것이 아니라 lazy하게 불러온다!

## UserModel
장고에서는 기본으로 제공? 되는 user 모델을 바꿀 수 있는데(Abstract User등을 상속받아서) 그 바뀐 것이 settings에 반영되니
user의 변경으로 인한 오류를 막을 수 있다. 


## ForeignKey.on_delete
코멘트랑 포스트가 연결되어 있을 때 Post가 삭제되면 어떻게 될까?


## User field 만들었을 때
null이 아니니까 값을 지정하라고 할텐데
user_id에 어떠한 값을 채워넣을까를 물어보는 것
외래키 관계에서는 숫자로 지정해줘야 함.



## Related_name
1:N에서 1에서 N으로 접근할 때 
```python
post = Post.objects.first()
print(Comment.objects.filter(post=post)) # 방법1
print(post.comment_set.all()) # 방법2
comment.post
```

그런데 user랑 연결된 같은 이름의 모델이 다른 앱 내의 존재할 경우
user.post_set.all이라고 하면 user와 관계를 맺은 어떤 post가 호출되는 것인지 모른다!.
related_name을 설정하여 특정한 이름으로 호출하도록 할 수도 있고
아니면 '+'라고 설정하여 무조건
shop.models.Post.objects.filter(user=user)로만 호출되도록 할 수도 있다. 