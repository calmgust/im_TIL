# Mongo DB



## 1. 설치

mac os에서 설치

`$ brew install mongodb`



서버 실행 전에 데이터가 저장될 폴더를 생성

`$ sudo mkdir -p /data/db`

Password: [macOS 계정 비밀번호 입력]



권한 생성

`$ sudo mongod`

Password: [macOS 계정 비밀번호 입력]

`$ brew services start mongodb`

`$ mongo`

`> use admin`

`> db.createUse({user:'이름', pwd:'비밀번호', roles:['root']})`

***비밀번호는 기억하고 있어야***



`$ brew services stop mongodb`

`$ vim /usr/local/mongod.conf`

밑에 두 줄 추가

```
...
security:
	authorization: enabled
```



mongod를 실행하고 접속

`$ brew services start mongodb`

`$ mongo admin -u [이름] -p [비밀번호]`





