---
layout: post
title: "Maven Plugin"
subtitle: "About Maven Plugin"
background: "/background.jpg"
---

# Maven Plugin  

***

## 배경지식  
XML, Maven

***

## Maven Plugin ?  
Apache Maven(이하 Maven)은 Java 진영에서 많이 사용되는 빌드 도구이며 플러그인을 실행시키는 프레임워크이다.  
또한 모든 작업은 플러그인에서 수행한다.  
플러그인은 빌드 단계, 리포트 단계에서 실행될 수 있다.  
플러그인은 하나 이상의 Goal(명령, 작업)을 가지고 있고 여러 Goal의 조합으로 구성된다.  
여러 Goal을 묶어서 Phase(작업 단계)라고 말하기도 한다.  

빌드 플러그인은 pom.xml 파일에 `<build></build>` 엘리먼트에 작성된다.  
리포트 플러그인은 pom.xml 파일에 `<reporting></reporting>` 엘리먼트에 작성된다.  

Maven은 프로젝트의 빌드를 위해 빌드 라이프사이클(Build Lifecycle)을 정의하였다.  
Default, Clean, Site 3가지의 표준을 정의하였으며 라이프사이클은 여러 페이즈들을 일련의 순서로 실행하는 것을 의미한다.  
빌드 라이프사이클의 주요 페이즈의 순서는 아래와 같다.  
![Maven Build Lifecycle]({{site.url}}/images/2018-11-21-Maven-Build-Lifecycle.PNG)

현재 목표로 하고 있는 프로젝트는 Spring + React 구조이며 Maven으로 빌드 시 Webpack 빌드도 수행되어야 한다.  
이러한 구조의 프로젝트 설정을 아래에서 설명한다.  

***

## Maven and NPM  
Maven과 NPM을 연계하여 사용하고 싶을 경우 플러그인을 통해 실행하는 방법이 있다.  
Reference Front-End Maven Plugin 링크를 열어보면 Github로 연결되는데, Maven으로 작성된 NPM 연동 플러그인이다.  
해당 플러그인을 사용하면 NPM 설치, Grunt, Gulp, Webpack 등 빌드나 번들링 관련 패키지를 실행할 수 있다.  

Spring + React 형태의 프로젝트를 구성하고 싶었기 때문에 아래와 같이 설정하였다.  
Spring에서 제공하는 Boilerplate [React.js and Spring Data REST](https://spring.io/guides/tutorials/react-and-spring-data-rest/) 프로젝트의 설정 값을 가져와서 사용하고 있다.  
```xml
<plugin>
<groupId>com.github.eirslett</groupId>
<artifactId>frontend-maven-plugin</artifactId>
<version>1.6</version>
<configuration>
    <installDirectory>target</installDirectory>
</configuration>
<executions>
    <execution>
        <id>install node and npm</id>
        <goals>
            <goal>install-node-and-npm</goal>
        </goals>
        <configuration>
            <nodeVersion>v10.11.0</nodeVersion>
            <npmVersion>6.4.1</npmVersion>
        </configuration>
    </execution>
    <execution>
        <id>npm install</id>
        <goals>
            <goal>npm</goal>
        </goals>
        <configuration>
            <arguments>install</arguments>
        </configuration>
    </execution>
    <execution>
        <id>webpack build</id>
        <goals>
            <goal>webpack</goal>
        </goals>
    </execution>
</executions>
</plugin>
```

***

## Reference  
1. [Apache Maven Plugins](https://maven.apache.org/plugins/)  
2. [Apache Maven Build Lifecycle](https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html)  
3. [Front-End Maven Plugin](https://github.com/eirslett/frontend-maven-plugin)  

***
