# CSS3

## Part 1

0. 注意浏览器对特性的兼容性问题
1. boder-radius: 圆角

		boder-radius:50px;
		-webkit-boder-radius:50px;
		-moz-boder-radius:50px;

2. box-shadow: 阴影

		box-shadow: 5px 5px 10px black;
		box-shadow: 5px 5px 10px rgba(10,10,10,5);
		/* overlay */
		box-shadow: 
			5px 5px 10px black,
			5px 5px 10px red;

3. text-shadow: 字体阴影;

		text-shadow: 0 1px 0 white;

4. linear-gradient: 渐进颜色

		background: linear-gradient(top, black, yellow);
		background: linear-gradient(top, black 50%, yellow 50%);

5. column: 规定列宽和列数 (可自动将文段分成若干列)  `columns: column-width column-count;`

		column-width: 100px;
		column-count: 4;
		column-gap: 20px;

6. Media-Queries: 根据不同的屏幕宽度作不同的修饰

		/* different screen size with different font size */
		@media screen and (max-width: 800px){
			font-size: 30;
		}
		@media screen and (max-width: 500px){
			font-size: 20;
		}

7. transiton: 属性的渐变

		li{transition: padding-left .5s, color 2s;}
		li:hover{padding-left: 20px;color: #980000;}

8. fontface: 设置字体

		@font-face{
			font-family: sans-serif;
			src: url('fonts/webfont.ttf') format('truetype');
			font-weight: normal;
			font-style: normal;
		}

9. selector: 选择性设置

		/* demo with nine li */
		li:first-child{background: green;}
		li:last-child{background: yellow;}
		li:nth-child(3){background: red;}
		li:nth-child(3n){background: red;}
		li:nth-child(3n+1){background: red;}

10. adjacent selector: 对邻近元素的设置

		/* set p that is adjacent to h2 */
		h2 + p{font-size: 2.5em;}

11. Sibling Combinator: 对在同一层的某元素作设置

		h2 ~ p{font-size: 2.5em;}

12. Target Elements Based On Attribute Values: 根据元素值设置

		a[href="http://herechen.github.io"]{color: yellow;}
		/* if contains the words */
		a[href*="herechen"]{color: yellow;}
		/* endding */
		a[href$=".pdf"]:before{content: 'PDF';}
		/* begining */
		a[href^="http"]{color: yellow;}

13. first line and letter: 设置第一行和第一个单词

		p::first-line{font-weight: bold;}
		p::first-letter{font-size: bold;font-weight: bold;}

14. transformation: 变换

		img:hover{-webkit-transform: rotate(90deg) scale(1.2);}	

## Part2

1. 简写(`font`, `padding`)

		/* normal */
		.demo-p{
			font-style: italic;
			font-weight: bold;
			font-size: 13px;
			line-height: 1.5;
			font-family: Arial, sans-serif;
			background-color: #ccc;
			padding-top: 1em;
			padding-bottom: 1em;
			padding-left: 1em;
			padding-right: 1em;
		}
		/* shorhand */
		.demo-p{
			font: italic bold 13px/1.5 Arial, sans-serif;
			background-color: #ccc;
			padding: 1em;
		}

2. 选择文本后的背景颜色

		::selection{
			background-color: red;
			color: white;
		}
		::-moz-selection{
			background-color: red;
			color: white;
		}

3. 字体设置

		/* the browser will read from the left to the right */
		/* move to check the next font if the font does not exist */
		body{
			font-family: Helvetica, Arial, "Lucida Grande", sans-serif;
		}

4. 段落首字符设置

		p:first-child:first-letter{
			float: left;
			color: green;
			font: 72px/100% Georgia,serif;
			margin: 0 14px 0 0;
		}

5. placeholder 字体颜色

		::-webkit-input-placeholder{
			color: yellow;
		};

6. 去除外边线(`a`, `input`)

		/* links */
		a:focus{outline: none;}
		/* input box */
		input[type="text"]{outline: none;}

7. 水平和垂直居中

		p{text-align: center;}
		p{width: 50%;margin: 0 auto;}
		img{display: block;margin: 0 auto;}
		.container{height: 15em;display: table-cell;vertical-align: middle;}
		.container{
			width: 100%;
			min-height: 30em;
			background: #ccc url(assets/image.jpg) center center no-repeat;
		}
		.container img{
			position: absolute;
			top: 50%;
			left: 50%;
			margin-top: -100px;
			margin-left: -100px;
		}

8. Properly Clear and Contain Floats

		.floated-p{float: left;}
		.clear{clear: both;}

9. CSS Triangles

		.up{
			border-left: 10px solid transparent;
			border-right: 10px solid transparent;
			border-bottom: 10px solid red;
		}
		.down{
			border-left: 10px solid transparent;
			border-right: 10px solid transparent;
			border-top: 10px solid red;
		}
		.left{
			border-top: 10px solid transparent;
			border-bottom: 10px solid transparent;
			border-right: 10px solid red;
		}
		.right{
			border-top: 10px solid transparent;
			border-bottom: 10px solid transparent;
			border-left: 10px solid red;
		}

10. 绘制圆形

		.circle{
			background-color: green;
			width: 10em;
			height: 10em;
			border-radius: 5em;
		}

11. 纸张效果图

		.paper{
			background-color: #fafafa;
			border: 1px solid #f2f2f3;
			border-bottom: 0;
			padding: 1em;
			text-align: center;

			box-shadow: 
				0 1px 1px rgba(0, 0, 0, .15),
				0 10px 0 -5px #eee,
				0 10px 1px -4px rgba(0, 0, 0, .15),
				0 20px 0 -10px #eee,
				0 20px 1px -9px rgba(0, 0, 0, .15);
		}

12.  列表效果

		ul{list-style-type: none;}
		.list-1 li{
			background: url(bullet.png) left center no-repeat;
			padding-left: 1em;
		}
		/* triangle */
		.list-2 li:before{
			content: "";
			display: inline-block;
			height: 0;
			width: 0;
			border-color: transparent #111;
			border-style: solid;
			border-width: 4px 0 4px 6px;
			margin-right: .5em;
		}
		/* circle */
		.list-3 li:before{
			content: "";
			display: inline-block;
			background-color: black;
			height: 6px;
			width: 6px;
			border-radius: 3px;
			margin: 0 .5em 1px;
		}

13. 返回顶部按钮

		/* <div id="top"> */
		/* <a href="#top" class="back-to-top">back to top</a> */
		.back-to-top{
			background-color: rgba(0, 0, 0, .75);
			position: fixed;
			bottom: 2em;
			right: 2em;
			color: white;
			padding: .5em 1em;
			text-transform: uppercase;
			font-size: 11px;
			font-weight: bold;
		}

14.  奇偶元素选择

		/* tr:nth-child(even){...} */
		tr:nth-child(odd){background-color: #fafafa;}
		li:nth-child(2n){color: #fafafa;}