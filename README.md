# VirtualBox에서 Vagrant 사용법 정리

## 설치

#### VirtualBox 설치
https://www.virtualbox.org/  
다운 및 설치

#### Vagrant 설치
https://www.vagrantup.com/downloads  
다운 및 설치

#### vagrant 초기 파일 생성
터미널 실행
```
C:\Users\WOOJAE>cd \
C:\HashiCorp>vagrant init
```

#### vagrant 설정 변경 (centos 설치를 위해)
C:\HashiCorp에 위치하는 Vagrantfile 파일에서  
15번째줄  
```
config.vm.box = "base" 
```
를
```
config.vm.box = "centos/7"
```
로 변경

마지막줄 #SHELL과 end 사이에 코드 추가
```
  config.vm.provider "virtualbox" do |v| 
	  v.memory = 4096 
	  v.cpus = 2
  end
```

이렇게 생김
```
... 생략
# SHELL
  config.vm.provider "virtualbox" do |v| 
	  v.memory = 4096 
	  v.cpus = 2
  end
end
```

#### vagrant 켜기
```
C:\HashiCorp>vagrant up
```
처음 실행인 경우 centcos가 자동으로 설치 됨


#### vagrant 가상머신 ssh로 접속
```
C:\HashiCorp>vagrant ssh
```

#### vagrant 종료
```
[vagrant@localhost ~]$ sudo shutdown -h now
```

<br/>

## 계정 추가 및 계정 이동

#### vagrant 실행
터미널 실행
```
C:\Users\WOOJAE>cd \
C:\HashiCorp>vagrant ssh
C:\HashiCorp>vagrant up
C:\HashiCorp>vagrant ssh
```

#### encore 계정 추가
```
[vagrant@localhost ~]$ adduser encore
[vagrant@localhost ~]$ sudo passwd encore
1234
```

#### encore 계정으로 이동
```
[encore@localhost ~]$ su encore
```

#### vagrant 계정으로 이동 (encore 계정 빠져나오기)
```
[encore@localhost ~]$ exit
[encore@localhost ~]$
```

## 파일 확인

#### 디렉토리(directory)에 있는 내용(디렉토리, 파일 등)을 확인
```
[vagrant@localhost ~]$ ls
```

#### 숨긴파일 포함 확인
```
[vagrant@localhost ~]$ ls -al
```

## 파일 생성 및 vi 편집기 열기, 권한 수정

#### a.txt 파일 vi 편집기에서 열기
```
[vagrant@localhost ~]$ vi a.txt
```

#### vi 내용 삽입
i 누르고 수정  
수정 완료 후 esc  
  
#### vi 저장 및 종료
esc -> :wq  


#### a.txt 권한 수정
```
[vagrant@localhost ~]$chmod 600 a.txt
[vagrant@localhost ~]$chmod 777 a.txt
```

<br/>

## 계정에 권한 부여

#### 가장 상위 폴더로 이동
```
[vagrant@localhost ~]$ cd /etc
```

#### sudo로 시작하는 파일 찾기
```
[vagrant@localhost etc]$ ls -al | grep sudo
```

#### sudoers 수정
```
[vagrant@localhost etc]$ sudo visudo
```

#### vi 편집기에 줄번호 표시
:set number

#### encore 계정에 권한 부여 코드 추가 
(101번째줄에 추가)
```
encore  ALL=(ALL)       ALL
```

#### vi 빠져나오기
esc -> :wq

<br/>

## 권한이 생긴 계정에서 파일 설치

#### encore 계정으로 이동
```
[vagrant@localhost etc]$ su encore
```

#### vim 설치
```
[encore@localhost etc]$ sudo yum install vim
```

#### yum update
```
[encore@localhost etc]$ sudo yum update
```

<br/>

## 미니콘다 설치

#### home 폴더로 이동
```
[encore@localhost etc]$ cd ~
```

#### wget 설치
```
[encore@localhost ~]$ sudo yum install wget
```

#### 미니콘다 설치파일 다운
```
[encore@localhost ~]$ wget wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

#### 미니콘다 설치파일 권한 수정
```
[encore@localhost ~]$ chmod 764 ./Miniconda3-latest-Linux-x86_64.sh
```

#### 미니콘다 설치파일 실행
```
[encore@localhost ~]$ ./Miniconda3-latest-Linux-x86_64.sh
```


#### 설치 과정 중 1
```
Please, press ENTER to continue
>>> 엔터누르기
```

#### 설치 과정 중 2
```
Do you accept the license terms? [yes|no]
[no] >>> yes 엔터
```

####설치 과정 중 3
```
Miniconda3 will now be installed into this location:
/home/encore/miniconda3

  - Press ENTER to confirm the location
  - Press CTRL-C to abort the installation
  - Or specify a different location below

[/home/encore/miniconda3] >>> 엔터
```

#### 설치 과정 중 4
```
Do you wish the installer to initialize Miniconda3
by running conda init? [yes|no]
[no] >>> yes 엔터
```

#### 설치 후 변경 된 설정값 적용
```
[encore@localhost ~]$ source ~/.bashrc
```

#### 미니콘다 python 실행
```
(base) [encore@localhost ~]$ python
```

### 미니콘다 python 종료
```
>>> exit()
```

### 리눅스 종료
```
(base) [encore@localhost ~]$ sudo shutdown -h now
```

