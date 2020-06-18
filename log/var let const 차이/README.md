## var, let, const 차이

### * 리터럴 : 할당된 값
```
let color = "RED";	//RED라는 값이 리터럴을 뜻함
```

### * 'use strict' 엄격 모드 
- js에 맨 위에 선언하여 보다 엄격적으로 문법 검사를 한다.  
```
'use strict'
```


### * var : function scope 변수, 재선언 가능, 재할당 가능  
```
var vName;				//먼저 선언하고 나중에 값 할당해도 된다.
var vName = "name1";
var vName = "name2";	//재선언 가능
vName = "name3";		//재할당 가능
```
  
#### - function 안에서 유효범위가 된다!  
```
var vName='vName'
function sayVName() {  //vName
  var vName='vName in function';
  console.log(vName);  //vName in function
}

sayVName();          //vName in function
console.log(vName);  //vName
```
#### - 미리 선언한 전역변수 값이 아닌 재선언한 값이 출력 된다.  
```
var vName='vName!';   //전역 변수 선언
{
  var vName='scope vName'; 
  console.log(vName); //scope vName
}
console.log(vName);   //scope vName
```
  
  
### * let : block scope 변수, 재선언 불가, 재할당 가능  
```
//var와 마찬가지로 먼저 선언하고 나중에 값을 할당해도 된다.
let lName;	
let lName = "name1";	
let lName = "name2";	//재선언 하면 syntax 에러 발생.. Identifier 'lName' has already been declared
lName = "name3";		//재할당 가능
```
  
#### - block scope 안에서만 유효범위가 된다!
```
let lName='lName';
{
  let lName='scope lName'; 
  console.log(lName); //scope lName
}
console.log(lName); //lName
```
  

### * const : block scope 상수,선언과 동시에 값 할당, 재선언 불가, 재할당 불가
```
//선언과 동시에 값을 할당해야 된다. syntax 에러 발생.. Uncaught SyntaxError: Missing initializer in const declaration
const C_NAME;	
const C_NAME = "name1";
const C_NAME = "name2";	//재선언 불가 syntax 에러 발생.. Identifier 'C_NAME' has already been declared
C_NAME = "name3";		//재할당 불가 TypeError: Assignment to constant variable.
```
  
#### -  block scope 안에서만 유효범위가 된다!
```
let C_NAME='C_NAME';
{
  let C_NAME='scope C_NAME'; 
  console.log(C_NAME); //scope C_NAME
}
console.log(C_NAME); //C_NAME
```
#### - * 변수와 상수를 구별하기 위해 const는 대문자와 언더스코어(_)를 이용한다!
