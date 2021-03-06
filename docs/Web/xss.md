# XSS란 무엇이고 이 공격은 어떻게 예방할 수 있을까요?
> This is a translation of 30-Seconds-of-knowledge's [What is a cross-site scripting attack (XSS) and how do you prevent it?](https://github.com/30-seconds/30-seconds-of-interviews/blob/master/questions/xss.md) in korean, and contains additional learning contents on this. 

XSS는 공격자가 합법적인 웹 사이트나 웹 애플리케이션에 악성 스크립트를 주입하는 Client-side 코드 주입을 말한다. 공격자는 주입한 악성 코드를 위와 같은 환경에서 실행되도록 하는 것이 목표이다. 이는 애플리케이션이 사용자 입력을 검증하지 않고 동적으로 HTML 코드를 자유롭게 주입할 경우 종종 이뤄지는 공격 방식이다. 

예를 들어, 댓글 시스템은 유저의 입력을 검증하거나 회피하지 않으면 위험에 처할 수 있다. 만약 댓글에 회피처리를 하지 않은 HTML이 포함된 경우, 웹 사이트의 댓글에 다른 유저들이 생각한 것과는 다른 일을 실행시킬 수 있는 `<script>` 태그를 주입할 수 있다.

- 악성 스크립트는 종종 세션 토큰을 저장하는 데 사용되는 쿠키에 접근한다. 만약 공격자가 유저의 세션 쿠키를 얻게되면, 그들은 그 유저가 될 수 있다. 때문에 유저처럼 작업을 수행할 수 있고, 유저의 민감한 데이터에 대한 권한을 얻을 수 있다. 
  > XSS 공격을 통해 쿠키를 가져오는 과정을 그린 그림
  ![steal cookies image](https://www.acunetix.com/wp-content/uploads/2012/10/how-xss-works-910x404.png)
- 스크립트는 스크립트가 실행 중인 페이지의 DOM을 임의적으로 조작할 수 있어서 공격자가 웹 사이트의 일부분에 실제로 보이는 내용을 조작할 수 있다.
- 스크립트는 AJAX를 사용해 임의의 내용이 담긴 HTTP 요청을 임의의 목적지로 보낼 수 있다. 
- 모던 브라우저의 자바스크립트는 HTML5 API를 사용할 수 있다. 예를 들어 사용자의 위치, 웹캠, 마이크, 심지어 사용자의 파일 시스템에도 접근할 수 있다. 이런 API는 대부분 사용자의 opt-in을 요구하지만, 공격자는 Social Engineering을 통해서 이런 한계도 극복할 수 있다.

## 알아두면 좋은 것
- 클라이언트에는 script를 실행시킬 수 있는 브라우저의 HTML 파서가 동작하지 않도록 `innerHTML`대신 `textContent` 하는 것이 좋다.
- 서버에서는 HTML tag에 회피 처리를 만들면 (태그를 제거하는 등) 브라우저가 사용자 입력을 HTML로 파싱할 수 없게되므로 스크립트를 실행하지 않게 할 수 있다.

## 참고 링크
- [Cross-Site Scripting Attack (XSS)](https://www.acunetix.com/websitesecurity/cross-site-scripting/)
- [Types of XSS](https://www.acunetix.com/websitesecurity/xss/)