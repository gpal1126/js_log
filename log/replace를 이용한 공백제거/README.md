## replace를 이용한 공백 제거

### * 모든 공백 제거
- \s : 공백  
```
let str = '   abc    def   ';
str = str.replace(/\s*/g, '');
//str = str.replace(/\s/g, '');
//'abcdef'
```

### * 앞에 공백 제거
- ^ : 앞  
- \s* : 모든 공백  
```
let str = '   abc    def   ';
str = str.replace(/^\s*/g, '');
//'abc    def   '
```
  
  
### * 뒤에 공백 제거
- $ : 뒤  
- \s* : 모든 공백    
```
let str = '   abc    def   ';
str = str.replace(/\s*$/g, '');
//'   abc    def'
```