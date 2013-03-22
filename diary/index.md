<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>jquery</title>
<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.3.2/jquery.min.js" type="text/javascript"></script>
<script type="text/javascript">
$(document).ready(  function(){});
/*function hiden(){
$("#divObj").hide();//hide()函数,实现隐藏,括号里还可以带一个时间参数(毫秒)例如hide(500)以500毫秒的速度隐藏,还可以带slow,fast
}
function slideToggle(){
$("#divObj").slideToggle(500);//窗帘效果的切换,点一下收,点一下开,参数可以无,参数说明同上
}
function show(){
$("#divObj").show();//显示,参数说明同上
}*/
function toggle(){
$("#divObj").toggle(500);//显示隐藏切换,参数可以无,参数说明同上
}
/*function slide(){
$("#divObj").slideDown();//窗帘效果展开
}*/
</script>
</head>
<body>
<h3>div里内容的显示隐藏特效</h3>
<!--<input type="button" value="隐藏" onclick="hiden()"/>
<input type="button" value="显示" onclick="show()"/>
<input type="button" value="窗帘效果显示2" onclick="slide()"/>
<input type="button" value="窗帘效果的切换" onclick="slideToggle()"/>-->
<input type="button" value="隐藏显示效果切换" onclick="toggle()"/>
<div id="divObj" style="display:none"> 1.测试例子<br/>
  2.测试例子<br/>
  3.测试例子<br/>
  4.测试例子<br/>
  5.测试例子<br/>
  6.测试例子<br/>
  7.测试例子<br/>
  8.测试例子<br/>
  9.测试例子<br/>
  0.测试例子<br/>
</div>
</body>
</html>
