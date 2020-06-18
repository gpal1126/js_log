## * 1분 타이머 설정 구현하기  

```
let timer;
function timerFunc(){
		
    //let hour = 0;
	let minute = '0'+1; 
	let second = '0'+0;
		
	//$('.countTimeHour').html(hour);
	$('.cntMinute').html(minute);
	$('.cntSecond').html(second);
	timer = setInterval(function(){
		//$('countTimeHour').html(hour);
		$('.cntMinute').html(minute);
		$('.cntSecond').html(second);
		
		if( second == 0 && minute == 0 /*&& hour == 0*/ ){
            console.log('타이머 end');
			clearInterval(timer);   //타이머 초기화				
			return false;
		}else {
			
			//초 감소
			second--;
			
			//분 카운트 
			if( second < 0){
				minute--;
				second = 59;
			}else if( second < 10 ){ //초를 두자리로 만들기 위해(초가 10보다 작으면 앞에 0을 붙임)
				second = '0'+second--;
			}//if 
				
			//분을 두자리로 만들기 위해
			if( minute < 10) {	//분이 10보다 작으면 앞에 0을 붙임 
				minute = '0'+minute--;
			}//if
				
			/*
			//시간 카운트
			if(minute < 0){
				if(hour>0){
					hour--;
					minute=59;
				}//if
			}//if 
			*/
		}//if
	}, 1000);
}
```
