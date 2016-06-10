---
layout: post
title: queue and stack
category : algorithm
---

### 큐 - 선입선출
### 스택 - 후입선출
### 데크- 양쪽 끝에서 넣고 뺄 수 있음

- 연결리스트로는 쉽게 구현 가능
- 동적배열로는 바로 스택
- 큐와 데크는 head와 tail 변수에 위치를 저장
- 배열이 끝나면 앞으로 땡겨서 tail을 저장함, 이는 처음과 끝을 원형으로 붙이는 원리이며, 환형 버퍼라 함