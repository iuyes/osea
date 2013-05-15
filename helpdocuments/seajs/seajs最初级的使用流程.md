For： seajs 2.0版本  

##《五步简单上手seajs的使用》

*    使用人群：需要快速了解seajs的功能并需要快速获得seajs上手假象快感的人。  
*    内容精要：基本的CommonJS模块结构和语法，页面如何引入seajs，seajs.use的基本使用  

###正文：  
####第一步：建立自己的测试目录  
目录可以随便取个名字。这里把建立自己的测试目录作为一步是想说明：学会在自己的电脑上创建合理的目录是一个非常有益的习惯。
我创建了一个测试目录E:\test\seajs，之后下载的seajs代码和自己编写的代码文件都将在这个目录里面。
![image](https://raw.github.com/klvoek/osea/master/images/seajs-primary-usage-1.jpg)
####第二步：获取seajs。  
获取一份seajs的代码（从官网找到seajs的下载，或者从github直接下载），下载后将dist目录中的sea.js文件复制到自己的测试目录中  
####第三步：编写自己的seajs CMD module(吐槽：到后来你就会发现你已经不能理解什么是AMD了)
先介绍一下定义seajs CMD module的经典代码结构  

    define(function (require, exports, module) {
		var mymodule = // 模块实现代码
		
		module.exports = mymodule;
	})
然后就需要构思自己要实现一个具有怎样功能的seajs CMD module了，经过慎重思考我打算这里实现一个能够在页面上指定ID的div中输出文字的工具。如果你不使用本文档中的代码，而是设计了自己想要实现的模块话，请不要依赖任何外部库，比如常见的使用jQuery操作DOM元素,否则这篇文章是帮不了你的。在确定了要实现的功能之后根据功能特点给自己的模块起一个霸气的名字：mywriter。然后在测试目录下创建对应的脚本文件，注意文件的名称就是模块的名称。  

mywriter的实现代码  

	define(function (require, exports, module) {
		var mywriter = {
			'write': function (divid, str) {
				var div = document.getElementById(divid);
				if (div) {
					div.innerText = str;
				}
			}
		};
		
		module.exports = mywriter;
	})
这个模块的代码实现正确吗？有效果吗？效果是什么样子的？
####第四步：编写测试的html页面  
在有了自己的seajs CMD module之后，迫不及待的就是创建一个测试html页面来验证自己的实现。我们在测试目录中创建一个测试页面test.html。页面的html结构如下：

	<html>
	<head>
		<title>测试</title>
		<style>
			.div{width:200px; height: 30px; margin:20px; color: gray; line-height: 30px; text-align: center;}
			.bdiv{background:black;}
			.ydiv{background:yellow;}
			.gdiv{background:green;}
		</style>
	</head>
	<head>
		<div>
			<div id="div1" class="div bdiv"></div>
			<div id="div2" class="div ydiv"></div>
			<div id="div3" class="div gdiv"></div>
			<div id="div4" class="div bdiv"></div>
		</div>
	</head>
	</html>
然后就是在页面上引入seajs脚本，并使用seajs.use引入我们开发的模块并对模块进行使用：

	<html>
	<head>
		<title>测试</title>
		<style>
			.div{width:200px; height: 30px; margin:20px; color: gray; line-height: 30px; text-align: center;}
			.bdiv{background:black;}
			.ydiv{background:yellow;}
			.gdiv{background:green;}
		</style>
	</head>
	<head>
		<div>
			<div id="div1" class="div bdiv"></div>
			<div id="div2" class="div ydiv"></div>
			<div id="div3" class="div gdiv"></div>
			<div id="div4" class="div bdiv"></div>
		</div>
		<script type="text/javascript" src="sea.js"></script>
		<script type="text/javascript">
			seajs.use('./mywriter.js', function (mywriter) {
				mywriter.write('div1', '我是黑颜色的');
				mywriter.write('div2', '我是黄颜色的');
				mywriter.write('div3', '我是绿颜色的');
				mywriter.write('div4', '我又是黑颜色的');
			});
		</script>
	</head>
	</html>
运行效果：

![image](https://raw.github.com/klvoek/osea/master/images/seajs-primary-usage-2.jpg)

####第五步：总结
我们已经成功的上手了seajs，简单的掌握了如何在页面上使用seajs以及开发自己的CommonJS模块代码。由于这部分内容的简单，这属于程序员的基本功，我也就不在这里对我们此次的成绩歌功颂德赞扬个不停了。当然之前已经说过这只是一个假象，是因为仅仅掌握了如何使用seajs加载CommonJS模块并不是完全上手seajs，甚至连十分之一都不到。而且seajs还隐含了一个非常重要的内容。所以，有些时候会让你觉得为什么五分钟的上手过程和自己之后项目中的实际使用过程差距怎么那么大呢？这并不是个人技术实力的问题，而是由于种种原因seajs并没有完善和公布那更加重要的一部分内容——这也是大公司式前端开发中一个非常重要的内容——项目式开发。
