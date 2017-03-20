**目录**

[TOC]

# 公共JavaScript使用

**公共JavaScript（以下简称JS）**：公共JS是指把页面的一些公有JS逻辑提取出来形成一个JS文件，便于代码复用，其定义方法和标准JS相同。

## 1、创建JS文件

如果一个项目中有一些公共的逻辑代码或工具方法，我们可以页面对应的JS之外创建的公共JS文件（如下图）。
![](http://mobile.yyuap.com/UAPMobile/UEditor/jsp/upload/image/20150409/1428564509178012375.jpg)

在controller上右击，选择新建-文件，输入com.demo.StringUtil.js，点完成，如下图：
![](http://mobile.yyuap.com/UAPMobile/UEditor/jsp/upload/image/20150409/1428564509256080795.jpg)

## 2、编辑JS文件

在JS文件中定义一个方法，代码如下：
```javascript
//JavaScript Framework 2.0 Code

// 声明一个命名空间
Type.registerNamespace('com.demo.StringUtil');

// 在此命名空间下声明方法：判断字符串是否为空
com.demo.StringUtil.isEmptyString = function(param){
	if (param == null || typeof(param) == 'undefined' || param == ''){
		return true;
	}
	return false;
}
```

注：方法最好在命名空间下定义，否则容易引起方法名冲突等问题。

## 3、导入JS文件

在Window的组件列表中点击增加，弹出组件增加对话框（如下图），选择类型text/javascript，然后选择刚才创建的样式文件。
![](http://mobile.yyuap.com/UAPMobile/UEditor/jsp/upload/image/20150409/1428564509412058707.jpg)

## 4、使用公共JS中的方法

此时在引入com.demo.StringUtil.js的页面JS中就可以使用isEmptyString方法了，代码如下：
```javascript
function com$demo$New_window1Controller$button0_onclick(sender, args){
	var str = $id("button1").get("value");
	var isEmptyString = com.demo.StringUtil.isEmptyString(str);
}
```

