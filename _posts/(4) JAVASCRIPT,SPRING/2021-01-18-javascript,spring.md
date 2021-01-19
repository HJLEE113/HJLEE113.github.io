---

layout: post
title: 21.01.18 Mon
date: 2021-01-18
category: interview
tags: [jsp, html]

---

## 1. 자바스크립트 타입의 종류는?
문자String, 숫자Number, 함수Function, 객체Object, 참거짓Boolean, Undefined
[예시]
~~~javascript
<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>Insert title here</title>
<script type="text/javascript"></script>
</head>
<body>
	<script type="text/javascript">
		var varStr = "ABCDEF";
		console.log("varStr : " + varStr);
 
		var varNum = 123456;
		console.log("varNum : " + varNum);
 
		var varBoo = false;
		console.log("varBoo : " + varBoo);
 
		var varFun = function fun() {};
		console.log("varFun : " + varFun);
 
		var varObj = {};
		console.log("varObj : " + varObj);
 
		var varUnd = undefined;
		console.log("varUnd : " + varUnd);
	</script>
</body>
</html>
~~~

## 2. 게시판 만들기