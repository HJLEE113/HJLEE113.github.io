---

layout: post
title: 21.01.22 Fri
date: 2021-01-22
category: interview
tags: [javascript, spring]

---

## 1. command객체에 대하여 설명하시오.

getParameter 대신 쓸 수 있는것

 

 

## 2.ModelAndView 객체에 대하여 설명하시오.

 

## 3.아래의 골뱅이에 대하여 설명하시오.

@Controller

@RequestParam

@RequestMapping

 

## 4.아래를 프로그래밍 스프링으로 프로그래밍 하시오.
-국영수 입력 페이지
-국영수점수를 서버에서 받아서,총점과 평균을 리턴
-해당 총점과 평균의 점수의 색깔은 각각 빨간색과 파란색으로 만들것(JS로).

~~~java
[GradeController.java]
package edu.bit.ex;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;


import edu.bit.ex.mygrade.Subject;

/**
 * Handles requests for the application home page.
 */
@Controller
public class GradeController {

	private static final Logger logger = LoggerFactory.getLogger(GradeController.class);

	/**
	 * Simply selects the home view to render by returning its name.
	 */
	@RequestMapping("/grade/input")
	public String MyGrade() {

		return "grade/input";
	}
	
	@RequestMapping("/grade/score")
	public String MyGrade(Subject subject) {

		return "grade/score";
	}
}
~~~
~~~java
[Subject.java]
package edu.bit.ex.mygrade;

public class Subject {
private double kor;
private double eng;

public Subject() {
	
}

public Subject(double kor, double eng, double math) {
	this.kor = kor;
	this.eng = eng;
	this.math = math;
}


public double getKor() {
	return kor;
}
public void setKor(double kor) {
	this.kor = kor;
}
public double getEng() {
	return eng;
}
public void setEng(double eng) {
	this.eng = eng;
}
public double getMath() {
	return math;
}
public void setMath(double math) {
	this.math = math;
}
private double math;

}
~~~

~~~jsp
[input.jsp]
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<%@ page contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" language="java" %>
<%@ page session="false" %>
<html>
<head>
	<title>Home</title>
</head>
<body>

<h1>My Grade</h1>

<form action="score">
국어 : <input type="number" name="kor"><br/>
영어 : <input type="number" name="eng"><br/>
수학 : <input type="number" name="math"><br/>
<input type="submit" value="제출">
</form>
</body>
</html>
~~~


~~~jsp
[score.jsp]
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<%@ page contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" language="java" %>
<%@ page session="false" %>
<html>
<head>
	<title>Home</title>
<script>
window.onload = function(){
	var scoreColor = document.getElementById("scoreColor");
	scoreColor.style.color = "blue";
	
	var avgColor = document.getElementById("avgColor");
	avgColor.style.color = "red";
};
</script>
</head>
<body>

<h1>My Grade</h1>

국어 : ${subject.kor}<br/>
영어 : ${subject.eng}<br/>
수학 : ${subject.math}<br/>
총점 : <span id="scoreColor">${subject.kor+subject.eng+subject.math}</span><br/>
평균 : <span id="avgColor">${(subject.kor+subject.eng+subject.math)/3}</span>
</body>
</html>
~~~

![image](https://user-images.githubusercontent.com/74958197/105635048-61990d80-5ea4-11eb-87c1-fc3e10c2ee2c.png)


 
## 5.제일위에 입력버튼 하나를 만든다.
-버튼을 누르면 200*200 파란색 박스가 하나씩 계속해서 생기는 프로그램을 만드시오.
~~~html
<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>JavaScript</title>
<script>
		function plus(){
		document.getElementById("box").innerHTML
								//inner'HTML'빼먹지 말기
			+= "<div style='background-color: blue; width: 200px; height: 200px;'></div><br>";

		}
		</script>
<style>

</style>
</head>
<body>
<div id="box">
	<input type="button" value="클릭" onclick="plus()">
	</div>
</body>
</html>
~~~
![image](https://user-images.githubusercontent.com/74958197/105635530-9e660400-5ea6-11eb-8793-a032fe330990.png)
