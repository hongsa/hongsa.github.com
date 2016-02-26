---
layout: post
title: Django Settings
category : programming
---

### settings를 common, prod, dev로 나누어서 개발
- 이는 환경설정을 일반, 개발용, 제품용으로 쉽게 나눔
- 기본적으로 common에서 기본 소스가 있고 prod와 dev는 이것을 임포트한 후, 오버라이딩

```
from .common import *
```

### requirements.txt 를 통해 pip 관리
- reqs 폴더에 common, prod, dev로 나누어서 pip 관리
- txt 파일에 한줄씩 라이브러리 명 기록
- pip install -r common.txt 이런식으로 한번에 install 가능

```
pip install -r reqs/common.txt
```