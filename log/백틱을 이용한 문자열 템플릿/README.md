## 백틱(`) 이용한 문자열 템플릿

### * 기존  ES5 이용
- 기존에는 큰 따옴표나 작은 따옴표로 변수에 +를 이용한 문자열 병합으로 처리했기 때문에 코드가 지저분하고 헷갈렸다.  
```
var deviceType;
var fileName;
var readFileUrl = "views/"+deviceType"+/users/"+fileName+".html";
```

### * 문자열 템플릿 안에 백틱(`)을 이용한 문자열 처리 - ES6
- 백틱을 이용하여 ${}으로 변수를 처리 하기때문에 코드가 깔끔해졌다.  
```
let deviceType;
let fileName;
const readFileUrl = `views/${deviceType}/users/${fileName}.html`;
```
