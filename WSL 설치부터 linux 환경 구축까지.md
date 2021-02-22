# WSL 설치부터 linux 환경 구축까지



## 01. wsl 설치



## 02. linux 환경 구축

- ubuntu 설치([일반, LTS 차이 설명](https://sosobaba.tistory.com/216))

  - https://corytips.tistory.com/185?category=658851
- https://github.com/kakao/khaiii/issues/96
  

  
- conda 설치(보통은 파이썬->conda-> jupyter 순서. 나는 conda->python)

  - https://davyk.tistory.com/34

  - https://myborn.tistory.com/7

  

  ```shell
  $ sudo apt-get update 
  $ sudo apt install python 
  $ python --version
  $ sudo apt install python3-pip
  ```
  
  
  
  ```shell
    $ wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
    $ bash Miniconda3-latest-Linux-x86_64.sh
    $ source ~/.bashrc #ubuntu 시작과 동시에 base 환경 자동 활성화
    $ conda --version
    $ conda update conda
    $ sudo apt install python3-pip 
    $ sudo pip3 install pip --upgrade
    $ pip3 install jupyter
  ```
  
    
  
- konlpy 설치

  - https://somjang.tistory.com/entry/UbuntuOpenJDK%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0

  - https://www.gitmemory.com/issue/kakao/khaiii/96/735773728

  - https://somjang.tistory.com/entry/PythonUbuntu%EC%97%90-mecab-ko-dic-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0?category=348828
  
  ```shell
  $ sudo apt-get update
  $ sudo apt-get install openjdk-8-jdk
  $ sudo apt-get install python3-dev; pip3 install konlpy
  $ sudo apt-get install curl
  $ bash <(curl -s https://raw.githubusercontent.com/konlpy/konlpy/master/scripts/mecab.sh)
  ```
  
  

- 참고

  https://brtech.tistory.com/123

