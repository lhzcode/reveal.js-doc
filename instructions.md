# 使用说明

## 标记<div id="Markup"></div>

这是一个标准的示例：

```
<html>
	<head>
		<link rel="stylesheet" href="css/reveal.css">
		<link rel="stylesheet" href="css/theme/white.css">
	</head>
	<body>
		<div class="reveal">
			<div class="slides">
				<section>Slide 1</section>
				<section>Slide 2</section>
			</div>
		</div>
		<script src="js/reveal.js"></script>
		<script>
			Reveal.initialize();
		</script>
	</body>
</html>
```

演示文稿的标记层次必须是 `.reveal > .slides > section` ，其中 ```section``` 代表一张幻灯片，并且可以重复。如果将多个 ```section``` 元素放在另一个 ```section``` 之内，则他们将显示为垂直幻灯片。垂直幻灯片的第一个是其他幻灯片的“根”(在顶部)，并且将包含在水平序列中。例如：

```
<div class="reveal">
	<div class="slides">
		<section>Single Horizontal Slide</section>
		<section>
			<section>Vertical Slide 1</section>
			<section>Vertical Slide 2</section>
		</section>
	</div>
</div>
```

## Markdown  <div id="markdown"></div>

可以使用Markdown编写幻灯片。 要启用Markdown，请将 ```data-markdown``` 属性添加到您的 ```<section>``` 元素中，然后将内容包装在 ```<textarea data-template>``` 中，如下例所示。您还需要将 ```plugin / markdown / marked.js``` 和 ```plugin / markdown / markdown.js``` 脚本（按此顺序）添加到HTML文件中。 

这是基于  [Paul Irish](https://github.com/paulirish) 的 [data-markdown](https://gist.github.com/1343518) 进行的修改，以 [marked](https://github.com/chjj/marked) 支持 [GitHub Flavored Markdown](https://help.github.com/articles/github-flavored-markdown)。 对缩进（避免混合制表符和空格）和换行符（避免连续的换行）敏感。

```
<section data-markdown>
	<textarea data-template>
		## Page title

		A paragraph with some text and a [link](http://hakim.se).
	</textarea>
</section>
```

#### 外部的Markdown

您可以将内容写在一个单独的文件当中，并在运行时加载reveal.js文件。 注意分隔符参数，这些参数确定如何在外部文件中分隔幻灯片：```data-separator``` 属性为水平幻灯片定义了正则表达式（默认为 ``` ^\r?\n---\r?\n$ ``` ,以换行符为水平），```data-separator-vertical``` 属性定义了垂直的幻灯片（默认禁止），``` data-separator-notes``` 属性是一个正则表达式，用于指定当前幻灯片的演讲注释的开头（默认为```notes?:``` ，所以会匹配到“note:”或“notes:”）， ``` data-charset ``` 属性是可选的，它指定在加载外部文件时使用哪个字符集。 

```
<section data-markdown="example.md"
         data-separator="^\n\n\n"
         data-separator-vertical="^\n\n"
         data-separator-notes="^Note:"
         data-charset="iso-8859-15">
    <!--
        Note that Windows uses `\r\n` instead of `\n` as its linefeed character.
        For a regex that supports all operating systems, use `\r?\n` instead of `\n`.
    -->
</section>
```

#### 元素属性<div id="element-attributes"></div>

特殊语法（通过HTML注释）可用于向Markdown元素添加属性。除此之外，这对于片段很有用。 

```
<section data-markdown>
	<script type="text/template">
		- Item 1 <!-- .element: class="fragment" data-fragment-index="2" -->
		- Item 2 <!-- .element: class="fragment" data-fragment-index="1" -->
	</script>
</section>
```

#### 幻灯片属性<div id="slide-attributes"></div>

特殊语法（通过HTML注释）可用于将属性添加到Markdown生成幻灯片的 ```<section>``` 元素中。 

```
<section data-markdown>
	<script type="text/template">
	<!-- .slide: data-background="#ff0000" -->
		Markdown content
	</script>
</section>
```

#### 配置*标记*

我们使用 [marked](https://github.com/chjj/marked) 来解析 Markdown。要自定义标记的渲染，你可以在 [配置reveal](configuration.md) 时传递选项

```
Reveal.initialize({
	// 传递到标记的选项
	// 参见 https://marked.js.org/#/USING_ADVANCED.md#options
	markdown: {
		smartypants: true
	}
});
```

 

