## HTML include 

프로젝트를 진행하면서 header, footer 등 공통적인 부분을 include 할 일이 생겼다.  
우선 include는 쉽게 말해서 부모 HTML 안에 자식 HTML을 넣는 것이다.  
아래는 HTML을 include할 수 있는 function이다.  
이 function을 이용해서 HTML을 include 해보자!  
  
  
### - includeHTML.js
- include-html 속성을 사용해서 해당 html을 include 할 예정!  
```
function includeHTML(cb) {
    var z, i, elmnt, file, xhttp;
    z = document.getElementsByTagName("*");
    for (i = 0; i < z.length; i++) {
      elmnt = z[i];
      file = elmnt.getAttribute("include-html");
      if (file) {
        xhttp = new XMLHttpRequest();
        xhttp.onreadystatechange = function() {
          if (this.readyState == 4 && this.status == 200) {
            elmnt.innerHTML = this.responseText;
            elmnt.removeAttribute("include-html");
            includeHTML(cb);
          }
        }      
        xhttp.open("GET", file, true);
        xhttp.send();
        return;
      }
    }
    if (cb) cb();
}
```
  

### - header.html(자식)
```
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <script src="/js/jquery.min.js"></script>	<!-- npm jquery -->
</head>
<body> 
    ..생략
    <div class="child"></div>
</body>
</html> 
```
  
  
### - main.html(부모)
- 그리고 부모 HTML에서 자식 HTML을 include 한다.  
- 방법은 아래와 같다.  
    - 1. HTML에서 위의 includeHTML.js를 import  
    - 2. include할 자식 HTML   
    - 3. includeHTML() 함수 호출  
```
<script type="text/javascript" src="/js/common/includeHTML.js"></script>	<!-- includeHTML js -->
<section class="header-html" include-html="/views/web/subpage/header.html"></section>
<script>includeHTML();</script> 	<!-- HTML include functon 호출 -->
<script type="text/javascript" src="/js/web/common.js"></script> <!-- common js -->

... 생략
```
#### - 결과  
- 이렇게 하면 부모 HTML에 자식 HTML이 포함되어 잘 출력된다!  
- 출력은 잘되지만 자식 HTML 안에 있는 태그 값들을 selector 할 수 없다...ㅠ   
  
​  
### - common.js
```
$(function(){
    //부모 HTML 안의 태그는 selector 잘됨
    console.log($('.header-html').attr('class')); //header-html 
    //자식 HTML 안의 태그는 selector 안됨....
    console.log($('.child').attr('class'));       //undefined....
    
    //on을 이용한 function은 사용 가능
    //$(부모HTML 태그).on('click', '자식HTML 태그')....
    $('.header-html').on('click', '.child', function(){
        //생략....
    });
});
```
  
  
### - 그땐 부모 HTML에서 사용할 js import 시 script 태그에 async 속성을 넣어주면 된다! selector도 아주 잘 된다!
- async : 스크립트 즉시 사용  
```
<body>
    ....생략
    <section class="header-html" include-html="/views/web/subpage/header.html"></section>
    ...생략

    <!-- 스크립트는 </body> 태그 바로 위에 선언해야 html이 보다 빠르게 로딩됨! -->
    <script type="text/javascript" src="/js/common/includeHTML.js"></script>	<!-- includeHTML js -->
    <script>includeHTML();</script> 	<!-- HTML include functon 호출 -->
    <script type="text/javascript" src="/js/web/common.js" async></script> <!-- common js	async: 스크립트 즉시 사용, includes된 html의 js도 사용 가능 -->
</body>
```

하지만 다수의 html 을 include시 selector가 먹지 않는 경우가 발생했다....  
그래서 부모 HTML과 common.js 를 수정 하였다.  

### - 부모 HTML
- 기존 소스는 아래에서 script를 모두 호출 하였다.  
- 하지만 변경한 소스는 맨위에 includeHTML.js 를 선언하고   
- include할 자식 html 아래에 includeHTML() 함수를 같이 호출하였다.  
```
<body>
    <!-- includeHTML js -->
    <script type="text/javascript" src="/js/common/includeHTML.js"></script>	

    ....생략
    <section class="header-html" include-html="/views/web/subpage/header.html"></section>
    <script>includeHTML();</script> 	<!--HTML include functon 호출-->
    ...생략
    <section class="footer-html" include-html="/views/web/subpage/footer.html"></section>
    <script>includeHTML();</script> 	<!--HTML include functon 호출-->
    ...생략

    <!-- 스크립트는 </body> 태그 바로 위에 선언해야 html이 보다 빠르게 로딩됨! -->
    <script type="text/javascript" src="/js/web/common.js" async></script> <!-- common js	async: 스크립트 즉시 사용, includes된 html의 js도 사용 가능 -->
</body>
```

### - common.js
- window.onload function으로 변경해주었다.  
- 아마 실행순서 때문에 그런거 같다.  
- 기존 $(function(){}); 는 브라우저가 DOM 트리를 생성한 직후 실행  
- 변경된 window.onload function 는 HTML 로딩이 끝난 후에 실행  
```
window.onload = function (){
    //부모 HTML 안의 태그는 selector 잘됨
    console.log($('.header-html').attr('class')); //header-html 
    //자식 HTML 안의 태그는 selector 잘됨....
    console.log($('.child').attr('class'));       //child....
    
    //on을 이용한 function은 사용 가능
    //$(부모HTML 태그).on('click', '자식HTML 태그')....
    $('.header-html').on('click', '.child', function(){
        //생략....
    });
};
```
- -> selector 도 잘되고 아직까진 문제없이 돌아간다!


## -------------------------------------------------------------------- 추가
- window.onload를 사용하면서 image crop 관련 js 와 충돌이 생겼다. 아마  로드 시점이 안맞는 문제 때문인거 같다.  
- 그래서 window.onload보다 로딩이 좀 더 빠른 window.addEventListener() 이벤트를 사용하여 문제점을 해결했다.  
- window.addEventListener() : HTML, script 로딩 후 실행  

### - common.js
```
window.addEventListener('load', function(){
    //부모 HTML 안의 태그는 selector 잘됨
    console.log($('.header-html').attr('class')); //header-html 
    //자식 HTML 안의 태그는 selector 잘됨....
    console.log($('.child').attr('class'));       //child....
    
    //on을 이용한 function은 사용 가능
    //$(부모HTML 태그).on('click', '자식HTML 태그')....
    $('.header-html').on('click', '.child', function(){
        //생략....
    });
};
```

### - 부모 HTML
- includeHTML.js 위 쪽에 선언  
- window.addEventListener() 이벤트를 사용하니 includeHTML() 메서드를 아래에서 한번만 호출해도 된다!  
- common.js 선언시 async 속성은 때에 따라 넣어준다.  
```
<body>
    <!-- includeHTML js -->
    <script type="text/javascript" src="/js/common/includeHTML.js"></script>	

    ....생략
    <section class="header-html" include-html="/views/web/subpage/header.html"></section>

    ...생략
    <section class="footer-html" include-html="/views/web/subpage/footer.html"></section>
    ...생략

    <!-- 스크립트는 </body> 태그 바로 위에 선언해야 html이 보다 빠르게 로딩됨! -->
    <script type="text/javascript" src="/js/web/common.js"></script> <!-- common js -->
    <script>includeHTML();</script> 	<!--HTML include functon 호출-->
</body>
```

### 참고 : [w3schools.com](https://www.w3schools.com/howto/howto_html_include.asp)
