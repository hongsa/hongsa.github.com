---
layout: post
title: Nginx Log & Fluentd
category : programming
---
### Fluentd 설치 순서 ( ex: Nginx log를 elasticsearch 로 보내기)
- td-agent 설치 (공식 홈페이지 참고)
- 원하는 플러그인 설치 

```
/usr/bin/td-agent-gem install <plugin name>
```

-  /etc/init.d.td-agent 에서 변경

```
TD_AGENT_USER = root
TD_AGENT_GRUOP = td-agent
```

- 변경해야지 access log를 가져올 수 있는 권한 획득
- /etc/td-agent/td-agent.config 에서 맞게 설정
- /etc/init.d/td-agent start하면 시작

### Nginx Log Format 수정
- nginx의 default log format에는 request time이 없음
- 따라서 /etc/nginx/nginx.conf 파일에서 log format을 원하는 값을 추가해야 함

```
log_format main '$remote_addr - $remote_user [$time_local] "$request" '
                        '$status $body_bytes_sent "$http_referer" '
                        '"$http_user_agent" $request_time ';

        access_log /var/log/nginx/access.log main;
        error_log /var/log/nginx/error.log;
```

### Fluentd Log Format 수정 
- 이에 맞게 fluented도 로그포맷을 받을 수 있게 정규표현식으로 수정
- error log도 마찬가지로 수정
- fluentd custom log format 정규표현식 테스트 사이트 
- http://fluentular.herokuapp.com/

```
<source>
  type tail
  path /var/log/nginx/access.log #...or where you placed your Apache access log
  pos_file /var/log/td-agent/nginx-access.log.pos
  tag nginx.access #fluentd tag!
  time_format %d/%b/%Y:%H:%M:%S %z
  format /^(?<remote_addr>[^ ]*) - (?<remote_user>[^ ]*) \[(?<time>[^\]]*)\]\s+"(?<request_type>[^ ]*) (?<request_url>[^ ]*) (?<request_http_protocol>[^ ]*)" (?<status>[^"]*) (?<body_bytes_sent>[^ ]*) "(?<http_referer>[^"]*)" "(?<http_user_agent>[^"]*)" (?<request_time>[^ ]*)/
</source>
```

```
<match nginx.access>
  type elasticsearch
  buffer_type file
  buffer_path /var/log/td-agent/buffer/nginx-access
  retry_limit 50
  flush_interval 30s
  logstash_format true
  logstash_dateformat %Y.%m # defaults to "%Y.%m.%d"
  logstash_prefix nginx-log
  hosts 주소
  port 포트
  index_name nginx-stg-access
  type_name nginx-stg-access
</match>

```


