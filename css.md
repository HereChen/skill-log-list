# CSS3

<https://github.com/HereChen/Front-End-Book>

## Part 1

* 注意浏览器对特性的兼容性问题
* boder-radius: 圆角

    ```css
    {
      boder-radius:50px;
      -webkit-boder-radius:50px;
      -moz-boder-radius:50px;
    }
    ```

* box-shadow: 阴影

    ```css
    {
      box-shadow: 5px 5px 10px black;
      box-shadow: 5px 5px 10px rgba(10,10,10,5);
      /* overlay */
      box-shadow: 5px 5px 10px black, 5px 5px 10px red;
    }
    ```

* text-shadow: 字体阴影;

    ```css
    {
      text-shadow: 0 1px 0 white;
    }
    ```

* linear-gradient: 渐进颜色

    ```css
    {
      background: linear-gradient(top, black, yellow);
      background: linear-gradient(top, black 50%, yellow 50%);
    }
    ```

* column: 规定列宽和列数 (可自动将文段分成若干列)  `columns: column-width column-count;`

    ```css
    {
      column-width: 100px;
      column-count: 4;
      column-gap: 20px;
    }
    ```

* Media-Queries: 根据不同的屏幕宽度作不同的修饰

    ```css
    {
      /* different screen size with different font size */
      @media screen and (max-width: 800px){
        font-size: 30;
      }
      @media screen and (max-width: 500px){
        font-size: 20;
      }
    }
    ```

* transiton: 属性的渐变

    ```css
    li { transition: padding-left .5s, color 2s; }
    li:hover { padding-left: 20px;color: #980000; }
    ```

* fontface: 设置字体

    ```css
    @font-face {
      font-family: sans-serif;
      src: url('fonts/webfont.ttf') format('truetype');
      font-weight: normal;
      font-style: normal;
    }
    ```

* selector: 选择性设置

    ```css
    /* demo with nine li */
    li:first-child{background: green;}
    li:last-child{background: yellow;}
    li:nth-child(3){background: red;}
    li:nth-child(3n){background: red;}
    li:nth-child(3n+1){background: red;}
    ```

* adjacent selector: 对邻近元素的设置

    ```css
    /* set p that is adjacent to h2 */
    h2 + p{font-size: 2.5em;}
    ```

* Sibling Combinator: 对在同一层的某元素作设置

    ```css
    h2 ~ p{font-size: 2.5em;}
    ```

* Target Elements Based On Attribute Values: 根据元素值设置

    ```css
    a[href="http://herechen.github.io"]{color: yellow;}
    /* if contains the words */
    a[href*="herechen"]{color: yellow;}
    /* endding */
    a[href$=".pdf"]:before{content: 'PDF';}
    /* begining */
    a[href^="http"]{color: yellow;}
    ```

* first line and letter: 设置第一行和第一个单词

    ```css
    p::first-line{font-weight: bold;}
    p::first-letter{font-size: bold;font-weight: bold;}
    ```

* transformation: 变换

    ```css
    img:hover{-webkit-transform: rotate(90deg) scale(1.2);}
    ```

## Part2

* 简写(`font`, `padding`)

    ```css
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
    ```

* 选择文本后的背景颜色

    ```css
    ::selection{
      background-color: red;
      color: white;
    }
    ::-moz-selection{
      background-color: red;
      color: white;
    }
    ```

* 字体设置

    ```css
    /* the browser will read from the left to the right */
    /* move to check the next font if the font does not exist */
    body{
      font-family: Helvetica, Arial, "Lucida Grande", sans-serif;
    }
    ```

* 段落首字符设置

    ```css
    p:first-child:first-letter {
      float: left;
      color: green;
      font: 72px/100% Georgia,serif;
      margin: 0 14px 0 0;
    }
    ```

* placeholder 字体颜色

    ```css
    ::-webkit-input-placeholder {
      color: yellow;
    }
    ```

* 去除外边线(`a`, `input`)

    ```css
    /* links */
    a:focus{outline: none;}
    /* input box */
    input[type="text"]{outline: none;}
    ```

* 水平和垂直居中

    ```css
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
    ```

* Properly Clear and Contain Floats

    ```css
    .floated-p{float: left;}
    .clear{clear: both;}
    ```

* CSS Triangles

    ```css
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
    ```

* 绘制圆形

    ```css
    .circle{
      background-color: green;
      width: 10em;
      height: 10em;
      border-radius: 5em;
    }
    ```

* 纸张效果图

    ```css
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
    ```

* 列表效果

    ```css
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
    ```

* 返回顶部按钮

    ```css
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
    ```

* 奇偶元素选择

    ```css
    /* tr:nth-child(even){...} */
    tr:nth-child(odd){background-color: #fafafa;}
    li:nth-child(2n){color: #fafafa;}
    ```
