스프링 메이븐
=======================

목표 
-----------------------
- 메이븐과 빌드 툴은 이해한다.
- pom.xml 의존성 설정을 할 수 있다.

실습 
-----------------------
- 메이븐 설치
- STS에서 메이븐 프로젝트를 생성
- 메이븐 의존성 설정하여 사용하기

## 1. 메이븐(Maven)
: 메이븐은 프로젝트의 라이브러리 관리 및 의존성을 설정하며, 라이프 사이클을 관리하는 빌드 도구 툴 이다.

- 라이프 사이클(Life Cylcle)
: 메이븐에서는 미리 정의하고 있는 빌드 순서가 있으며, 이 순서를 라이프 사이클이라 한다. 라이프 사이클은 각 단계(Phase)별로 의존 관계를 가지고 있어 순서 대로 실행한다.

|Phase|설명|
|------|------|
|Clean|이전 빌드에서 생성 된 파일들을 삭제하는 단계|
|Validate|프로젝트가 올바른지 확인하고 필요한 모든 정보를 사용할 수 있는지 확인하는 단계|
|Complie|프로젝트의 소스코드를 컴파일하는 단계|
|Test|유닛(단위) 테스트를 수행 하는 단계(테스트 실패시 빌드 실패로 처리, 스킵 가능)|
|Package|실제 컴파일 된 소스 코드와 리소스들을 jar 등의 배포를 위한 패키지로 만드는 단계|
|Verify|통합 테스트 결과에 대한 검사를 실행하여 품질 기준을 충족하는지 확인하는 단계|
|Install|패키지를 로컬 저장소에 설치하는 단계|
|Site|프로젝트 문서를 생성하는 단계|
|Deploy|만들어진 package를 원격 저장소에 release 하는 단계|

- Phase와 Goal
: Phase는 메이븐의 빌드 라이프 사이클을 각각의 단계를 의미한다. 각각의 Phase는 의존관계를 가지고 있어 해당 Phase가 수행되려면 이전 단계의 Phase가 모두 수행되어야 한다. 각각의 Phase는 어떤 일을 할지 정의하지 않고 어떤 플러그의 Goal을 실행할지 설정한다.

2. POM - Project Object Model
: pom(pom.xml)은 메이븐 프로젝트의 기본 정보와 의존성 정보들을 담고 있는 파일이다. 

- 프로젝트 정보 : 프로젝트의 이름, 개발자 목록, 라이센스 등
- 빌드 설정 : 소스, 리소스, 라이프 사이클별 실행할 플러그인(Goal) 등 빌드와 관련된 설정
- 빌드 환경 : 사용자 환경 별로 달라질 수 있는 프로파일 정보
- POM 연관 정보 : 의존 프로젝트(모듈), 상위 프로젝트, 포함하고 있는 하위 모듈 등

1) pom.xml 구성
- Group Id : 네임스페이스이며 동일한 프로젝트라도 Group Id로 프로젝트를 구분
- Artifact Id : 프로젝트 이름이면서, 패키지 파일로 묶을 때 사용
- Version : Group Id와 Artiface Id가 동일한 프로젝트가 개발의 진척에 따라서 다른 내용임을 구분
- Packaging : 프로젝트 타입을 나타내는 정보로 자바 웹 프로젝트는 war, 일반 자바 프로젝트는 jar 로 설정, 이외에도 ejb, ear, pom 등의 타입 사용
- repositories : 의존성을 받아올 원격 메이븐 저장소, 사설 저장소도 사용 가능, 한 번 다운로드한 의존성 파일들은 원격 저장소가 아닌 로컬 저장소에 저장된 라이브러리를 참조
- properties : <키>값</키> 형태로 중복되는 값을 변수처럼 사용
- dependencies : 의존성 정의


2. 메이븐 설치 및 설정
- Window 
1) 메이븐 프로젝트 다운로드 : http://maven.apache.org/download.cgi
2) apache-maven-3.6.1-bin.zip 다운로드 후 압축 해제
3) 환경 변수 설정
  3-1) MAVEN_HOME : 압축해제 경로/apache-maven-3.6.1
  3-2) Path에 메이븐 변수 추가 : %MAVEN_HOME%/bin
