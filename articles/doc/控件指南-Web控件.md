**目录**

[TOC]

# 网页控件（Webcontrol）

**功能说明**

内嵌本地的html，在WebControl下新建文件夹，把本地的html文件拷贝到该文件。

**HTML5**
```html
<web:html  id="webcontrol0"  startpage="page1.html" />
```

**属性列表**

| 属性名 | 属性值 | 说明 |
| ------------ | ------------ | ------------ |
| web |   | html文件夹 |
| startpage |   | Html网页起使页 |
| bindfield |   | 扫描的结果 |

**支持公共属性**
*参见公共属性说明*

**事件列表**

| 事件名 | 说明 |
| ------------ | ------------ |
| 无 | 无 |

**支持公共事件**
*参见公共事件说明*

**实例**

1、更改起始页
```html
$id("webcontrol0").set("startpage"," page1.htm2");
```

#  Web扩展概述

## 1、什么是Web扩展

众所周知，DSL工程最终生成的是原生工程。当DSL工程本身提供的功能无法满足你的使用的时候，你可以考虑通过HTML5技术，以Web扩展的形式来满足你的开发需求。

## 2、Web扩展的分类

在Hybrid Mobile APP开发中，通过HTML5以Web技术来实现Mobile App的开发使用非常广泛。这里只讲解基于DSL工程下，如何做Web扩展。

如果你想了解如何使用HTML5技术来开发Hybrid Mobile App请使用新建web project来解决，也可参考相关的开发文档。网址在mobile.yyuap.com的文档中心上的Web开发模块。

# WebControl的使用

## 1、什么是WebControl扩展

**什么是WebControl**

一个WebControl就是一系列HTML+CSS+JavaScript等组成的一个文件夹，这个文件夹可称之为一个WebControl。

在这个文件夹内的HTML可以正确独立运行，并保证没有什么语法等错误。这些HTML可以看成是一个独立的小应用，只不过是采用HTML5 Web来开发的。

**起始页**

在这些HTML页面中有一个是起始页面，作为将来原生代码调用该WebControl时的入口页面。有点类似微信等轻应用的首页面一样。

**WebControl和DSL工程间的交互**

原生工程中的Context（业务数据）、原生设备服务、甚至原生UI控件等均可以在WebControl中调用，并且编程API和在原生的JSController中的完全一致。

## 2、使用方法

使用WebControl的前提：

1）你已经做好了HTML页面，可以正常的在Chrome或Safari等浏览器中正确运行，并且没有语法等错误。

你可以尝试在chrome等浏览器中运行看看效果。例如下图就是一个使用HTML5技术编写的一个图表功能的例子，单独在浏览器下运行的效果如下图所示：

![](http://mobile.yyuap.com/UAPMobile/UEditor/jsp/upload/image/20150805/1438761028340057270.png)

**场景假设:我们HTML图表的数据实际上是通过原生JSController访问后台获取的，如果在JSController中将获取的数据传递给HTML图表呢？**

答案是JSController通过$service.callAction或$service.get等访问后台获取数据后，放入Context中，然后在通过$js.runjs方法调用WebControl中的指定JS方法，在该JS方法中再访问Context从而获得图表所需要的数据。从而实现WebControl与加载后台数据或者原生JSController中的数据之间的通讯。

使用步骤如下：

1) 声明一个WebControl

在DSL工程中页面中，拖拽一个WebControl到页面上，可以设置WebControl合适的width和height，例如可以设置为fill、比重等.

2) 创建WebControl

a) 在DSL工程下有一个WebControl节点，鼠标右键菜单中新建一个文件夹。该文件夹的命名就是你的WebControl的名字。这里的名字没有实际含义，仅仅作为你多个WebControl时容易识别。建议你最好还是起一个有意义的名字。这样也便于你将来的代码维护。

![](http://mobile.yyuap.com/UAPMobile/UEditor/jsp/upload/image/20150805/1438761028418079492.png)

b) 建好文件夹后，拷贝你的HTML页面到这个文件夹下。这样你的WebControl就创建好了。如图所示：

![](http://mobile.yyuap.com/UAPMobile/UEditor/jsp/upload/image/20150805/1438761028465047047.png)

3) 使用WebControl

回到你要使用的WebControl的window页面，鼠标点击window上的WebControl，在属性栏中填入两个关键属性。

第一个属性是【空间名称】，通过右侧按钮可以选择你的WebControl（文件夹的名称）

第二个属性是【启示页】，通过右侧按钮可以选择一个HTML作为起始页

![](http://mobile.yyuap.com/UAPMobile/UEditor/jsp/upload/image/20150805/1438761028496086814.png)

如果你的WebControl不需要和原生JS Controller进行交互，到这一步就完成了WebControl的使用。如果你的WebControl中的HTML页面还需要访问原生（如Context、服务、控件等）则继续下面的4）

4) 原生调用WebControl中的JS方法

在JSController中，写代码

```javascript
$js.runjs({
	"controlid" : "webcontrol0",//webControl的id
	"func" : "loaddata()"//要执行位于webControl中的js方法名
})
```

