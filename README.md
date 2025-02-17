
# LambdaTest Maven Tunnel
[![Maven Health Check](https://github.com/LambdaTest/lambdatest-maven-tunnel/actions/workflows/healthCheck.yml/badge.svg)](https://github.com/LambdaTest/lambdatest-maven-tunnel/actions/workflows/healthCheck.yml)
![LambdaTest Logo](https://www.lambdatest.com/static/images/logo.svg)

---

### Prerequisites
1. Maven is required to be installed:
   https://maven.apache.org/install.html

### Environment Setup
1. Global Dependencies
    * Install [Java8](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
2. Lambdatest Credentials
    * Set LambdaTest username and access key in environment variables. It can be obtained from [LambdaTest dashboard](https://automation.lambdatest.com/)    
    example:
    - For linux/mac
    ```
    export LT_USERNAME="YOUR_USERNAME"
    export LT_ACCESS_KEY="YOUR ACCESS KEY"
    
    ```
    - For Windows
    ```
    set LT_USERNAME="YOUR_USERNAME"
    set LT_ACCESS_KEY="YOUR ACCESS KEY"
    
    ```
3. Add following dependency to your POM.xml file
```xml
<dependency>
    <groupId>com.github.lambdatest</groupId>
	  <artifactId>lambdatest-tunnel-binary</artifactId>
    <version>1.0.4</version>
</dependency>
```
## Example

```java
import com.lambdatest.tunnel.Tunnel;

# creates an instance of Tunnel
Tunnel t = new Tunnel();

# replace <lambdatest-username>,<lambdatest-accesskey> with your username and key. You can also set an environment variable - "LT_USERNAME" and "LT_ACCESS_KEY".
HashMap<String, String> tunnelArgs = new HashMap<String, String>();
tunnelArgs.put("user", "<lambdatest-username>");
tunnelArgs.put("key", "<lambdatest-accesskey>");

# starts the tunnel instance with the required arguments
t.start(tunnelArgs);

# stops the tunnel instance
t.stop();
```
## Arguments

Apart from the username and access key, all other lambdatest tunnel parameters are optional.

#### Change Tunnel Name
```java
tunnelArgs.put("tunnelName","YourName");
```
#### Change pid path
```java
tunnelArgs.put("pidFile","Your/pid/path");
```
#### Change directory path
```java
tunnelArgs.put("dir","give/lambda/directory/path");
```
#### Change tunnel.log path
```java
tunnelArgs.put("logFile","give/tunnel/log/directory/path");
```
For full list of tunnel parameters, please refer tunnel parameters documentation file.

### Advice/Troubleshooting
1. It may be useful to use a Java IDE such as IntelliJ or Eclipse to help troubleshoot potential issues. 

## About LambdaTest
[LambdaTest](https://www.lambdatest.com/) is a cloud based selenium grid infrastructure that can help you run automated cross browser compatibility tests on 2000+ different browser and operating system environments. LambdaTest supports all programming languages and frameworks that are supported with Selenium, and have easy integrations with all popular CI/CD platforms. It's a perfect solution to bring your [selenium automation testing](https://www.lambdatest.com/selenium-automation) to cloud based infrastructure that not only helps you increase your test coverage over multiple desktop and mobile browsers, but also allows you to cut down your test execution time by running tests on parallel.

### Steps to publish
1. Create a Ticket in OSSRH for new release using "support@lambdatest.com" credential.. Wait for approval.
   Example:https://issues.sonatype.org/browse/OSSRH-66845
2. Validate approval by login into https://oss.sonatype.org/#welcome using "support@lambdatest.com" credential.
3. Generating gpg passphrase
```java
gpg --gen-key
``` 
4. Place below content after replacing PASSWORD with "support@lambdatest.com"`s password and PASSPHRASE with your gpg passphrase into ~/.m2/settings.xml file.
```java
<settings>
  <servers>
    <server>
      <id>ossrh</id>
      <username>Lambdatest</username>
      <password>PASSWORD</password>
    </server>
  </servers>
  <profiles>
    <profile>
      <id>ossrh</id>
      <activation>
        <activeByDefault>true</activeByDefault>
<settings>
      </activation>
      <properties>
        <gpg.executable>gpg</gpg.executable>
        <gpg.passphrase>PASSPHRASE</gpg.passphrase>
      </properties>
    </profile>
  </profiles>
</settings>
```
5. Go inside lambdatest-mavan-tunnel and execute below command to deploy newer version to nexus repository manager.
```java
mvn clean deploy
```
6. After successfull deploy to nexus repository manager. Your central maven repository will be in sync with new version after few hours.(In my case took almost 2 days)