4) cmd 창에서 메이븐 버전 확인
   mvn --version
   
- 실습 - 1
1) 메이븐 프로젝트 생성하기
* mvn archetype:generate
```console
D:\maven>mvn archetype:generate
[INFO] Scanning for projects...
[INFO]
[INFO] ------------------< org.apache.maven:standalone-pom >-------------------
[INFO] Building Maven Stub Project (No POM) 1
[INFO] --------------------------------[ pom ]---------------------------------

.... 생략 ...
Choose a number or apply filter (format: [groupId:]artifactId, case sensitive co
ntains): 1355: [엔터]
Choose org.apache.maven.archetypes:maven-archetype-quickstart version:
1: 1.0-alpha-1
2: 1.0-alpha-2
3: 1.0-alpha-3
4: 1.0-alpha-4
5: 1.0
6: 1.1
7: 1.3
8: 1.4
Choose a number: 8: [엔터]
Define value for property 'groupId': net.wds 
Define value for property 'artifactId': sample
Define value for property 'version' 1.0-SNAPSHOT: : [엔터]
Define value for property 'package' net.wds: : [엔터]
Confirm properties configuration:
groupId: net.wds
artifactId: sample
version: 1.0-SNAPSHOT
package: net.wds
 Y: : [엔터]

hetype-quickstart:1.4
[INFO] -------------------------------------------------------------------------
---
[INFO] Parameter: groupId, Value: net.wds
[INFO] Parameter: artifactId, Value: sample
[INFO] Parameter: version, Value: 1.0-SNAPSHOT
[INFO] Parameter: package, Value: net.wds
[INFO] Parameter: packageInPathFormat, Value: net/wds
[INFO] Parameter: package, Value: net.wds
[INFO] Parameter: version, Value: 1.0-SNAPSHOT
[INFO] Parameter: groupId, Value: net.wds
[INFO] Parameter: artifactId, Value: sample
[INFO] Project created from Archetype in dir: D:\maven\sample
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  02:58 min
[INFO] Finished at: 2019-05-03T14:46:58+09:00
[INFO] ------------------------------------------------------------------------


```

2) 자바 버전 수정
: pom.xml에서 자바 버전 수정
```xml
<plugin>
 <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-compiler-plugin</artifactId>
   <configuration>
    <source>1.8</source>
    <target>1.8</target>
    <encoding>UTF-8</encoding>
   </configuration>
 </plugin>
```

3) 컴파일 해보기
: mvn complie
+ class 파일 생성 확인 : target/classes
```console
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  4.189 s
[INFO] Finished at: 2019-05-03T14:54:57+09:00
[INFO] ------------------------------------------------------------------------
```

4) 테스트 확인
: mvn test
+ test 폴더 확인
```console
[INFO] -------------------------------------------------------
[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] Running net.wds.AppTest
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.023 s -
 in net.wds.AppTest
[INFO]
[INFO] Results:
[INFO]
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  2.423 s
[INFO] Finished at: 2019-05-03T15:14:59+09:00
[INFO] ------------------------------------------------------------------------
```

5) package 확인
: mvn package

```console
[INFO] -------------------------------------------------------
[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] Running net.wds.AppTest
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.025 s
 in net.wds.AppTest
[INFO]
[INFO] Results:
[INFO]
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0
[INFO]
[INFO]
[INFO] --- maven-jar-plugin:3.0.2:jar (default-jar) @ sample ---
[INFO] Building jar: D:\maven\sample\target\sample-1.0-SNAPSHOT.jar
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  2.268 s
[INFO] Finished at: 2019-05-03T15:16:38+09:00
[INFO] ------------------------------------------------------------------------
```

6) Dependency 설정
: pom.xml에 사용할 모듈 라이브러리 의존성 설정
```pom.xml
<dependency>
    <groupId>commons-dbcp</groupId>
    <artifactId>commons-dbcp</artifactId>
    <version>1.2.1</version>
</dependency> 
```

7) 
