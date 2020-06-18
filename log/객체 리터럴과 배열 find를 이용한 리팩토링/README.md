## 객체 리터럴과 배열 find를 이용한 view routes 리팩토링  

### * 예전 switch 문 이용  
```
const urlParamId = req.params.id;  //넘어온 url id
let fileName;               //파일명

switch(urlParamId){
    case 'joinUser':        //유저 가입 페이지
        fileName = 'u_join_user';
        break;
    case 'userInfo':        //유저 정보 페이지
        fileName = 'u_info_user';
        break;
   .... 생략
}//switch
```

### * 객체 리터럴과 배열 find를 이용한 리팩토링  
```
const urlParamId = req.params.id;  //넘어온 url id
let fileName;               //파일명

//객체 리터럴로 urlParamId 값과 파일명 매핑
const objUrlId = {
    'joinUser' : 'u_join_user',             //유저 가입 페이지
    'userInfo' : 'u_info_user',             //유저 정보 페이지
    .... 생략
}

//Object.entries(objUrlId) : 객체 -> 배열
fileName = Object.entries(objUrlId).find(function(v){   //객체를 배열로 변환하여 찾음
    //console.log(v[0]);    //index 0은 urlParamId
    //console.log(v[1]);    //index 1은 파일명
    return v[0] === urlParamId;  //배열 값과 넘어온 urlParamId 값과 비교
})[1];
```
