### sass基本用法：

> #### 一、 变量机制

所有变量使用 <font color='red'>`$`</font>  ，若嵌在字符串中必须使用 <font color='red'>`#{}`</font> 中

```SAS
$main-color: #333;
$side: left;

.div1{
	background: $main-color;
	border-#{side}-radius: 5px;
}
```

======>>>>可把频繁使用的变量属性放置在单一文件夹下



> #### 二、嵌套写法

css写法如下：

```css
.container .content .left-side .name{
    font-size: 20px;
}
.container .content .left-side .age{
    font-size: 14px
}
```

sass写法：

```SAS
.container{
	.content{
		.left-side{
			.name{
				font-size: 20px;
			}
			.age{
				font-size: 14px
			}
		}
	}
}
```



> #### 三、模块机制

<font color='red'>`@import` </font> 规则-------->>>CSS和HTML完全分离，通过文件引入即可，

```SAS
@import "common";
```



> #### 四、Mixin: 一种混合指令，可将公共样式抽离放在单独的文件中，便于多处复用

css写法：

```css
.div1{
    background: red;
    border: 1px solid #333;
    border-radius: 2px;
}
.div2{
    background: blue;
    border: 1px solid #333;
    border-radius: 2px;
}
```

抽离公共样式的话就是：

```css
.div1,
.div2{
	border: 1px solid #333;
	border-radius: 2px
}
.div1{...}
.div2{...}
```

Sass的<font color='red'>`@mixin` </font> 如下：

```SAS
@mixin grey-border-radius {
	border: 1px solid #333;
	border-radius: 2px;
}
.div1{
	@include grey-border-radius;
	backgroud: red;
}
```

另外还可指定参数：

```SAS
@mixin ml($value: 10px){
	float: left;
	margin-left: $value;
}
.div1{
	@include ml(20px);
}
```



> #### 五、继承机制： 允许一个选择器继承另一个选择器

假如有一个消息框，除基础样式外，还有成功和失败的样式，css写法如下：

```css
.msg{
    border: 1px solid #e3e3e3;
    background: #dff08d;
}
.msg-success{
    color: #4cae4c;
}
.msg-error{
    color: #d43f3a;
}
```

定义上述样式后，需要在每个标签都添加一个 `.msg` 的类名，但使用sass继承机制后：

```SAS
.msg{
	border: 1px solid #e3e3e3;
	backgroung: #dff08d
}
.msg-success{
	@extend .msg;
	color: #4cae4c;
}
.msg-error{
	@extend .msg;
	color:  #d43f3a;
}
```

注： @mixin也可实现相同的效果，不同的是  <font size='4'>*继承拷贝的是选择器，而混合拷贝的是样式片段。*</font>



> #### 六：自定义函数

主要用于一些计算或者控制语句使用

如移动应用开发时，可以封装一个函数将px转换为rem：

```SAS
$baseFontSize: 20;
@function px2rem($val){
	@return $val/$baseFontSize + rem;
}
.big-text{
	font-size: px2rem(30);
}
```

