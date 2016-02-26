---
layout: post
title: ionic에 facebook 로그인 달기
---



###django model
- 테이블을 user 테이블과 Facebook 테이블을 따로 만들고 외래키로 연결한다.
- 값이 날라오면 user 테이블에 들어갈 값으로 user row 생성하고 Facebook row로 생성
- user 칼럼에 소셜로 가입했는 지 boolean으로 저장
- 위의 칼럼값으로 로그인할 때 판단해서 처리

###djang view
- 그냥 requset.data 값을 알아서 나누어서 테이블에 저장하면됨
- token값을 생성해서 response에 담아서 보내줌

###ionic
- openfb, ngopenfb 라이브러리를 사용

```javascript
ngFB.init({appId: '고유번호', tokenStore: $window.localStorage, accessToken : $window.localStorage.fbAccessToken});
```

- ionic run할 때 선언하며, 내 appid와 localstorage에 저장하는 것을 명시해줘야 함
- 처음 로그인할 때 facebook token을 가져옴
- 토큰값을 로컬 스토리지에 저장되며, facebook token을 이용해서 다른 정보를 가져옴
- 가져온 정보를 서버에 보내서 저장함

```javascript
  var token = resp.data.token;
      var username = resp.data.username;
      var userid = resp.data.id;

      if (token && username) {
        $window.localStorage.token = token;
        $window.localStorage.username = username;
        $window.localStorage.userid = userid;
        deferred.resolve(true);
        $state.go('tab.slack');
      } else {
        deferred.reject('Invalid data received from server');
      }

```
###결론
- session 관련한 삽질을 한 후, 안보이던게 보임
- 어느정도나마 인증과, 소셜로그인의 흐름을 이해함