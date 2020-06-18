## 문서의 로드 이벤트

### 1. window.onload = function(){}
- 웹페이지의 html의 로딩이 끝난 후 실행  
- 문서의 모든 요소(js, css, images, html 등...)가 로드된 후 실행  
- 하나의 문서에는 하나의 onload만 존재 :  여러 개가 사용된 경우 마지막 선언한 것이 실행  
- 웹 페이지의 이미지나 외부 파일이 로드된 후 실행되기 때문에 로딩 시간이 길어질 수 있다.  
  
​  
### 2. window.addEventListener('DOMContentLoaded', function(){ })  
- HTML과 script가 로드된 후 실행된다.  
- onload 보다는 먼저 실행  
  
​  
### 3. <body onload="">  
- window.onload와 동시에 사용 불가능 / <body onload="">를 사용하면 window.onload를 사용할 수 없다.  
  
​  
### 4. $(document).ready(function(){})  
- 외부 리소스, 이미지 로딩과 상관없이 DOM이 모두 로드된 후 실행  
- window.onload 보다 빠르다  
- 중복 사용 가능  
- 순서대로 실행  

​
### 5. $(function(){})  
- $(document).ready(function(){})의 함축형 이벤트  
- document로 보다 명확하게 명시해주기 때문에  
- $(function(){})보다 $(document).ready(function(){}) 사용하는 것이 더 좋다.  
  
​  
  
### * 스크립트는 </body> 태그 바로 이전에 선언해주는 게 좋다.
- 마지막에 스크립트를 선언해야 보다 빠르게 페이지를 로딩할 수 있다! 
- 하지만 때에 따라 위쪽에 선언해야 되는 경우가 있는데  
- 그 때는 문서의 로드 시점에 따라 처리해주면 된다!  