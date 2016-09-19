# Learning Log for JavaScript

2014-05-10 21:55:37 Sat

0. demo-html

		<!DOCTYPE html>

		<html lang="en">
		<head>
			<meta charset="uft-8"/>
			<title>JavaScript</title>
			<style>
				.css-class{background-color: yellow;font-size: 20px;}
				.css-class2{height: 50px;color: #980000;}
			</style>
		</head>
		<body>
			<div id="main">
				<p> This is main div.</p>
			</div>
			<p>Try.</p>
			<script src="helloworld.js"></script>
		</body>
		</html>

1. 字符串中双引号可包括单引号,单引号可以包含双引号

		alert("It's single...")
		alert('It"s double...')

2. 变量声明 

		var myvariable; // undefined
		myvariable = "Hello World!";
		/* or
		var myvariable = "Hello World!";
		var PI = 3.14;
		var boolVar = false;
		*/
		alert(myvariable);

3. 变量书写开始以下划线、字母或者 $, 为了让变量更加可读, 可用单词组合变量, 并且词首建议用大写. 比如: `oneTwoThreeFour`.
4. 在 HTML 中引用 JavaScript 的方法.

		<!-- 方法1 -->
		<script>
		  alert("Hello, Wolrd!");
		</script>

		<!-- 方法2: 引入外部文件 -->
		<script src="helloworld.js"></script>

5. 计算示例

		var sum = 4 +5,
			deiff = 4 - 5,
			product = 4 * 5,
			quotient = 4 / 5;
		var foo = "Hello" + ", " + "World!";
		var foo = 4 + 5 + "7" + 6 + 5; // "9765"

6. 函数调用

		// example1
		var foo = doSomthing(1);
		function doSomthing(paramOne){
			paramOne = paramOne + 1;
			paramOne = paramOne * 8;

			return paramOne;
		}
		alert(foo);

		// example2
		var doSomthing = function(paramOne){
			paramOne = paramOne + 1;
			paramOne = paramOne * 8;

			return paramOne;
		}
		var foo = doSomthing(2);
		alert(foo);

7. Object 及方法调用

		var obj = "this is a string object.",
			length = obj.length; 		// length of obj
		var index = obj.indexOf("is");  // match 'is'
		var substr = obj.substring(0,4);
		alert(substr);

8. 创建 Object

		var person = {
			firstName: "Here",
			lastName: "Lei",
			getFullName : function(){
				return this.firstName + " " + this.lastName;
			}
		};
		alert(person.getFullName());

9. Array

		var foo = [10, true, "Hello"]; // index: 0 1 2
		foo[3] = "string";
		foo[foo.length] = "New Value"; // new a value
		alert(foo[0]);
		var foo2 = ["string two"];
		var fooTwo = foo.concat(foo2);	// merge foo and foo2 
		alert(fooTwo);

10. Conditions

		var con1 = "6" == 6;
		var con2 = "6" === 6;
		if (con1) { alert(con1); }
		if (con2) { alert(con2); } 
		else { alert("else here");}

11. loop-for

		var string = ["string1", "string2"]
		for (var i = 0; i < 2; i = i + 1){
			alert(string[i]);
		}

12. loop-while

		var string = ["string1", "string2"];
		while (string.length > 0){
			var element = string.pop();
			alert(element);
		}

13. window object

		var foo = "hello windows";
		var bar = function(){
			var foo = "hello function";
			alert(window.foo);
			alert(foo);
		}
		bar();

14. location

		var href = location;
		alert(href);

15. confirm
		if (confirm("Go to duckduckgo.com?")){
			location = "http://www.duckduckgo.com";
		} else {
			alert("You clicked cancel.");
		}

17. 将 JavaScript 放于文末的一个原因在于,如果一个操作依赖于已经导入的网页,那么只有当数据到进来之后才可以操作.这样就可以先加载需要操作的数据,然后加载要进行的操作代码段.

18. getElementsByTagName, getElementById

		(function(){
			// NodeList of p
			var pElements = document.getElementsByTagName("p");	
			alert(pElements.length);

			var pElement = document.getElementById("main");
			alert(pElement);
		}()	);

19.  querySelectorAll, querySelector

		(function(){
			var pElement = document.querySelectorAll("p");
			alert(pElement.length);

			var pElement = document.querySelector("#main");
			alert(pElement.parentNode.tagName);
		}()	);

20. createElement, appendChild, innerHTML

		(function(){
			var el = document.createElement("p");
			content = document.createTextNode("this is a new p tag.");
			el.appendChild(content);
			el.id = "new";				// create attribute
			document.body.appendChild(el);
			// parentNode replaceChild(node2,node1) innerHTML
			el.innerHTML = el.innerHTML + "<br/>innerHTML";
		}());

21. style

		// example 1
		(function(){
			var divFoo = document.getElementById("main"),
				style = divFoo.style;
			style.backgroundColor = "yellow";
			style.height = "50px";
		}())

		// example 2
		(function(){
			var divFoo = document.getElementById("main");
			divFoo.className = " css-class css-class2 ";
			divFoo.className = divFoo.className.replace(" css-class2 ", "");
			// getComputedStyle currentStyle
		}())

22. setTimeout - timer

		(function(){
			var doSomthing = function(){
			console.log("doSomthing() executed");
			};
			setTimeout(doSomthing, 2000);
			// clearTimeout()
			alert("hello");
		}());