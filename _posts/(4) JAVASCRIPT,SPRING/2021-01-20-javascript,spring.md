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

### #DI  : Dependency Injecton (=종속성 주입)

부품 객체를 생성하고 조립한다.
###### <주입방법 2가지>
###### -Setter Injection : setter 함수로 주입
~~~
ex. B b = new B();

    A a = new A();

    a.setB(b); //이게 spring. spring은 이렇게 부품을 조립해준다.
~~~


###### -Construction Injection : 생성자를 통해 주입
~~~
ex. B b = new B();

    A a= new A(b); //A(b)가 spring
~~~

### #IoC : Inversion of Control

### #IoC 컨테이너

역순으로 조립한 컨테이너(작은 부품에서 큰부품으로 조립해서 과정을 알 수 있다.
DI(부품)이 결합해 역순으로 조립한 컨테이너  
~~~
//IOC 생성순서
Computer computer = new Computer(); 같은 완제품이 아닌
Chip chip = new Chip();
CPU cpu = new Cpu(chip);
Computer computer = new Computer(Cpu); // = 조립컴
~~~
## 2. JS로 시간이 초단위로 갱신되는 페이지를 만드시오.
~~~html
<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>Insert title here</title>
</head>
<body>
	<script type="text/javascript">
	setTimeout("location.reload()", 1000);
	</script>
</body>
</html>
//1초후마다 계속 갱신된다.
~~~

## 3. js 에서의 객체생성 방법은?
var 변수명 = {
  key : value,
  key : value,
   ...
}
~~~java
ex.
var objCar = {
		width : "3m",
		height : "2m",
		cc : "2000cc",
		energy : 100
        }
~~~

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
![image](https://user-images.githubusercontent.com/74958197/105212326-a5cc9b00-5b90-11eb-9ca3-8053ba3d09db.png)

## 5.위와 같은 방식으로 가위바위보 게임을 짜시오.

-DOM 객체를 배우면 이미지도 바꿔 보도록 합시다.


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
		function Game() {
			var com;
			var user;

			this.getCom = function() {
				return this.com = Math.floor(Math.random() + 1);
				;
			}
			this.setCom = function(com) {
				this.com = com;
			}

			this.getUser = function() {
				return this.user;
			}
			this.setUser = function(user) {
				if (user == 1 || user == 2 || user == 3) {
					this.user = user;
				} else {
					console.log("가위=1, 바위=2, 보=3 중에 입력하세요")
				}
			}
		}
		this.result = function() {

			if (this.com == 1 && this.user == 1) {
				console.log("비김");
			} else if (this.com == 1 && this.user == 2) {
				console.log("이김");
			} else if (this.com == 1 && this.user == 3) {
				console.log("컴퓨터승리");
			}

			if (this.com == 2 && this.user == 2) {
				console.log("비김");
			} else if (this.com == 2 && this.user == 1) {
				console.log("컴퓨터승리");
			} else if (this.com == 2 && this.user == 3) {
				console.log("이김");
			}

			if (this.com == 3 && this.user == 3) {
				console.log("비김");
			} else if (this.com == 3 && this.user == 1) {
				console.log("이김");
			} else {
				console.log("컴퓨터승리");
			}
		}

		var getResult = new Game();
		var userinput = prompt("가위=1, 바위=2, 보=3", "입력")
		getResult.getCom()
		getResult.getUser();
		console.log("결과는 : " + getResult.result());
	</script>
</body>
</html>











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

~~~html
[applicationCTX.xml]
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

	<!-- 클래스명만 수정하면 각각의 넓이가 구해짐-->
	<!--<bean id="ishape" class="com.javalec.ex.Circle"> -->
	<!-- <bean id="ishape" class="com.javalec.ex.Rectangle"> -->
	<bean id="ishape" class="com.javalec.ex.Triangle">
		<property name="side">
			<value>2</value>
		</property>
	</bean>
</beans>
~~~
~~~java
[MainClass.java]
package com.javalec.ex;

import org.springframework.context.support.AbstractApplicationContext;
import org.springframework.context.support.GenericXmlApplicationContext;

public class MainClass {

	public static void main(String[] args) {
		String configLocation = "classpath:applicationCTX.xml";
		AbstractApplicationContext ctx = new GenericXmlApplicationContext(configLocation);
											
		IShape ishape = ctx.getBean("ishape",IShape.class);
		
		System.out.println(ishape.getArea());
		//void가 아니기 때문에 클래스 return값을 호출해야함
		
		ctx.close();
	}
}
~~~
~~~java
[IShape.java]
package com.javalec.ex;

public interface IShape {

	double getArea();
}
~~~
~~~java
[Triangle.java]
package com.javalec.ex;

public class Triangle implements IShape {
	double side;

	public double getSide() {
		return side;
	}

	public void setSide(double side) {
		this.side = side;
	}

	@Override
	public double getArea() {
		System.out.println("정삼각형의 넓이는 : ");
		return side*side*0.5;
	}
}
~~~
~~~java
[Circle.java]
package com.javalec.ex;

public class Circle implements IShape {
	double side;

	public double getSide() {
		return side;
	}

	public void setSide(double side) {
		this.side = side;
	}

	@Override
	public double getArea() {
		System.out.println("원의 넓이는 : ");
		return side*side* Math.PI;
	}
}
~~~
~~~java
[Rectangle.java]
package com.javalec.ex;

public class Rectangle implements IShape {
	double side;

	public Rectangle(double side) {
		this.side = side;
	}
	public double getSide() {
		return side;
	}
	public void setSide(double side) {
		this.side = side;
	}

	@Override
	public double getArea() {
		System.out.println("정사각형의 넓이는 : ");
		return side*side;
	}
}
~~~
![image](https://user-images.githubusercontent.com/74958197/105211609-d06a2400-5b8f-11eb-93aa-3052ec49de09.png)


8.스프링 미리 공부 구현 해야될 내용-미리준비해 놓읍시다.(한마디로 외워 제낍시다).
스프링 게시판(오라클 + 마이바티스),스프링 시큐리티, 소셜로그인(OAuth2)-카카오,네이버 먼저, 결재구현(아임포트)
