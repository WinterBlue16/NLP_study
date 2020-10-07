# 자연어 처리를 위한 Docker:whale:

전반적인 도커 설치는 [이 페이지](https://steemit.com/kr/@mystarlight/docker)를 참고했다. 로컬 운영체제는 window 10 Home, 64bit이다.

## 1. Docker Toolbox 설치

> window 10 Home 버전 이하의 운영체제를 사용할 경우, Docker For Windows가 아니라 Docker Toolbox를 사용한다.

### 1.1 가상화 옵션 사용으로 변경

> BIOS에 들어가 가상화 옵션을 '사용'으로 변경

### 1.2 Docker Toolbox 다운로드 및 설치

> [docker github](https://github.com/docker/toolbox/releases)에서 파일을 다운로드할 수 있다. 가장 최신 버전은 19.03.1이다. 



## 2. 이미지 및 컨테이너 생성

### 2.1 이미지 다운로드

> ubuntu 16.04 기준

```shell
$ docker run ubuntu:16.04 /bin/bash # ubuntu 16.04 image 다운로드
$ docker images # 전체 이미지 조회
```



### 2.2 컨테이너 실행 및 생성

```shell
$ docker run -it ubuntu:16.04 # docker container 생성
$ docker ps # 실행 중인 container 조회
$ docker ps -a # 전체 container 조회
```



## 3. wiki.wp2txt 파일 생성하기

### 3.1 wikipedia 데이터 다운로드

```shell
$ apt-get update
$ apt-get update; apt-get install curl # curl: command not found 메시지 방지
$ curl https://dumps.wikimedia.org/kowiki/latest/kowiki-latest-pages-articles.xml.bz2 -o kowiki-latest-pages-articles.xml.bz2
```

### 3.2 ruby 설치

### 3.3 xml 파일 txt로 변환 

### 3.4 wp2txt 파일로 저장



