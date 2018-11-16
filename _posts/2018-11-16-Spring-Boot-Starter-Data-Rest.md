---
layout: post
title: "Spring-Boot-Starter-Data-Rest"
subtitle: "About Spring-Boot-Starter-Data-Rest"
background: "/background.jpg"
---

# Spring Boot Starter Data Rest

***

### Spring Boot Starter Data Rest  
Spring Boot에서는 쉽고 간편하게 의존성을 관리할 수 있는 Starter를 제공하고 있다.  
이번에 소개하려고 하는 spring-boot-starter-data-rest도 Starter 중 하나이다.  
Spring Boot로 웹 어플리케이션을 만들 때 매번 같은 작업을 반복하게 되고 비슷한 의존성을 가지게 된다.  
이러한 매번 동일한 소스코드나 의존성을 관리해주고 쉽게 사용할 수 있게 만들어져있다.  
또한 REST API를 노출하기 위해 단순히 CRUD를 HTTP Method에 매칭되는 것만 아니라 RESTful하게 구성되어 있다.  
>makes it easy to build hypermedia-driven REST web services on top of Spring Data repositories  

***

### Features 
공식 문서에 나온 대표적인 기능에 대해 알아보도록 한다.  
1. Exposes collection, item and association resources representing your model.  
: 저장소(Repository)에 있는 리소스를 Rest API로 노출한다.  
모든 리소스를 노출하지만 원하면 커스터마이징을 통해 노출을 하지 않는 것도 가능하다.  
2. Supports pagination via navigational links.  
: 링크를 통해 RESTful한 서비스를 만들 수 있다.  
REST 규칙 중에서 HATEOAS는 굉장히 중요한 부분이다.  
요청에 대한 응답에 링크(_links)를 통해 클라이언트는 동적으로 상호작용이 가능해진다.  
[Spring REST HATEOAS 문서](https://spring.io/guides/gs/rest-hateoas/)를 통해 자세한 내용을 확인하도록 하자.  

[Spring Data Rest 문서](https://spring.io/projects/spring-data-rest#overview)를 통해 내용을 이해하도록 하자.  

***

### Quick Start

1. Project 생성.  
: [Spring Initializr](https://start.spring.io/) 혹은 IDE를 통해 프로젝트를 생성한다.  
2. 의존성 추가.  
: pom.xml 파일에 spring-boot-starter-data-rest 의존성을 추가한다.  
jpa와 h2 의존성은 테스트를 위해 메모리 데이터베이스를 사용하기 위해 추가한다.  
```
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.0.5.RELEASE</version>
</parent>

<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-rest</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>com.h2database</groupId>
        <artifactId>h2</artifactId>
        <scope>runtime</scope>
    </dependency>
</dependencies>
```
3. Spring Boot로 어플리케이션을 구성.  
: @SpringBootApplication 어노테이션을 사용하여 어플리케이션 실행 환경을 만든다.  
```
@SpringBootApplication
public class DataRestDemoApplication {
	
	public static void main(String[] args) {
		SpringApplication.run(DataRestDemoApplication.class, args);
	}
}
```
4. JDO 구현.  
: JDO(Java Data Object)를 구현한다.  
Lombok을 사용하거나 직접 구현 한다.  
Eclipse를 사용중이라면 우클릭 메뉴에서 Source-Generate Getters and Setters 기능을 이용하자.  
```
@Entity
public class Person {
	private @Id @GeneratedValue Long id;
	private String name;
	private Long age;
	
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public Long getAge() {
		return age;
	}
	public void setAge(Long age) {
		this.age = age;
	}
	
	Person() {}
	
	Person(String name, Long age) {
		this.name = name;
		this.age = age;
	}
}

```
5. Repository 구현.  
의존성에서 확인할 수 있겠지만 여기에서는 JPA를 사용하기 때문에 Repository는 Spring에서 제공하는 CrudRepository/JpaRepository 등을 사용하면 된다.  
```
public interface PersonRepository extends CrudRepository<Person, String> {}
```

여기까지 따라와서 실행까지 성공했다면 http://localhost:8080 으로 접속해보자.  
우리는 Controller를 구현하지도 않았지만 REST Api가 노출되어 있는 것을 확인할 수 있다.  
Tip: 본인은 Chrome을 사용하는데, JSON Parse 관련 플러그인을 설치하면 JSON 데이터 보기가 편하다.  

Spring에서 HATEOAS 규칙을 지키기 때문에 응답(JSON)에 링크(_links)가 나타날 것이다.  
http://localhost:8080/persons  
http://localhost:8080/profile/persons  
즉, PersonRepository를 구현하였고 이에 대해 Person(맨 첫글자를 소문자 + s 형태)에 대한 REST Api가 노출되어 있고 Self Description 규칙을 따르기 때문에 REST Api가 설명된다.  

간단하게 REST Api 호출로 데이터 하나를 생성해보고 결과를 확인해보자.  
1. 호출  
```
curl -X POST localhost:8080/persons -d "{\"name\": \"james\", \"age\": \"10\"}" -H "Content-Type:application/json"
```
2. 결과  
```
{
    "_embedded": {
        "persons": [
            {
                "name": "james",
                "age": 10,
                "_links": {
                    "self": {
                        "href": "http://localhost:8080/persons/1"
                    },
                    "person": {
                        "href": "http://localhost:8080/persons/1"
                    }
                }
            }
        ]
    },
    "_links": {
        "self": {
            "href": "http://localhost:8080/persons"
        },
        "profile": {
            "href": "http://localhost:8080/profile/persons"
        }
    }
}
```
***
