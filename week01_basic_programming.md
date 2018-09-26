---
layout: default
title: "SSH통신으로 첫 자바 프로젝트 생성하기"
---

> SSH통신으로 우분투 환경에서 첫 자바 프로젝트 생성하기

## SSH통신

<br/>
제 경우는 MacOS를 활용했으며 리눅스 4.14.27(kernel), ubuntu 16.04를 사용했습니다
<br/>
가상머신은 Oracle VM virtualbox를 사용했습니다.
<br/>
먼저 virtualbox의 네트워크 환경설정은 (어댑터1)NAT, (어댑터2)bridge으로 설정했습니다.
<br/>
이후 우분투에서 ctrl + alt + t를 통해 터미널을 열어주고 <code>sudo apt-get install ssh</code>의 명령어를 통해 ssh통신을 위한 모듈을 설치해줍니다.
<br/>
이제 <code>ifconfig</code>명령어를 통해 현재 연결된 네트워크의 inet address를 확인합니다. ex 192.xxx.xxx.xxx
<br/>
이제 맥 환경(윈도우의 경우 다른 툴을 사용할 수 있습니다)에서 터미널을 열어준 후 <code>ssh [우분투이름]@[inet address]</code>를 통해 우분투에 접속해줍니다.
<br/>
예를 들어, ubuntu1@192.168.0.0 이런식으로 적어주시면 됩니다. 아래처럼 되면 연결이 성공된 것입니다.
```
Last login: Wed Sep 26 16:22:08 on ttys001
gimgiseong-ui-MacBook-Pro:tutoring kisung$ ssh ubuntu1@[inet address] 
ubuntu1@[inet address]'s password: 
Welcome to Ubuntu 16.04.4 LTS (GNU/Linux 4.14.27 x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

패키지 169개를  업데이트할 수 있습니다.
0 업데이트는 보안 업데이트입니다.

새 배포판 '18.04.1 LTS'을(를) 사용할 수 있습니다.
업그레이드를 하시려면 'do-release-upgrade' 명령을 실행하세요.

*** 시스템을 다시 시작해야 합니다 ***
Last login: Mon Sep 24 12:10:44 2018 from [inet address]
ubuntu1@ubuntu1-VirtualBox:~$ 

```

## jdk설치

> sudo, apt-get, default-jdk 만 기억하시면 됩니다.

1. sudo apt-get update : 패키징툴인 apt-get을 관리자권한으로 update한다는 의미입니다.
2. sudo apt-get install default-jdk : java develop kit를 본인 우분투에 설치한다는 의미입니다.
설치가 완료되었다면 다음을 확인할 수 있습니다.
```
ubuntu1@ubuntu1-VirtualBox:~$ java -version
openjdk version "1.8.0_181"
OpenJDK Runtime Environment (build 1.8.0_181-8u181-b13-0ubuntu0.16.04.1-b13)
OpenJDK 64-Bit Server VM (build 25.181-b13, mixed mode)
ubuntu1@ubuntu1-VirtualBox:~$ 
```

## 자바 프로젝트 생성

> .java파일(들) -> 명령어를 통해 패키지로 묶어주기 -> 묶어준 패키지의 실행 클래스 파일을 실행
보통 이클립스에서 자바프로젝트를 생성해주면 자동으로 소스폴더 밑에 package가 생성됩니다.
<br/>
이클립스를 사용하지 않는다면 본인이 프로젝트로 만들 폴더를 만들고 그 안에 자바 파일을 만들어주면 됩니다. 
<br/>
예를 들어서..
```java
package test0922;

public class MainClass {
  public static void main(String args[]) { 
    System.out.println("Hello JAVA!!");
    new TestClass().showMessage();

  }
}
```
