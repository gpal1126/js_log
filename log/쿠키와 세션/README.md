## 쿠키(Cookie) & 세션(Session)

### 쿠키(Cookie)
- 간단히 말해서 사용자의 정보를 클라이언트(브라우저)에서 관리하는 방법이다.  
- 프로젝트를 하면서 쿠키(Cookie)를 사용할 일이 꽤 있다.  
- 방문했던 사이트의 아이디 저장이나 자동로그인, 팝업, 장바구니 등 간단한 데이터를 관리할 수 있다.  
- 하지만 브라우저에 값이 노출되기 때문에 중요한 정보는 쿠키(Cookie)를 사용하지 않는게 좋다.  
- 쿠키(Cookie)와 비슷하지만 조금은 다른 세션(Session)이라는 기능이 있다.  

### 세션(Session)
- 사용자의 정보를 서버에서 관리하는 방법이다.  
- 서버에 저장되기 때문에 정보가 유출 되지 않고 보안상에도 좋다.  
- 세션(Session)의 예로는 대표적으로 로그인이 있다.  
- 사용자가 로그인을 하면 브라우저를 닫기 전 까지는 페이지를 이동해도 로그인이 유지된다.  


이렇게 보면 세션(Session)의 장점이 더 많은거 처럼 보인다.  
하지만, 세션(Session)은 서버에서 관리하기 때문에  
중요하지 않은 정보까지 세션(Session)을 사용하게 되면 서버 과부하가 걸린다.  
보다 가벼운 데이터 쿠키(Cookie)로, 중요한 데이터는 세션(Session)으로 나눠서 사용하는 것이 좋다.   
  
​  
세션(Session)은 서버에서 사용하는 기능이기 때문에 다른 카테고리인 Node.js에 있고,  
아래는 w3schools 에서 지원하는 쿠키(Cookie)의 자바스크립트 기반 사용 방법이다.  
  
  
### - setCookie 
```
function setCookie(cname, cvalue, exdays) {
    let d = new Date();
    d.setTime(d.getTime() + (exdays * 24 * 60 * 60 * 1000));
    let expires = "expires="+d.toUTCString();
    document.cookie = cname + "=" + cvalue + ";" + expires + ";path=/";
}
```

### getCookie
```
function getCookie(cname) {
    let name = cname + "=";
    let ca = document.cookie.split(';');
    for(let i = 0; i < ca.length; i++) {
        let c = ca[i];
        while (c.charAt(0) == ' ') {
            c = c.substring(1);
        }
        if (c.indexOf(name) == 0) {
            return c.substring(name.length, c.length);
        }
    }
    return "";
}
```

### - removeCookie
```
function removeCookie(cname) {
    setCookie(cname, '', -1)
}
```
