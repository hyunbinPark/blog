---
title: "Google Cloud Platform에 있는  인스턴스 mysql에 Remote Connection"
date: 2019-04-29 16:46:25 -0400
categories: setting
---


Mysql 에 원격접속을 하려면 
	
	1. 방화벽에서 mysql에 접근하는 tcp 3306  포트를 열어준다.

	2. Mysql conf 파일에서 
    
         16.0 버전 이하이면 vi /etc/mysql/my.cnf
		
         16.0버전 이상 vi /etc/mysql/mysql.conf.d/mysqld.cnf)


*변경 전*
```
# Instead of skip-networking the default is now to listen only on
# localhost which is more compatible and is not less secure.
bind-address            = 127.0.0.1
```

*변경 후*
```
#bind-address            = 127.0.0.1 
Or
bind-address.         = 0.0.0.0
```

-> 로컬에서만 mysql 접속가능하게 하던 부분을 -> 모든 아이피에서 접근할수 있도록 수정

*Mysql 재시작*

```
service mysql restart
```

```
netstat -antp | grep mysql
tcp        0      0 0.0.0.0:3306            0.0.0.0:*               LISTEN      3432/mysqld
```

이런 식으로 tcp 3306 포트의 모든 아이피 접속이 가능해졌다는 것을 확인해볼 수있다.


*계정의 특정아이피 접근 권한 설정*

```
GRANT all ON DBname.*  TO ‘user’@‘ip’;
```
```
Flush privileges;
```

*GCP방화벽 setting*

google cloud platform 에 들어가서 vpc network -> firewalls rules ->

새로운 규칙으로 모든 아이피(0.0.0.0/0) 의 tcp 3306 포트를 열어주는 규칙을 만들고 tag 를 생성한다. 

그리고 내가 적용 시키고자 하는 instance의 수정에 들어가서 network 아래 tag 로 입력한 후 

다시 detail을 통해 잘 적용 되었는 지 확인한다.

방화벽이 잘 열렸는지 확인 ->

```
nmap -p [port num] [IP address] 를 통해 확인한다.
```

이 모든게 완료 되었으면

```
Mysql -h[IP address] -u [user] -p [password] 
```

를 통해 원격 접속이 가능해진다. 


*GCP SETTING 참고*
[link]https://brunch.co.kr/@smalljiny/3

*에러시 참고* 
[link]https://zetawiki.com/wiki/ERROR_2003_(HY000):_Can%27t_connect_to_MySQL_server_on