---
layout: post
title: Django api 서버 구축 삽질기
---

###결국 Function Based View 로 개발
- 일단 cbv로 하기에는 django에 익숙치 않기 때문에 결국 fbv로 결정
- 이미 익숙한 Flask와 굉장히 유사
- 내부 구조에 대한 정확한 이해가 부족하니, 디버깅하기가 굉장히 어려움
- 코드에 대한 가독성이 오히려 cbv가 떨어진다고 생각함, 개발자의 욕심이 아닐까?

###FBV로 개발하니 생각보다 빨리 개발가능
- 여러가지 삽질끝에 fbv로 개발하니 생각보다 빠르게 개발이 가능
- 코드도 꽤나 깔끔
- restframework의 serializer, Response, api_view, status 정도 사용

```
from rest_framework.response import Response
from rest_framework.decorators import api_view
from rest_framework import status
from rest_framework import serializers
```

###Restframework를 사용했으나 restful 하지 않음
- 내가 생각하는 기준선에서 최대한 깔끔하게(응답코드 신경쓰기)
- 완벽한 restful을 억지로 맞추는 것이 더욱 부담스럽다는 판단
- cbv에 익숙해진 후, restful에 맞추는 것이 낫다는 판단

