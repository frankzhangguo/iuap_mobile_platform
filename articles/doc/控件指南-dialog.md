**目录**

[TOC]

# 对话框（Dialog）

对话框是页面的一种形态，和Window关系密切。
可在工程或UI下的Window目录上右击创建一个Dialog。

**属性列表**

| 属性名 | 属性值 | 说明 |
| ------------ | ------------ | ------------ |
| 无 | 无 | 无 |

**事件列表**

| 事件名 | 说明 |
| ------------ | ------------ |
| onbackpressed | 按下回退键时触发，仅Android支持 |
| onkeydown | 按下回退键时触发，仅Android支持 |

# 对话框使用

## 1、Window页面弹出Dialog及回调

**语法**
```javascript
var newDialog = $window.showModalDialog({
	dialogId : "字符串", // 形如”com.yyuap.test.Dialog1”, Dialog的包名+类名
	arguments : "JSON",
	features : "JSON",
	callback : "JS方法"
});
```

**说明**
1、showModelDialog的时候都会自动创建一个Dialog实例；
2、dialogId是Dialog定义时的全类名，即包名+dialog的id，在showModalDialog的时候，系统会根据dialogId自动实例化一个新的dialog Dialog实例。
3、$window是JS框架封装提供的全局对象，职责为用来访问管理当前页面级对象及操作。
4、callbck是关闭dialog后主页面要执行的JS方法，通常callback用来处理dialog的返回值

**示例**
```javascript
var newDialog = $window.showModalDialog({
	"dialogId" : "com.yyuap.contact.Dialog1",
	"animation-type" : "right", //left|bottom|top|right|center弹出的起始方向
	"arguments" : {
		"name" : "张三",
		"code" : "C001"
	}, //支持形如： arguments :”xxxxx”
	"features" : {
		"dialogLeft" : 123,
		"dialogTop" : 200, //从右边弹出到（123，200）处
		"dialogWidth" : 300, //如设置此参数则弹窗页面设置大小无效
		"dialogHeight" : 400 //如设置此参数则弹窗页面设置大小无效
	},
	callback : "mycallback()"
});
function mycallback(sender, args) {//args就是返回值
	args = $stringToJSON(args);
	var x = args.x;
	//x的值为字符串 123
	var y = args.y;
	//y的值为JSON对象{a:1,b:2}
}
```

## 2、Dialog窗体接受参数

Dialog窗体创建

在工程的window上右击新建—〉dialog，dialog上需要什么元素，与window一样绘制即可
![](http://mobile.yyuap.com/UAPMobile/UEditor/jsp/upload/image/20150608/1433729247624005224.png)

**语法**
接收参数必须为arguments，具体下面哪个方法接收由arguments类型决定
_ $param.getJSONObject("arguments");_
_$param.getString("arguments");_

**示例**
```javascript
/*Dialog页面onload的时候可以获取传入参数*/
var param = $param.getJSONObject("arguments");//获取父窗体传递的参数字符串形式
alert("您传递的参数为：" + param);//弹出结果为字符串{"name":"张三"，"code","C001"}
alert($stringToJSON(param).name)//弹出结果为"张三"
```

## 3、Dialog的关闭及返回值

**语法**
```javascript
$window. close ()
$window. close ({…})
```

**说明**
1、Dialog有自己的JSController
2、在JSController中，通过close方法关闭自己
3、close方法的参数 是可选的， 可以是一个JSONObject

**示例1**
```javascript
$window.close({
	type : “JSON”,
	tata : {x:1,y:2}
});
```

**示例2**
```javascript
$window.close({
	type : ”String”
	data : {x:1,y:2}
});
```

**示例3**
```javascript
$window.close({
	“x” : “123”,
	“y” : {a:1,b:2}
});
```


