## base64 이미지 File 정보로 변환

- 이미지 crop 기능을 사용하면서 base64로 출력되었다.  
- 파일 업로드 모듈인 multer를 사용하려면 File 정보가 필요한데   
- base64 -> File Obj로 변환해주는 function이 필요해서 아래를 사용하였다.  

### - base64ToFileObj(base64 데이터, 'fileName');
```
function base64ToFileObj(dataurl, filename) {
    let arr = dataurl.split(','), mime = arr[0].match(/:(.*?);/)[1],
        bstr = atob(arr[1]), n = bstr.length, u8arr = new Uint8Array(n);
    while(n--){
        u8arr[n] = bstr.charCodeAt(n);
    }
    return new File([u8arr], filename, {type:mime});
}
```

