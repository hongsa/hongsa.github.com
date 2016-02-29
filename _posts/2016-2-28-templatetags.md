---
layout: post
title: Django TemplateTags 사용하기
category : programming
---

###디렉토리 구성
- app - templatetags - custom_tags.py
- 요일마다 색깔 바꾸는 것을 태그로 이용해봄 
- middleware에 로컬 추가

```python
'django.middleware.locale.LocaleMiddleware',
```

```python
from django import template
register = template.Library()

@register.filter(name = 'date_color')
def data_color(val):
if val == u'월요일':
val = DEFAULT_COLOR

elif val == u'화요일':
val = CHANGE_COLOR

elif val == u'수요일':
val = DEFAULT_COLOR

elif val == u'목요일':
val = CHANGE_COLOR

elif val == u'금요일':
val = DEFAULT_COLOR

elif val == u'토요일':
val = CHANGE_COLOR
else:
val = SUNDAY
return val

```

- 템플릿에서 사용하기

```
진자 문법 사용함(마크다운에서 에러남..)
load custom_tags
데이터 값| date_color
```
