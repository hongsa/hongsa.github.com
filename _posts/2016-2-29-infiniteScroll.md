---
layout: post
title: Ionic infinite scroll
category : programming
---
###아이오닉에서 스크롤 통신 구현하기
- 템플릿에 ion-infinite-scroll 쓰기

```javascript
<ion-infinite-scroll on-infinite="loadMore()" distance="5%" ng-if="!noMoreItemsAvailable"></ion-infinite-scroll>
```
- loadMore 함수에서 서버와 통신하고, ng-if에서 불러올 것이 더이상 없는 지 체크
- controller 부분 함수 선언 및 팩토리 이용하기
- 불러올 때마다 기존 slacks와 concat으로 합치기

```javascript
$scope.slacks = [];
$scope.noMoreItemsAvailable =false;
var num = 0;
var AJAX_URL = "/주소";

 $scope.loadMore = function() {
    ListGet.ListMore(AJAX_URL, num).then(function(slacks){
      if(slacks === 404){
        $scope.noMoreItemsAvailable = true;
      }
      else{
        num += 1;
        $scope.slacks = $scope.slacks.concat(slacks);
        $scope.$broadcast('scroll.infiniteScrollComplete');
      }
    });
  };
 ```

 - factory 부분
 - 서버에서 404로 return 하면 더이상 불러올 값이 없음

 ```javascript
 ListMore: function(AJAX_URL, num){
      return $http.get(BASE_URL+ AJAX_URL+ num +'/').then(function(resp){
        lists = resp.data;
        return lists;
      },
      function(err) {
        lists = err.status;
        return lists;
      })
```


### refresh 부분도 동일한 구조로 이용할 수 있음

```javascript
$scope.doRefresh = function() {
    num = 0;
    $scope.noMoreItemsAvailable = false;
    ListGet.ListMore(AJAX_URL, num).then(function(slacks){
      num += 1;
      $scope.slacks = slacks;
      $scope.$broadcast('scroll.refreshComplete');
    });
  };
```










