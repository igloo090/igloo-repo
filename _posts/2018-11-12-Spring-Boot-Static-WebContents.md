---
layout: post
title: "Spring Boot Static WebContents"
subtitle: "About Spring Boot Static WebContents"
background: "/background.jpg"
---

# Spring Boot Static WebContents

***

### 스프링 부트에서 정적 웹 컨텐츠  
스프링, JSP 등 Web MVC 패턴을 따르는 프레임워크 내에서 정적 웹 컨텐츠는 특정 위치에서 관리된다.  
그렇다면 스프링 부트에서는 어떤 위치에서 관리되어야 하는 것일까?  

[Serving Static Web Cotents with Spring Boot](https://spring.io/blog/2013/12/19/serving-static-web-content-with-spring-boot)  

위 문서를 기준으로 이해한 내용을 정리해보고자 한다.  
스프링 부트에서는 특정 경로들을 기본적으로 정적 웹 컨텐츠가 위치하는 경로라고 인식한다.  
1. /META-INF/resource/  
2. /resources/  
3. /static/  
4. /public/  

만약 다른 경로를 지정하고 싶다면, 아래와 같이 `WebMvcConfigurationSupport` 클래스를 상속받은 `@Configuration` 속성을 빈으로 등록해야 한다.  
```java
@Configuration
public class FcmManagerDemoConfiguration extends WebMvcConfigurationSupport {
	private static final String[] CLASSPATH_RESOURCE_LOCATIONS = {
            "classpath:/META-INF/resources/", "classpath:/resources/",
            "classpath:/static/", "classpath:/public/" };
	
    @Override
    protected void addResourceHandlers(ResourceHandlerRegistry registry) {
        //
        registry.addResourceHandler("/**").addResourceLocations(CLASSPATH_RESOURCE_LOCATIONS);
    }
}
```  

스프링 부트에서는 `@SpringBootApplication` 어노테이션을 통해 많은 속성들이 자동화된다.  
`@SpringBootApplication` 어노테이션은 `@EnableAutoConfiguration` 어노테이션을 포함하고 있으며, `AutoConfigurationImportSelector` 클래스에 의해서 자동화될 속성들을 선별한다.  
위의 소스처럼 `@Configuration` 어노테이션으로 속성을 빈으로 등록할 경우 `AutoConfigurationImportSelector`에서 선별 과정에서 자동화가 이루어지지 않게 되어 자신이 만든 속성이 적용될 수 있는 것이다.  

***

