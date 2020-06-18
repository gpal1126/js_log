## 객체(Object)

### 원시타입
- 단 하나의 값만 나타낼 수 있다(불변)  
- 문자열, 숫자, 불리언, null, undefined, 심볼  

### 객체
- 여러 가지 값이나 복잡한 값을 나타낼 수 있다.  
- 본질은 컨테이너(컨테이너의 내용물은 바뀔 수 있지만, 컨테이너가 바뀌지는 않는다.)  
  
  
### ​- obj에 저장된 객체를 수정했지만, 항상 같은 객체를 가리키고 있다.  
    - 즉, obj는 항상 같은 객체를 가리키고, 바뀐 것은 객체의 프로퍼티이다!  
``` 
//객체 선언
const obj = {};

//color="red"(객체의 컨텐츠)는 객체의 프로퍼티 or 멤버
obj.color = "red";    //.을 이용한 멤버 접근 연산자
obj["color"] = "blue";    //[]을 이용한 멤버 접근 연산자
obj["a color"] = "white"; //[]을 이용한 멤버 접근 연산자
```


### - num1과 num2는 같은 원시 값이지만, obj1과 obj2는 서로 다른 객체 이다.  ​
```
const num1 = 3;

const num2 = 3;

const obj1 = {
    name: 'muram',    //프로퍼티
    age: 9,
};

const obj2 = { name: 'muram', age: 9 };
```

  
### - 객체에 객체를 담을 수 있다.  
```
const obj3 = {
    name: 'muram',    //프로퍼티
    age: 9,
    detailInfo: {    //객체도 프로퍼티가 될 수 있다.
        gender: 'F',
        height: 160,
    }
};
```
  
  
### - 객체에 함수를 담을 수 있다.  
```
//객체에 함수를 담을 수 있다.
obj3.walk = function() { return "one step"; };

obj3.walk();    //함수 호출

//delete 연산자를 이용한 프로퍼티 삭제
delete obj3.walk;
```

