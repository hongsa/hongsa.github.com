---
layout: post
title: 재밌어이웹툰
category : portfolio
---

### 웹툰 리뷰 앱 (Android, Ios - 2017.10 출시)

![_config.yml]({{ site.baseurl }}/images/webtoonreview.jpg)

##### 0. 개발 및 운영
- 2017.07 ~ 2017.10(개발 기간)
- 2017.10 ~ (운영 중)

##### 1. 타겟 사용자
- 재밌는 웹툰을 찾는 웹툰 하드 유저
- 여러 웹툰 플랫폼을 모아서 보길 원하는 유저


##### 2. 해결하고자 하는 문제점
- 대부분의 웹툰 평점은 9.9x여서 선택에 대한 기준이 되지 못한다.
- 댓글은 각 회차에 대한 댓글일 뿐 전체 웹툰에 대한 리뷰가 없다.
- 다운로드 100만 이상의 웹툰 플랫폼만 해도 약 10개정도가 있을 정도로 상당히 많은 웹툰이 존재한다.


##### 3. 솔루션
- 리뷰를 통해 웹툰 선택에 대한 기준을 제시한다.
- 다양한 웹툰 플랫폼을 하나로 모아 앱 내에서 바로 볼 수 있도록 한다.


##### 4. 서비스 링크
- [안드로이드](https://goo.gl/cnYgNB)
- [아이폰](https://goo.gl/tka3S6)
- [프론트엔드 Git Repository](https://github.com/hongsa/review-frontend) / 코드 일부


##### 5. 리뷰를 선택한 이유
- 야동 추천 서비스를 운영했을 경우, 추천보다는 리뷰에 좀 더 사용자가 반응함을 경험했다.
- 취향 기반으로 추천해주어도, 다시 리뷰를 보고 선택한다고 생각했다.
- 협업 필터링(collaborative filtering)을 통해 추천을 해준다면, 늘 접하는 장르만의 작품만 추천되는 맹점이 있다고 생각했다.


##### 6. 서비스 설계 및 특징
  - Front-end
    - React-Native를 통해 안드로이드와 아이폰 모두 개발
    - Redux, Redux-thunk를 이용해 data state 관리
    - ESLint를 사용하여 코드퀄리티 관리
    - [프론트엔드 Git Repository](https://github.com/hongsa/review-frontend) / 코드 일부
  - Back-end
    - Python Flask Restful api로 개발
    - Flask-SQLAlchemy를 기본 orm으로 사용하며, join이 있을 경우 raw query 사용
    - Json Web Token - 사용자 인증
    - AWS SQS - 좋아요 버튼에 사용
    - Push - One Signal [http://onesignal.com]
  - Crawl
    - Python - requests, beautifulsoup4, selenium
    - 기본적으로 requests를 통해 크롤링이 가능한 경우, requests + bs4로 크롤링
    - requests를 통해 가져오지 못할 경우, selenium을 사용해 크롤링
    - 총 9개의 웹툰 플랫폼 크롤링(네이버, 다음, 카카오, 레진코믹스, 탑툰, 투믹스, 배틀코믹스, 코미카, 코미코)
  - Infra
    - AWS EC2 - Ubuntu 16.04.2
    - AWS RDS - Maria DB
    - Storage - AWS S3
    - Image CDN - CloudFlare(무료여서 사용)
    - Google analytics
