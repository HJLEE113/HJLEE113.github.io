---

layout: post
title: 21.01.29 Fri
date: 2021-01-29
category: interview
tags: [javascript, spring]

---

## 1. Spring에서의 리소스 처리 방법에 대하여 설명하시오

-webapp 폴더
⊃resources 폴더(정적리소스)
⊃WEB-INF 폴더(보안이 필요한것들)

이걸 처리할때 수정하는 부분이 servlet-context.xml이다.

`<resources mapping="/resources/**"  location="/resources/" />`
          mapping : 접속 URL 패턴/  location : 물리적 폴더 경로

## 2. 아래와 같이 페이징을 구현하시오.

![image](https://user-images.githubusercontent.com/74958197/106385203-56009600-6412-11eb-9db7-be7f372264c6.png)
![image](https://user-images.githubusercontent.com/74958197/106385205-5a2cb380-6412-11eb-9fac-5d8904002c85.png)
~~~java
[BoardController.java]
// 페이징
	@GetMapping("/list2")
	public void list2(Criteria cri, Model model) {
		log.info("list() 호출");
		log.info(cri);
		model.addAttribute("list2", boardService.getList(cri));

		int total = boardService.getTotalCount(cri);
		log.info("total" + total);
		model.addAttribute("pageMaker", new PageVO(cri, total));
		// cri, total(전체 데이터 개수), new PageDTO(cri, total)->paging관련 파라미터 계산됨->list.jsp
	}
~~~
~~~java
[BoardService.java]
//페이징처리
	public List<BoardVO> getList(Criteria cri);

	public int getTotalCount(Criteria cri);
~~~
~~~java
[BoardServiceImpl.java]
// 페이징
	@Override
	public List<BoardVO> getList(Criteria cri) {
		
		return mapper.getPaging(cri);
	}

	@Override
	public int getTotalCount(Criteria cri) {
		
		return mapper.getTotalCnt(cri);
	}	
~~~
~~~java
[BoardMapper.java]
// 전체 게시글 갯수
	public int getTotalCnt(Criteria cri);
~~~
~~~java
[Criteria.java]
package edu.bit.board.page;

import lombok.Getter;
import lombok.Setter;
import lombok.ToString;

@ToString
@Getter
@Setter // 롬보기로 get set tostring 만들기
public class Criteria {
	// 페이징 처리를 위해선 페이지 번호와
	// 한페이지당 몇개의 데이터를 보여줄것이지 결정되어야함.
	private int pageNum;// 페이지 번호
	private int amount;// 한페이당 몇개의 데이터를 보여줄것인가?

	public Criteria() {
		this(1, 5);// 기본값 1페이지 10개로 지정; - this는 생성자를 호출
	}

	public Criteria(int pageNum, int amount) {
		this.pageNum = pageNum;
		this.amount = amount;
	}
}
~~~
~~~java
[PageVO.java]
package edu.bit.board.page;

import org.springframework.web.util.UriComponents;
import org.springframework.web.util.UriComponentsBuilder;

import lombok.Getter;
import lombok.Setter;
import lombok.ToString;

@ToString
@Setter
@Getter
public class PageVO {
//페이징 처리할때 필요한 정보들
	private int startPage;// 한번에 보여지는 페이지 시작번호
	private int endPage; // 화면에 보여지는 끝번호
	private boolean prev, next;// 이전과 다음으로 이동가능한 링크 표시

	private int total;// 전체가 나와야 위에 변수들이 조합이 되어서 세팅이 가능하다.
	private Criteria cri;

	public PageVO(Criteria cri, int total) {
		this.cri = cri;// 1번페이지에 10개 뿌리기
		this.total = total;// 전체 몇개가 있는지 알아야 세팅이 됨

		// 예:현재 페이지가 13이면 13/10 = 1.3 올림 → 2 끝페이지는 2*10=20
		this.endPage = (int) (Math.ceil(cri.getPageNum() / 5.0)) * 5;
		// 10.0개를 따로 변수지정해서 넣어도 상관없긴하지만 10개이상인 경우는 거의 없기 때문에 그냥 다이렉트로 넣는다.
		// startPage는 1, endPage는 10이 나오기위한 공식

		this.startPage = this.endPage - 4;

		// Total을 통한 endPage의 재계산
		// 10개씩 보여주는 경우 전체 데이터 수가 80개라고 가정하면 끝번호는 10이 아닌 8이 됨.
		int realEnd = (int) (Math.ceil((total * 1.0) / cri.getAmount()));

		if (realEnd <= this.endPage) {
			this.endPage = realEnd;
		}

		// 시작번호가 1보다 큰경우 존재
		this.prev = this.startPage > 1;// prev는 startPage가 1이라도 있게되면 존재

		// realEnd가 끝번호(endPage)보다 큰 경우에만 존재
		this.next = this.endPage < realEnd;

	}
  
	// 쿼리 만듦
	public String makeQuery(int page) {
		UriComponents uriComponentsBuilder = UriComponentsBuilder.newInstance().queryParam("pageNum", page)
				// pageNum = 3

				.queryParam("amount", cri.getAmount()) // pageNum=3&amount=10
				.build(); // ?pageNum=3&amount=10
		return uriComponentsBuilder.toUriString(); // ?pageNum=3&amount=10 리턴
	}

}
~~~
~~~java
[BoardMapper.xml]
<!-- 페이징 쿼리문 -->
	<select id="getPaging"
		resultType="edu.bit.board.vo.BoardVO">
   <![CDATA[
          
	     select * from ( SELECT ROWNUM AS rnum, A.* FROM (
                select * from mvc_board order by bGroup desc, bStep asc
           	 ) A where rownum <= #{pageNum} * #{amount}
  	 ) where rnum > (#{pageNum}-1) * #{amount}
   ]]>
	</select>

		<select id="getTotalCnt" resultType="int">
	
		select count(*) from mvc_board
		
	</select>
~~~ 
~~~java
[list2.jsp]
<!-- 페이징처리 코드 -->
	<c:if test="${pageMaker.prev}">
		<a href="list2${pageMaker.makeQuery(pageMaker.startPage - 1) }">pre</a>
	</c:if>

	<c:forEach begin="${pageMaker.startPage }" end="${pageMaker.endPage }"
		var="idx">
		<c:out value="${pageMaker.cri.pageNum == idx?'':''}" />
		<a href="list2${pageMaker.makeQuery(idx)}">${idx}</a>
	</c:forEach>

	<c:if test="${pageMaker.next && pageMaker.endPage > 0}">
		<a href="list2${pageMaker.makeQuery(pageMaker.endPage +1) }">next</a>
	</c:if>
	<br>
~~~	

`insert into mvc_board (bid, bname, btitle, bcontent, bhit, bgroup, bstep, bindent) values (mvc_board_seq.nextval, 'test', '테스트', '테스트', 0 , mvc_board_seq.currval, 0, 0);`

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


