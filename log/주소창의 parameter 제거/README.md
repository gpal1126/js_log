## 주소창에서 parameter 값 제거하기

### - 실행 전 
- http://localhost:3000/main?param=1  
- 주소창에 parameter 값 제거  
```
history.replaceState({}, null, location.pathname);
```


### - 실행 후
- http://localhost:3000/main  

