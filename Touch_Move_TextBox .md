Touch_Move_TextBox
==================
Multitouch.inputMode = MultitouchInputMode.TOUCH_POINT;

var array:Array ;
var where:Number = 0;
var begin:Number = 0;
var end:Number = 0;
var timer:Timer = new Timer(1);

stage.addEventListener(TouchEvent.TOUCH_BEGIN, f3f1);
stage.addEventListener(TouchEvent.TOUCH_END, f3f2);

function f3f1(event:TouchEvent):void{
	removeEventListener(Event.ENTER_FRAME,f3f5);
	stage.addEventListener(TouchEvent.TOUCH_MOVE,f3f3);
	timer.start();
	array = new Array();
	array.push(event.stageY);
	begin = event.stageY;}


function f3f2(event:TouchEvent):void{
	timer.stop();
	end = event.stageY;
	if(timer.currentCount >= 5 && timer.currentCount <= 100 && Math.abs(end - begin) > 10){addEventListener(Event.ENTER_FRAME,f3f5);}
	if(timer.currentCount <= 30 && Math.abs(end - begin) < 10){removeEventListener(Event.ENTER_FRAME,f3f5);}
	timer.reset();
	stage.removeEventListener(TouchEvent.TOUCH_MOVE,f3f3);}
	

function f3f3(event:TouchEvent){
	array.push(event.stageY);
	if(array[1] > array[0]){where = 100/ (timer.currentCount/10)}
	if(array[0] > array[1]){where = -100/(timer.currentCount/10)};
	where = 2 * Math.floor(where/2)
	if(myObject.y <= 32 && myObject.y >= -4293){myObject.y = myObject.y + array[1] - array[0];}
	if(myObject.y > 32){myObject.y =32}
	if(myObject.y < -4293){myObject.y = -4293}
	array.shift();}

function f3f5(e:Event){
	if(where > 0){where -= 2}
	if(where < 0){where += 2}
	if(myObject.y > 32){myObject.y =32}
	if(myObject.y < -4293){myObject.y = -4293}
	if(myObject.y <= 32 && myObject.y >= -4293){myObject.y +=where;}
	if(where == 0){removeEventListener(Event.ENTER_FRAME,f3f5);}}
