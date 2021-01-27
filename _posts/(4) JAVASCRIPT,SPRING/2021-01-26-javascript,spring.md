---

layout: post
title: 21.01.26 Tue
date: 2021-01-26
category: interview
tags: [javascript, spring]

---


## 1.아래의 xml 에 대하여 설명하시오.

-pom.xml

개발자가 사용할 모듈(라이브러리)를 가져오기 위한 '<'dependency(의존성), artifactId(어떤모듈을 사용할지), version(모듈버전)'>'이 들어있는 파일

 
 

-web.xml

어떤 servlet을 배포할 것인지, 그 servlet이 어떤 url에 매핑되는지 설정해주는 파일. 톰켓이 최초 구동될때 web.xml을 읽고 해당 설정을 구성한다. 

 

 

-context.xml

servlet-context.xml : 웹관련쪽(dispatcher,controller-view)-어노테이션, 리소스 디렉토리, ViewResolver에 관한 설정

root-context.xml : 그 외 부분(command, dao)-View 지원을 제외한 bean을 설정. ex) Service / Repository(DAO) / DB/ log 등등

 


## 2.스프링에서 게시판 사용을 위한 설계도를 그리시오.
![sttst](https://user-images.githubusercontent.com/74958197/105840863-0fc4c480-6017-11eb-8bda-ae2b3ae950c5.png)






## 3.스프링에서 한글처리는 어떻게 하는가?



web.xml에서 `<filter>`소스를 넣어야 한다.
~~~xml
				'''
   </servlet-mapping>
여기와
   
   <filter>
      <filter-name>encoding</filter-name>
      <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
      <init-param>
         <param-name>encoding</param-name>
         <param-value>UTF-8</param-value>
      </init-param>
   </filter>

   <filter-mapping>
      <filter-name>encoding</filter-name>
      <servlet-name>appServlet</servlet-name>
   </filter-mapping>
   
   여기 사이에 붙여넣기
   </web-app>
~~~

## 4.마이바티스에 대하여 설명하시오.

XML이나 @(annotation)을 사용하여 SQL문으로 객체를 연결시키는 것.



pom.xml에 해당 소스를 넣어야한다.
~~~xml
[pom.xml]
					'''
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
		<dependency>
			<groupId>org.mybatis</groupId>
			<artifactId>mybatis</artifactId>
			<version>3.4.6</version>
		</dependency>

		<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
		<dependency>
			<groupId>org.mybatis</groupId>
			<artifactId>mybatis-spring</artifactId>
			<version>1.3.2</version>
		</dependency>
					'''
~~~



수업시간 MyBatis 사용으로 만든 xml코드.  src/main/resource 에 파일 생성
~~~xml
[BoardMapper.xml]
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="edu.bit.board.mapper.BoardMapper">
					<!-- ↑인터페이스 -->
					
<!--↓인터페이스 BoardMapper의 자식이 구현해야하는데 id=""로 구현 -->
	   <select id="getList" resultType="edu.bit.board.vo.BoardVO">
   <![CDATA[
      select bId, bName, bTitle, bContent, bDate, bHit, bGroup, bStep, bIndent from mvc_board order by bGroup desc, bStep asc
   ]]>
   </select>          
</mapper>
~~~



## 5.스프링에서 hello.jsp 가 유저에게 전달되기 까지의  순서와 해당 객체를 그림으로 표현하시오.

![spring](https://user-images.githubusercontent.com/74958197/105836382-6f6ba180-6010-11eb-9a16-cb6acc0272de.png)