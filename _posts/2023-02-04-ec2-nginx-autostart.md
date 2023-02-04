---
published: true
title:  "[AWS] Ubuntu ec2 재부팅 시 NginX 자동실행 설정하기(+그냥 끄고 켜기도 포함)"  
excerpt: ""

categories:
  - AWS
tags:
  - [AWS, EC2, NginX]

toc: true
toc_sticky: true
 
date: 2023-02-04 23:00:00
last_modified_at: 2023-02-04 23:00:00
---

## EC2를 재부팅 하면 NginX가 자동실행된다!  
AWS의 EC2(Ubuntu)에 NginX 한번 설치하면 EC2를 중지하고 새로 시작하면(설치 시부터, 혹은 재부팅, 재시동 등) NginX가 자동으로 실행되어 오히려 다른 서버로 80포트(NginX는 기본적으로 80포트 사용)를 실행하지 못할 때가 있다.  
그때 이걸 끄고 키는 법을 다루겠다.

<br>

## 개발 환경  

* AWS EC2  
* Ubuntu 22.04  
* NginX 1.18.0 (Ubuntu)  

<br>

## 정리  

### NginX 상태 확인  

* `systemctl status nginx.service`

```shell
# in Ubuntu EC2

systemctl status nginx.service

# 결과
nginx.service - A high performance web server and a reverse proxy server
Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
~~(기타)
```

<br>

`/lib/systemd/system/nginx.service; enabled)` 이 부분이 `enaled`이기 때문에 자동실행되는 것이다!

* `enabled` : 자동실행 On  
* `disabled` : 자동실행 Off  

<br>

### NginX 자동실행 설정  

* On : `sudo systemctl enable nginx.service`  
* Off : `sudo systemctl disable nginx.service`  

```shell
# 자동실행 On
sudo systemctl enable nginx.service

# 결과
Synchronizing state of nginx.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable nginx
Created symlink /etc/systemd/system/multi-user.target.wants/nginx.service → /lib/systemd/system/nginx.service.


# 자동실행 Off
sudo systemctl disable nginx.service

#결과
Synchronizing state of nginx.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install disable nginx
Removed /etc/systemd/system/multi-user.target.wants/nginx.service.
```

<br>

## 기타 - 그냥 NginX 끄기, 켜기  
* Off : `sudo service nginx stop`  
* On : `sudo service nginx start`  


## 기타 - 한마디  
NginX를 설치하는 순간부터 Express 서버를 80포트로 돌리려다 실패한 적도 있다 보니 이런 것도 잘 아는 게 중요하다 생각된다.  
사실 처음부터 뭔지는 알고, 혹은 다룰 줄 알고 설치했어야 했는데 항상 개념 부족을 느낀다...ㅠㅠ  

<br>

## 참고 문서  
[블로그 링크](https://blog.nachal.com/1682)


<br>
<br>