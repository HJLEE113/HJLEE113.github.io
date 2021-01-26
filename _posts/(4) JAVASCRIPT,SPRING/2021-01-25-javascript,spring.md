---

layout: post
title: 21.01.25 Mon
date: 2021-01-25
category: interview
tags: [javascript, spring]

---
## 1.아래 annotation 의 용도는? 
@ModelAttribute



@ModelAttribute : 유효성 검사를 할 form과 커맨드 객체 타입 지정


## 2. id 와 pw 를 두개를 만든후 아래와 같이 유효성 검사를 하시오. 

-클라이언트쪽 체크: id 가 널이거나 없으면 서버로 보내지 않으면서 - 해당 페이지에 다시 입력하세로 라는 문구 출력 
-서버쪽 체크: id에 10자 초과이거나 숫자로만 되어 있어 있으면 다시 입력하는 페이지로 이동하여 다시 입력하세요 라는 문구 출력 

-클라이언트쪽 체크: pw 가 널이거나 없으면 서버로 보내지 않으면서 - 해당 페이지에 패스워드 다시 입력하세로 라는 문구 출력 
-서버쪽 체크: pw에 8자 미만이거나, 숫자로만 되어 있어 있거나, 문자로만 되어 잇으면, 다시 입력하는 페이지로 이동하여 패스워드 다시 입력하세요 라는 문구 출력 

-성공시 로그인이 되었습니다. 라는 페이지로 이동 

//하는중
~~~java
[Studnet.java]
package edu.bit.ex;

import lombok.AllArgsConstructor;
import lombok.Getter;
import lombok.NoArgsConstructor;
import lombok.Setter;

@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
public class Student {
	
private String id;

private String pw;
}
~~~java
[StudentController.java]
package edu.bit.ex;

import javax.servlet.http.HttpServletRequest;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.validation.BindingResult;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.RequestMapping;

/**
 * Handles requests for the application home page.
 */
@Controller
public class StudentController {

	@RequestMapping("studentNg")
	public String studentNg(Model model) {

		return "/studentNg";
	}

	@RequestMapping("/studentForm")
	public String studentForm() {
		return "createPage";
	}

	@RequestMapping("student/studentNg")
	public String studentCreate(@ModelAttribute("student") Student student, BindingResult result) {
		// Validator쓰려면 BindingResult result 이걸 넣어야함. 그리고 이건 다형성이다!
		String page = "loginDone";

		StudentValidator validator = new StudentValidator();
		validator.validate(student, result);

		if (result.hasErrors()) {
			page = "studentLogin";
		}

		return page;
	}
	@RequestMapping("StudentValidator")
	public String validate() {
		return "loginForm";
	}

}
~~~
~~~java
[StudentValidator.java]
package edu.bit.ex;

import org.springframework.validation.Errors;
import org.springframework.validation.Validator;

public class StudentValidator implements Validator {

	@Override
	public boolean supports(Class<?> clazz) {
		// Class<?> = 어떤 클래스든지 잡아도 좋다 라는 말인데 지금은 이해할필요X

		return false;
	}

	@Override
	public void validate(Object obj, Errors errors) {
		//StudentController.java 에서 BindingResult result는 자식, Errors errors가 부모이다★★
		
		System.out.println("validate()");

		// obj가 넘어오는건 학생이다.
		Student student = (Student) obj; // 형변환

		String studentId = student.getId();
		//studentId가 10자초과 또는 숫자로만 되어있으면
		if (studentId.length()>10 || studentId.matches(".*[0-9].*")) {
			//다시 입력하는 페이지로 갈것
			errors.rejectValue("name", "trouble");
		}

		String studentPw = student.getPw();
		//studentPw가 8자 미만 또는 숫자로만 되어있으면
		if (studentPw.length()<8 || studentPw.matches(".*[0-9].*")) {
			//다시 입력하는 페이지로 갈것
			errors.rejectValue("id", "trouble");

		}
	}

}
~~~
~~~jsp
[createPage.jsp]
<%@ page language="java" contentType="text/html; charset=EUC-KR"
    pageEncoding="EUC-KR"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=EUC-KR">
<title>Insert title here</title>
</head>
<body>
createPage.jsp
<br />

<% 
   String conPath = request.getContextPath();
%>

<!-- <form action="student/create"> -->
<!-- ↑상대령로 ↓절대경로 //절대적으로 에러가 덜나기때문에 절대경로 넣기! -->
<form action="<%=conPath %>/student/create">
   이름 : <input type="text" name="name" value="${student.name}"> <br />
   아이디 : <input type="text" name="id" value="${student.id}"> <br />
   <input type="submit" value="전송"> <br />
</form>

</body>
</html>
~~~
~~~jsp
[loginDone.jsp]
<?xml version="1.0" encoding="UTF-8"?>

<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<!DOCTYPE html>
<html>

<head>
<title>Home</title>
</head>

<body>
		<h1>로그인이 되었습니다.<br>

	</h1>
</body>
</html>
~~~
~~~jsp
[studnetLogin.jsp]
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>

<head>
<title>JavaScript</title>

<script>
	window.onload = function() {

		//submit button
		var sbmBtn = document.getElementById("sbmBtn");
		sbmBtn.onclick = function() {

			if (document.getElementById("Id").value == "") {
				alert("다시 입력하세요");
				return false;
				//return "redirect:studentNg";///
			} else if (document.getElementById("Pw").value == "") {
				alert("패스워드 다시 입력하세요");
				return false;
				//return "redirect:studentNg";
			}  else {		
				document.getElementById("loginDone").submit();
			} 
		};
	}
</script>
<style></style>
</head>
<body>

	<form  action="loginDone">
		USER ID : <input id="Id" type="text" name="Id"><br>
		USER PW : <input id="Pw" type="password" name="pw"><br>
		<input id="sbmBtn" type="button" value="SUBMIT">
	</form>

</body>

</html>
~~~

## 3.마이바티스를 활용하여, emp 12개를 뿌리시오. 
