# .NET 学习笔记


### 利用基类方法传递参数

	public void function(Type var1, Type var2, Typ2 var3)
		: base(var1, var2)
	{
		// sentence here
	}

### virtual

virtual 关键字用于指定属性或方法时可以在派生类中重写。

### abstract

抽象类用做基类，不能被实例化，用途是派生出其他非抽象类。

### Page Trace属性

设置`Trace="true"`可以查看

### Default Button，Default Focus

Default Button：回车默认点击的按钮
Default Focus：默认聚焦的文本框

	<form deaultbutton="这里填写按钮的ID" defaultfocus="这里填写文本框ID"></form>

或者直接在cs文件中填写

	...TexBox.Fous();

### Header,Footer Control

后缀为ascx。只作为页面的一部分，因此不能直接通过浏览器预览。可以直接将ascx文件拖到aspx文件中，作为引用。