实现调用指定WebControl的指定js方法，其中loaddata()是定义在WebControl起始页面的一个全局function。

以上代码通常位于在原生JSController 的onload或一个控件的事件中，例如在JSController的onload事件中调用WebControl中起始页的JS方法，从而实现WebControl的数据加载。

综上，实现了在原生JSController调用WebControl起始页的指定JS方法，剩下的逻辑就是该HMTL页面内部的逻辑了。如图所示：

![](http://mobile.yyuap.com/UAPMobile/UEditor/jsp/upload/image/20150805/1438761028543983136.png)

**新版本（V2.7及以后）只需要引用如下1个JS即可**
```html
<script language="JavaScript" src="../Frameworks/iuapmobile.native.all.js" ></script>
```
**注意引用路径是否正确，可到native目录找到文件用浏览器打开，查看引用路径是否正确
路径和WebControl中的html目录层级有关，请注意**

5) WebControl中JS方法访问原生

在WebControl的HTML页面中可以调用与原生JSController中的一致，API可参考mobile.yyuap.com文档中心。需要强调的一点就是，在你的HTML中务必要引用必要的JS。为保险起见，你可以引用所有的JS，如图所示

![](http://mobile.yyuap.com/UAPMobile/UEditor/jsp/upload/image/20150805/1438761028731034198.png)

**新版本（V2.7及以后）只需要引用如下1个JS即可**
```html
<script language="JavaScript" src="../Frameworks/iuapmobile.native.all.js" ></script>
```
**注意引用路径是否正确，可到native目录找到文件用浏览器打开，查看引用路径是否正确
路径和WebControl中的html目录层级有关，请注意**

**【小技巧】你可以在当前dsl工程下的\native\android\工程名\assets\loads下打开一个html，将他的<script></script>引用部分复制到你的WebControl的HTML中**。如下图所示

![](http://mobile.yyuap.com/UAPMobile/UEditor/jsp/upload/image/20150805/1438761028809049482.png)

**新版本（V2.7及以后）只需要引用如下1个JS即可**
```html
<script language="JavaScript" src="../Frameworks/iuapmobile.native.all.js" ></script>
```
**注意引用路径是否正确，可到native目录找到文件用浏览器打开，查看引用路径是否正确
路径和WebControl中的html目录层级有关，请注意**

例如：在WebControl的HTML的JS方法中可以有如下代码

```javascript
$ctx.getJSONObject()
$ctx.push(json)
$camera.open({
	bindfield : "xxxfieldName",
	callback : "mycallback()"
})

var val = $id("button0").get(attrName);
$id("button0").set(attrName, value);
```

例如：下图说明了在WebControl中通过访问Context获得图表所需要的数据。

![](http://mobile.yyuap.com/UAPMobile/UEditor/jsp/upload/image/20150805/1438761028543983136.png)

## 3、常见QA

**Q：JSController如何与WebControl进行通讯调用？**

A：在JSController中使用$js.runjs()来调用WebControl中的JS方法

在WebControl中的HTML加载和原生JSController的JS加载是异步的，所以不能在WebControl的HTML中直接通过$ctx.getJSONObject()来访问Context，所以一定要有JSController来调用之，因为在JSController才能控制是否已经加载数据至Context。

JSController可以将数据放入Context、本地存储中，再在WebControl的方法中通过相应的API进行获取即可实现原生JSController与WebControl之间的数据通讯。

**Q：和JQueyr的ready方法中能否访问Context

A：不能，因为HMTL中JQuery的ready方法仅仅表示HTML中的DOM加载完毕，不能说明JSController中的Context加载完毕。但是与JSController无关的逻辑当然可以放在JQuery的ready方法里。

**Q：WebControl中怎么访问Context怎么进行服务调用？**

A：书写的代码和JSController的代码一样，及$ctx.getJSONObject()、$camera..open()等等。

只要注意写这些代码的时机即可，一定要在JSController的onload之后才能调用。

**Q：WebControl中如何对后台进行访问？**

A：书可以通过$service.callAction、$service.get、$service.post发起请求来访问后台。写法与JSController一样，强大且方便吧：）

**Q：WebControl中能不能使用HTML本身的AJAX对后台进行访问？**

A：可以。但是需要解决跨域问题。因为WebControl的HTML本身实在原生中的，如果是原生发起后台请求不存在跨域。使用AJAX请求，相当于绕过了原生系统直接对后台请求，所以需要解决跨域问题。可以通过JSONP或者通过后台代码设置response的来解决跨域问题。可以上网搜一下AJAX跨域解决方法参考一下。

# WebView的使用

WebView是什么？请问度娘，这里就不作回答了。

## 1、使用方法

通过Studio的控件工具栏，拖拽一个WebView控件，设置器网址属性即可使用。

详细用法参见mobile.yyuap.com文档中心。

适应范围：

（1）要加载的URL的HTML相对独立，即HTML的逻辑部分都独立完成

和本身的DSL工程没有太多的交互。

（2）适合集成现有web资源，例如已经在运行的WebSite等。

***更多文档查看【DSL开发指导】-【原生与H5数据交互】***
