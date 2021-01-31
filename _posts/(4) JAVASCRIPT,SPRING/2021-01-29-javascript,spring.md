---

layout: post
title: 21.01.29 Fri
date: 2021-01-29
category: interview
tags: [javascript, spring]

---

## 1. Spring에서의 리소스 처리 방법에 대하여 설명하시오







## 2. 아래와 같이 페이징을 구현하시오.

![image](https://user-images.githubusercontent.com/74958197/106385203-56009600-6412-11eb-9db7-be7f372264c6.png)
![image](https://user-images.githubusercontent.com/74958197/106385205-5a2cb380-6412-11eb-9fac-5d8904002c85.png)

## 3. 소셜로그인(OAuth2)-카카오,네이버 
소셜로그인 - 카카오계정
~~~java
[KakaoController.java]
package edu.bit.board.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import java.text.DateFormat;
import java.util.Date;
import java.util.Locale;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class KakaoController {

	private static final Logger logger = LoggerFactory.getLogger(KakaoController.class);

	/**
	 * Simply selects the home view to render by returning its name.
	 */
	@GetMapping("/home")
	public void home(Locale locale, Model model) {
		logger.info("Welcome home! The client locale is {}.", locale);

		Date date = new Date();
		DateFormat dateFormat = DateFormat.getDateTimeInstance(DateFormat.LONG, DateFormat.LONG, locale);

		String formattedDate = dateFormat.format(date);

		model.addAttribute("serverTime", formattedDate);

	}

}
~~~
~~~jsp
[home.jsp]
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, width=device-width" />
    <title>Login Demo - Kakao JavaScript SDK</title>
    <script src="http://developers.kakao.com/sdk/js/kakao.min.js"></script>

</head>
<body>
    <a id="kakao-login-btn"></a><br>
    <a href="http://developers.kakao.com/logout">Logout</a>
    <script type='text/javascript'>
       
        // JavaScript 키 설정
        Kakao.init('36d5bbfd1b0bc7d5ce37f1dfa97fb95c');
        // 카카오 로그인 버튼을 생성
        Kakao.Auth.createLoginButton({
            container: '#kakao-login-btn',
            success: function (authObj) {
                alert("로그인 성공");
            },
            fail: function (err) {
                alert("로그인 실패");
            }
        });
      
    </script>
</body>
</html>
~~~
![image](https://user-images.githubusercontent.com/74958197/106385465-ceb42200-6413-11eb-8423-219a550c1948.png)
![image](https://user-images.githubusercontent.com/74958197/106385470-d4aa0300-6413-11eb-8dbe-06fa7e8d7ef8.png)


