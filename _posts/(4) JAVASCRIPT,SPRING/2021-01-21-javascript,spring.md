---

layout: post
title: 21.01.21 Thu
date: 2021-01-21
category: interview
tags: [javascript, spring]

---



## 1.게시판 replyShape 생성시 아래의 쿼리문에서
bStep > ? 은 무슨 의미 인가?
`update mvc_board set bStep = bStep + 1 where bGroup = ? and bStep > ?`

 bStep = 위에서 몇 번째 위치할 것이냐는 뜻.
 원문에서 bStep+1 해준다.


## 2.sql 문제
-17. 부서별 급여 평균을 출력하시오.
~~~sql
select deptno,avg(sal) from emp group by deptno;
~~~
![image](https://user-images.githubusercontent.com/74958197/105342243-774bd000-5c23-11eb-8907-43f432299686.png)
-18. 오늘은 몇요일인가? 
~~~sql
select to_char(sysdate, 'day') as "오늘 요일" from dual;
~~~
![image](https://user-images.githubusercontent.com/74958197/105342853-3902e080-5c24-11eb-8fa9-89807eea6d99.png)

-10. EMP Table에서 급여가 1800 이상이면 ‘good’, 아니면 ‘poor’를 출력하시오. 
~~~sql
select sal, case when sal>=1800 then 'good' else 'poor' end as "1800기준sal" from emp;
~~~
![image](https://user-images.githubusercontent.com/74958197/105342874-3ef8c180-5c24-11eb-9283-283ac69eb5db.png)
## 3.가위바위보 이미지 넣어서 짜시오.



~~~javascript
<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>Insert title here</title>
<script type="text/javascript">
</script>
<style>
</style>
</head>
<body>
	<script type="text/javascript">

		var scissor = "가위.PNG"
		var rock = "바위.PNG"
		var paper = "보.PNG"

		var comimg = document.createElement("img");
		var userimg = document.createElement("img");
		comimg.setAttribute("src", "가위.PNG");
		comimg.setAttribute("src", "바위.PNG");
		comimg.setAttribute("src", "보.PNG");

		function Game() {
			var com;
			var user;
			var result;
			this.getCom = function() {

			}
			this.setCom = function(com) {

				this.com = com;
				if (this.com == 1) {

					document.write("컴퓨터 <br>");
					comimg.setAttribute("src", "가위.PNG");
					document.body.appendChild(comimg);
				} else if (this.com == 2) {
					document.write("컴퓨터 <br>")
					comimg.setAttribute("src", "바위.PNG");
					document.body.appendChild(comimg);
				} else if (this.com == 3) {
					document.write("컴퓨터 <br>")
					comimg.setAttribute("src", "보.PNG");
					document.body.appendChild(comimg);

				}
			};

			
			this.getUser = function() {
				return this.user;
			};

			this.setUser = function(user) {
				this.user = user;
				if (this.user == 1) {
					document.write("유저 <br>");
					userimg.setAttribute("src", "가위.PNG");
					document.body.appendChild(userimg);
				} else if (this.user == 2) {
					document.write("유저 <br>")
					userimg.setAttribute("src", "바위.PNG");
					document.body.appendChild(userimg);
				} else if (this.user == 3) {
					document.write("유저 <br>")
					userimg.setAttribute("src", "보.PNG");
					document.body.appendChild(userimg);
				}
			}

			this.result = function() {
				if (this.user == this.com) {
					return ("비김");
				} else if (this.user == 1 && this.com == 3 || this.user == 2
						&& this.com == 1 || this.user == 3 && this.com == 2) {
					return ("유저 승");
				} else if (this.user == 1 && this.com == 2 || this.user == 2
						&& this.com == 3 || this.user == 3 && this.com == 1) {
					return ("컴퓨터 승");
				}

			}
		}
		var userinput = prompt("가위=1, 바위=2, 보=3", "입력");
		var cominput = Math.floor((Math.random() * 3) + 1);
		var gameResult = new Game();
		gameResult.setCom(cominput);
		gameResult.setUser(userinput);

		document.write("결과는 : " + gameResult.result() + "<br>");
	</script>
~~~
![image](https://user-images.githubusercontent.com/74958197/105342964-5b94f980-5c24-11eb-8acf-f74ac7e8d178.png)
## 4.Bom , 과 Dom 이란?
BOM = 브라우저 객체


DOM - 알고리즘. 트리구조. 부모자식관계.

소프트웨어는 DOM처럼 짜야한다.

Javascript를 이용해서 html태그 객체를 생성, 추가, 삭제, 이동 등의 작업을 할 수 있다.

=DOM은 자바스크립트를 동적으로 바꿔준다.

##5. 3조 조별회의

//shape.setWidth(10);이 안되는 이유.
~~~java
public class MainClass {
 
	public static void main(String[] args) {
		String configLocation = "classpath:applicationCTX.xml";
		AbstractApplicationContext ctx = new GenericXmlApplicationContext(configLocation);
											
		IShape ishape = ctx.getBean("ishape",IShape.class);
		//shape.setWidth(10);이 안되는 이유.
		System.out.println(ishape.getArea());
		
		ctx.close();
	}
}
~~~

IShape 인터페이스는 부모, 세 도형들은 자식으로 자식이 getter/setter 메소드를 구현했는데 부모는 자식에게 물려주기만 했을 뿐 정보를 받지 않았기 때문에 자식만의 고유 정보를 쓸 수 없다.

shape.setWidth를 쓰면 오류나는 이유는 다형성 때문!