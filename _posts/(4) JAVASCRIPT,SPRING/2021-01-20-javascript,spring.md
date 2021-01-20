---

layout: post
title: 21.01.20 Wed
date: 2021-01-20
category: interview
tags: [javascript, spring]

---

## 1. 아래를 설명하시오.
-DI
-IoC
-IoC 컨테이너

## 2. JS로 시간이 초단위로 갱신되는 페이지를 만드시오.


## 3. js 에서의 객체생성 방법은?


## 4. 아래를 자바 스크립트로 작성하시오.
-변수 radius
-get set 함수 작성
-프롬프트로 숫자 입력값 받음
-set 함수를 radius 값 세팅
-객체 생성후 getArea() 함수 호출하면 원넓이 출력
~~~javascript
<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>Insert title here</title>
<script type="text/javascript"></script>
<style>
</style>
</head>
<body>
	<script type="text/javascript">
		function Circle() {
			var radius = 0;

			this.area = function() {
				return (this.radius * this.radius * Math.PI);

			}
			this.getRadius = function() {
				return this.redius;
			}
			this.setRadius = function(radius) {
				if (!isNaN(radius)) {
					this.radius = radius;
				} else {
					console.log("radius is NaN(Not a Number)!");
				}
			}
		}

		var getArea = new Circle();
		this.radius = prompt("원의 넓이 구하기", "원의 반지름을 입력하세요.")
		getArea.setRadius(this.radius);
		console.log("원의 넓이는 : " + getArea.area());
	</script>
</body>
</html>
~~~

## 5.위와 같은 방식으로 가위바위보 게임을 짜시오.

-DOM 객체를 배우면 이미지도 바꿔 보도록 합시다.














## 6.annotation 방식으로 하여 객체 생성후 사각형과 삼각형 넓이를 구하시오.

~~~java
[MainClass.java]
package com.javalec.ex;

import org.springframework.context.annotation.AnnotationConfigApplicationContext;


public class MainClass {

	public static void main(String[] args) {
		
		AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext(ApplicationConfig.class);
		
		Area triangle = ctx.getBean("triangle", Area.class);
		System.out.println("삼각형의 가로는 : " + triangle.getWidth());
		System.out.println("삼각형의 세로는 : " + triangle.getHeight());
		System.out.println("삼각형의 넓이는 : " + triangle.getTriArea());
		

		Area rectangle = ctx.getBean("rectangle", Area.class);
		System.out.println("사각형의 가로는 : " + rectangle.getWidth());
		System.out.println("사각형의 세로는 : " + rectangle.getHeight());
		System.out.println("사각형의 넓이는 : " + rectangle.getRecArea());
		
		ctx.close();
	}
}
~~~
~~~java
[Area.java]
package com.javalec.ex;

public class Area {
	private double triArea;
	private double recArea;
	double width;
	double height;


	public Area(double height, double width) {
		this.height = height;
		this.width = width;
		this.triArea = triArea;
		this.recArea = recArea;
	}

	public double getTriArea() {
		return triArea;
	}

	public void setTriArea(double triArea) {
		this.triArea = triArea;
	}

	public double getRecArea() {
		return recArea;
	}

	public void setRecArea(double recArea) {
		this.recArea = recArea;
	}

	public double getWidth() {
		return width;
	}

	public void setWidth(double width) {
		this.width = width;
	}

	public double getHeight() {
		return height;
	}

	public void setHeight(double height) {
		this.height = height;
	}

	
}
~~~
~~~java
[ApplicationConfig.java]
package com.javalec.ex;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class ApplicationConfig {

	@Bean
	public Area triangle() {
		Area triangle = new Area(7.0,3.0);
		triangle.setTriArea(triangle.width*triangle.height*0.5);	
		
		return triangle;	
	}
	
	@Bean
	public Area rectangle() {
		Area rectangle = new Area(5.0, 3.0);
		rectangle.setRecArea(rectangle.width*rectangle.height);
		
		return rectangle;
	}
}
~~~




7.금일 배운 Pencil의 예처럼 아래를 인터 페이스를 구현하여, 원, 삼각형, 사각형의 넓이를 설정파일 에서 바꾸면 각각의 넓이가  구하여 지도록 하시오.

interface IShape{
double getArea();
}




8.스프링 미리 공부 구현 해야될 내용-미리준비해 놓읍시다.(한마디로 외워 제낍시다).
스프링 게시판(오라클 + 마이바티스),스프링 시큐리티, 소셜로그인(OAuth2)-카카오,네이버 먼저, 결재구현(아임포트)
