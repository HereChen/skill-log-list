# CSS3

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