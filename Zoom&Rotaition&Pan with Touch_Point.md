Zoom&Rotaition&Pan with Touch_Point
==================
/*create your movie clip and named  =  pic  */


var points:Array = new Array();
var array_rotate:Array = new Array();
var array_scale:Array = new Array();
var array_positionx:Array = new Array();
var array_positiony:Array = new Array();
var dis:Number = 0;
var rotate:Number = 0;


stage.addEventListener(TouchEvent.TOUCH_BEGIN, onTouchBegin); 
function onTouchBegin(e:TouchEvent) {
		var b:MovieClip = new _oval();
		b.x = e.stageX;
		b.y = e.stageY;
		b.name = String(e.touchPointID);
		addChild(b);
		points.push(b);
		array_rotate = new Array();
		array_scale = new Array();
		array_positionx = new Array();
		array_positiony = new Array();}

stage.addEventListener(TouchEvent.TOUCH_MOVE, onTouchMove);
function onTouchMove(e:TouchEvent) {
	if(points.length == 1 ){
	array_positionx.push(e.stageX);
	array_positiony.push(e.stageY);
		if(array_positionx.length >=2){
		pic.x = pic.x + array_positionx[1] - array_positionx[0];
		pic.y = pic.y + array_positiony[1] - array_positiony[0];
		array_positionx.shift();
		array_positiony.shift();}}else
	if(points.length == 2){
		for(var i:int = 0;i<points.length;i++){
			if(points[i].name == String(e.touchPointID)){
				points[i].x = e.stageX;
				points[i].y = e.stageY;}}
		twoPoint();
		twoPointzoom();
		twoPointrotate();}}

function twoPoint(){
	array_positionx.push((points[0].x + points[1].x)/2);
	array_positiony.push((points[0].y + points[1].y)/2);
	if(array_positionx.length >= 2){
	pic.x = pic.x + array_positionx[1] - array_positionx[0];
	pic.y = pic.y + array_positiony[1] - array_positiony[0];
	array_positionx.shift();
	array_positiony.shift();}}

function twoPointzoom(){
	dis = Math.sqrt(((points[0].x - points[1].x)*(points[0].x - points[1].x))+((points[0].y - points[1].y)*(points[0].y - points[1].y)));
	array_scale.push(2 * dis/650);
	if(array_scale.length >= 2){
	if(pic.scaleX <= 3 && pic.scaleX >= .4){pic.scaleX = pic.scaleX + array_scale[1] - array_scale[0];
	pic.scaleY = pic.scaleY + array_scale[1] - array_scale[0];}
	if(pic.scaleX > 3){pic.scaleX = 3;pic.scaleY = 3}else 
	if(pic.scaleX < .4){pic.scaleX = .4;pic.scaleY = .4}
	array_scale.shift();}
}

		
function twoPointrotate(){
	rotate = Math.atan2((points[1].y - points[0].y) , (points[1].x - points[0].x));
	array_rotate.push(180 * rotate /Math.PI);
	if(array_rotate.length >=2){
	pic.rotation = pic.rotation + array_rotate[1] - array_rotate[0];
	array_rotate.shift();}
}


stage.addEventListener(TouchEvent.TOUCH_END, onTouchEnd);
function onTouchEnd(e:TouchEvent){
	for(var i:int = 0;i<points.length;i++){
	if(points[i].name == String(e.touchPointID)){
	removeChild(points[i]);
	points.splice(i,1);}}
	if(points.length == 1){
		array_rotate = new Array();
		array_scale = new Array();
		array_positionx = new Array();
		array_positiony = new Array();}
	if(points.length == 0){array_positionx = new Array();array_positiony = new Array();}}
