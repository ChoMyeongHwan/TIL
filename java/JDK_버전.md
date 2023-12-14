# JDK 버전 전환하기

## 1. Java 버전 다운로드

먼저, Java 11과 Java 17을 모두 컴퓨터에 설치하여야 한다.

- [Java 11 다운로드](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)
- [Java 17 다운로드](https://www.oracle.com/java/technologies/javase-jdk17-downloads.html)

다운로드 후, 각각의 JDK를 설치하고, 설치된 경로를 확인하여 기록해두자.

## 2. 환경 변수 설정

다음으로, 윈도우의 환경 변수 설정을 통해 Java 버전을 쉽게 변경할 수 있도록 준비하자.

- '제어판' > '시스템 및 보안' > '시스템' > '고급 시스템 설정'을 클릭
- '환경 변수' 버튼을 클릭하여 시스템 변수에 'JAVA_HOME'이라는 새 변수를 추가
- 'JAVA_HOME' 변수의 값으로 JDK 11이 설치된 경로를 입력

이렇게 하면 기본적으로 JDK 11이 시스템의 Java 버전으로 설정된다.

## 3. 버전 변경 방법

Java 17로 버전을 변경하고 싶을 때는 다음의 단계를 따르면 된다.

- '환경 변수' 설정으로 다시 들어가 'JAVA_HOME' 변수의 값을 JDK 17이 설치된 경로로 변경하자.

이제 시스템의 Java 버전은 JDK 17로 설정되었다.

## 4. 인텔리제이에서의 버전 변경

인텔리제이에서는 프로젝트 별로 사용하는 Java 버전을 따로 설정할 수 있다.

- 'File' > 'Project Structure'를 클릭
- 'Project' 탭에서 'Project SDK'를 원하는 Java 버전으로 설정

이렇게 하면 인텔리제이에서는 선택한 버전의 Java를 사용하게 된다.

## 5. 버전 확인 방법

현재 시스템에서 사용하는 Java 버전을 확인하는 방법을 알아보자.

- '명령 프롬프트'를 열고 'java -version'을 입력하면 현재 시스템의 Java 버전을 확인할 수 있다.
- 인텔리제이에서는 'Help' > 'About'을 클릭하여 현재 사용하는 Java 버전을 확인할 수 있다.

## 6. JDK 버전 전환 도구

### 6.1 리눅스에서의 JDK 버전 관리 - SDKMAN

리눅스에서는 SDKMAN을 사용하여 JDK 버전을 관리할 수 있다.

SDKMAN 설치:

```bash
curl -s "https://get.sdkman.io" | bash
```

설치 확인:

```bash
sdk version
```

JDK 설치:

```bash
sdk install java 11.0.3-open
sdk install java 17.0.1-open
```

JDK 버전 전환:

```bash
sdk use java 11.0.3-open
sdk use java 17.0.1-open
```

### 6.2 윈도우에서의 JDK 버전 관리 - jEnv

윈도우에서는 jEnv를 사용하여 JDK 버전을 관리할 수 있다. 

jEnv 설치:

- [jEnv 다운로드](https://www.jenv.be/)

jEnv를 사용하여 JDK 버전을 관리하는 방법에 대해서는 아래의 링크를 참고하자.

- [Windows에서 여러 JDK(Java) 간 전환하는 방법](https://ichi.pro/ko/windowseseo-yeoleo-jdk-java-gan-e-jeonhwanhaneun-bangbeob-188808991195692)

## 7. 추가 참고 자료

여러 JDK 버전을 관리하고 전환하는 방법에 대한 추가적인 정보는 아래의 블로그 링크에서 얻을 수 있다.

- [컴퓨터 과학 학생 블로그](https://computer-science-student.tistory.com/467)
