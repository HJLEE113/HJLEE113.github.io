---

layout: post
title: 21.01.19 Tue
date: 2021-01-19
category: interview
tags: [javascript, spring]

---

## 1.클로져란 무엇인가?

클로저(closure)는 내부함수와 밀접한 관계를 가지고 있는 주제다. 

외부함수의 지역변수에 접근 가능한 내부함수가 소멸할 때까지 외부함수가 소멸되지 않는 특성을 의미
~~~java
[closure 클로저 예제]
function outter(){
    var title = 'coding everybody';  
    return function(){        
        alert(title);
    }
}
inner = outter();
inner();
//coding everybody를 출력
~~~

## 2.js를 이용하여, 구구단중 홀수단만 나오게 하시오.
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
		document.write("<table border = 1>")	
		for (var k = 1; k <= 4; k++) {
			document.write("<td>" + (2*k+1) + "단</td>")
		}
		for (var i = 1 ; i <= 9; i++) {
			document.write("<tr>");
			for (var j =1; j <= 4; j++) {
			
				document.write("<td>" + (2*j+1) + "x" + i + "=" + i * j + "</td>");
			}
			document.write("</tr>");
		}
		document.write("</table>")
	</script>
</body>
</html>
~~~
## 3.부서별로 sal의 최소 값을 구하는데, 30번 부서의 sal 최소값 보다 큰것을 구하시오. 
~~~sql
select deptno, min(sal) from emp group by deptno 
having min(sal) > (select min(sal) from emp where deptno = 30);

select deptno, sal from emp where sal >(select min(sal) from emp where deptno = 30)
and(deptno, sal) in(select deptno,min(sal) from emp group by deptno);
~~~
## 4.삼각형및 사각형의 넓이를 구하는 프로그래밍을 IoC 컨테이너를 이용하여 프로그래밍 하시오.
~~~html
[applicationCTX.xml]
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

	<bean id="trirec" class="com.javac.ex.TriRec">
		<property name="width">
			<value>3</value>
		</property>
		<property name="height">
			<value>4</value>
		</property>
	</bean>
</beans>
~~~
~~~java
[MainClass.java]
package com.javac.ex;

import org.springframework.context.support.AbstractApplicationContext;
import org.springframework.context.support.GenericXmlApplicationContext;

public class MainClass {

	public static void main(String[] args) {
		String configLocation = "classpath:applicationCTX.xml";
		AbstractApplicationContext ctx = new GenericXmlApplicationContext(configLocation);
		TriRec trirec = ctx.getBean("trirec", TriRec.class);
		trirec.TriRecArea();
		ctx.close();
	}
}
~~~
~~~java
[TriRec.java]
package com.javac.ex;

public class TriRec {
	private double width;
	private double height;
	private double triArea;
	private double recArea;


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

	public void TriRecArea() {
		triArea = width * height * 0.5;
		recArea = width * height;
		System.out.println("가로는 " + width);
		System.out.println("세로는 " + height);
		System.out.println("삼각형의 넓이는 : " + triArea);
		System.out.println("사각형의 넓이는 : " + recArea);

	}

}
~~~
![image](https://user-images.githubusercontent.com/74958197/105024756-d4168180-5a8f-11eb-805c-5d4c6c9e336c.png)
