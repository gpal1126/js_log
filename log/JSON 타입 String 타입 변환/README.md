## JSON 타입 / String 타입 변환

### * JSON 타입 객체 만들기
```
let person = new Object();
person['name'] = 'hml';
person['age'] = 20;
person['gender'] = 'female';
//{name: "hml", age: 20, gender: "female"}

let person = {
    name: 'hml',
    age: 20,
    gender: 'female'
};
//{name: "hml", age: 20, gender: "female"}
```

### * JSON -> String
- JSON.stringify() 사용  
```
const personStr = JSON.stringify(person);
//personStr, JSON -> String 변환
{"name":"hml","age":20,"gender":"female"}
```
- -> key, value가 모두 쌍따옴표("")로 감싸져서 나온다.  
  
  
### * String -> JSON
- JSON.parse() 사용  
```
const personJson = JSON.parse(personStr);
//personJson String -> JSON 변환
{name: "hml", age: 20, gender: "female"}
```
- -> key, value 값으로 출력된다.  
  
### * JSON key get
```
Object.keys(personJson)    //["name", "age", "gender"]
```

### * JSON values get
```
Object.values(personJson)    //["hml", 20, "female"]
```

### * JSON length 값
```
Object.keys(personJson).length    //3
```

## * 응용하기
- input value -> Json 형태로 push 후 String 로 변환  
```
/* input data -> Json 형태로 push 후 String으로 변환 func */
function getJsonDataFunc(typeVal){
    let typeValJson = new Object();  //객체 생성
    $(`.${typeVal}`).each(function(idx){
        if( $(this).val().trim() !== '' ){
            typeValJson[idx] = $(this).val();    //json에 data push
        }
    });
    return JSON.stringify(typeValJson);    //Json -> String
}
```
  
- String -> Json 변환 후 data input  
```
/* String -> Json 변환 후 data input func */
function jsonDataInputFunc(typeVal, strVal){
    let jsonVal = JSON.parse(strVal);    //String -> Json
    $.each(jsonVal, function(idx){
        console.log(jsonVal[idx]);
        let id = parseInt(idx) + 1;
        $(`#${typeVal}${id}`).val(jsonVal[idx]);    //해당 input에 Json data 값 출력
    });
}
```