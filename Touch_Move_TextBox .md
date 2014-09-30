Touch_Move_TextBox
==================
/*creat movie clip and add text field in that. movie clip neme = txt

*/

Multitouch.inputMode = MultitouchInputMode.TOUCH_POINT;

var array:Array ;
var where:Number = 0;
var begin:Number = 0;
var end:Number = 0;
var timer:Timer = new Timer(1);

stage.addEventListener(TouchEvent.TOUCH_BEGIN, f_begin);
stage.addEventListener(TouchEvent.TOUCH_END, f_end);


function f_begin(event:TouchEvent):void{
	removeEventListener(Event.ENTER_FRAME,f_motion);
	stage.addEventListener(TouchEvent.TOUCH_MOVE,f_move);
	timer.start();
	array = new Array();
	array.push(event.stageY);
	begin = event.stageY;}


function f_end(event:TouchEvent):void{
	timer.stop();
	end = event.stageY;
	if(timer.currentCount >= 2 && timer.currentCount <= 150 && Math.abs(end - begin) > 20){addEventListener(Event.ENTER_FRAME,f_motion);}
	if(timer.currentCount <= 20 && Math.abs(end - begin) <= 20){removeEventListener(Event.ENTER_FRAME,f_motion);}
	timer.reset();stage.removeEventListener(TouchEvent.TOUCH_MOVE,f_move);}
	

function f_move(event:TouchEvent){
	array.push(event.stageY);
	if(array[1] > array[0]){where =  (end - begin)/(timer.currentCount)};
	if(array[0] > array[1]){where =  (end - begin)/(timer.currentCount)};
	where =Math.round(where);
	if(where >= 100){where = 100}else
	if(where <= -100){where = -100}
	if(txt.y <= 20 && txt.y >= -txt.height + 450){txt.y = txt.y + array[1] - array[0];}
	if(txt.y > 20){where = 0;txt.y =20;}
	if(txt.y < -txt.height + 450){where = 0;txt.y = -txt.height + 450;}
	array.shift();}


function f_motion(e:Event){
	if(where > 0){where -= 1}else
	if(where < 0){where += 1}
	if(txt.y > 20){where = 0;txt.y =20;}
	if(txt.y < -txt.height + 450){where = 0;txt.y = -txt.height + 450;}
	if(txt.y <= 20 && txt.y >= -txt.height + 450){txt.y +=where;}
	if(where == 0){removeEventListener(Event.ENTER_FRAME,f_motion);}}
