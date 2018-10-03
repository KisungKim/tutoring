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

### 자바 기본개념

예를 들어 요리를 한다고 가정합시다. 어떤 요리를 할지는 모르지만 요리를 할때에 분명 재료와 그 재료를 다듬고 요리하는 작업이 필요할 것 입니다 <br/>
요리를 할 때에 저희가 알아야 할 기본적인 정보는 (1)어떤 요리를, (2)무슨 재료로, (3)어떤 작업을 통해 만들겠다 라는 것입니다 <br/>
보통 객체는 다음과 같은 과정을 거쳐서 생성됩니다<br/>

(1) 어떤 요리를?

```java
class이름 인스턴스이름 = new class이름();
예를 들어.. 된장국을
Cooking duenjang = new Cooking();
이런식으로 만들어 줄 수 있습니다.
```

(2) 무슨재료로? 생각해 보면 어떤 요리든, 소금이 들어가지 않는 요리는 없습니다. 그럼 요리라는 클래스에는 항상 소금이 있어야 할 것입니다.<br/>

```java
int salt; // 'salt'라는 이름의 정수형 자료형(integer)이라는 의미입니다.
```

(3) 어떤 작업을? 마지막으로 요리가 만들어졌을 때, 요리가 완성되었다는 신호는 필요할 것입니다.<br/>

```java
public void finished() { System.out.println("요리가 완성되었습니다"); }
```

이 세가지의 개념만 가지고 있으면 이제 저희는 프로그램을 만들 수 있습니다.

<div>
<br/>리눅스 콘솔 명렁어<br/>
<code>pwd</code> : 현재 디레토리 위치<br/>
<code>ls</code> : 현재 디렉토리 위치에서 파일 목록 보기<br/>
<code>touch</code> : 빈 파일 생성<br/>
<code>cd</code> : 디렉토리 이동<br/>
<code>vim</code> : 파일 수정<br/>
</div>

아래는 현재 위치에서 javaTest_0926이라는 이름의 프로젝트 폴더를 만들고,<br/>
그 폴더 내부로 들어가 Cooking.java와 Main.java라는 빈 파일을 만들기까지의 과정입니다.<br/>

```
ubuntu1@ubuntu1-VirtualBox:~/java_tutoring$ pwd
/home/ubuntu1/java_tutoring
ubuntu1@ubuntu1-VirtualBox:~/java_tutoring$ mkdir javaTest_0926
ubuntu1@ubuntu1-VirtualBox:~/java_tutoring$ ls
javaTest_0922  javaTest_0926
ubuntu1@ubuntu1-VirtualBox:~/java_tutoring$ cd javaTest_0926
ubuntu1@ubuntu1-VirtualBox:~/java_tutoring/javaTest_0926$ ls
ubuntu1@ubuntu1-VirtualBox:~/java_tutoring/javaTest_0926$ touch Cooking.java
ubuntu1@ubuntu1-VirtualBox:~/java_tutoring/javaTest_0926$ touch Main.java
ubuntu1@ubuntu1-VirtualBox:~/java_tutoring/javaTest_0926$ ls
Cooking.java  Main.java
```

이제 빈 파일들을 만들었으니 위에설명처럼 파일을 자바 코드로 채워줘야 합니다. 다음과 같이 채워주시면 됩니다.

```java
// Cooking.java
package recipes;

public class Cooking {
  private int salt;
  public void finished() {
    System.out.println("finished!!");
  }
}
```

Main클래스는 다음과 같이 채워줍니다

```java
// Main.java
package recipes;

public class Main {
  public static void main(String args[]) {
    Cooking duenjang = new Cooking();
    duenjang.finished();
  }
}
```

이제 파일들을 만들었으니 위 파일들을 컴파일해줍니다.<br/>
javac명령어에서(javac) 패키지 컴파일 옵션을 주고(-d) 현재 디렉토리의(.) Cooking.java와 Main.java라는 파일을 (Cooking.java Main.java)
 컴파일해달라는 의미입니다.<br/>
코드에 오류가 없다면 새로 recipes라는 패키지가 생성된 것을 볼 수 있습니다.<br/>
이제 java명령어를 통해(java) 특정 패키지의(recipes.) 메인함수가 들어가있는 클래스를(Main) 실행시키면 다음과 같이 'finished'라는 메시지를 볼 수 있습니다

```
ubuntu1@ubuntu1-VirtualBox:~/java_tutoring/javaTest_0926$ javac -d . Cooking.java Main.java 
ubuntu1@ubuntu1-VirtualBox:~/java_tutoring/javaTest_0926$ ls
Cooking.java  Main.java  recipes
ubuntu1@ubuntu1-VirtualBox:~/java_tutoring/javaTest_0926$ java recipes.Main 
finished!!
```


