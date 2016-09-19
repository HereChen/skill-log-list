### CSS Tips and Tricks

1. Use CSS Shorthand

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

2. Change Text Selection Color

		::selection{
			background-color: red;
			color: white;
		}
		::-moz-selection{
			background-color: red;
			color: white;
		}

3. Awesome Font Stacks

		/* the browser will read from the left to the right */
		/* move to check the next font if the font does not exist */
		body{
			font-family: Helvetica, Arial, "Lucida Grande", sans-serif;
		}

4. First Letter ( Drop Caps )

		p:first-child:first-letter{
			float: left;
			color: green;
			font: 72px/100% Georgia,serif;
			margin: 0 14px 0 0;
		}

5. Style Placeholder Text

		::-webkit-input-placeholder{
			color: yellow;
		};

6. Remove Dotted Outline on Links

		/* links */
		a:focus{outline: none;}
		/* input box */
		input[type="text"]{outline: none;}

7. Horizontal and Vertical Centering

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

10. CSS Circles

		.circle{
			background-color: green;
			width: 10em;
			height: 10em;
			border-radius: 5em;
		}

11. Create a Layered Paper Effect

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

12.  Get Creative With the List Bullets

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

13. Create a Fixed Back to Top Button

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

14.  Even and Odd Rows

		/* tr:nth-child(even){...} */
		tr:nth-child(odd){background-color: #fafafa;}
		li:nth-child(2n){color: #fafafa;}