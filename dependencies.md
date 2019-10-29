# 依赖

Reveal.js不*依赖*任何第三方脚本来工作，但默认情况下包括一些可选库。这些库按照它们出现的顺序作为依赖项加载，例如： 

```
Reveal.initialize({
	dependencies: [
		// 解析 <section> 元素中的 Markdown
		{ src: 'plugin/markdown/marked.js', condition: function() { return !!document.querySelector( '[data-markdown]' ); } },
		{ src: 'plugin/markdown/markdown.js', condition: function() { return !!document.querySelector( '[data-markdown]' ); } },

		// <code>元素的语法突出显示
		{ src: 'plugin/highlight/highlight.js', async: true },

		// 使用Alt +单击放大和缩小
		{ src: 'plugin/zoom-js/zoom.js', async: true },

		// 演讲注释
		{ src: 'plugin/notes/notes.js', async: true },

		// MathJax
		{ src: 'plugin/math/math.js', async: true }
	]
});
```

你可以使用相同的语法添加自己的扩展。以下属性可用于每个依赖的对象当中：

- **src:** 脚本加载的路径。
- **async:** 是否异步, 可选标志。本是否在 reveal.js 之后开始加载, 默认值为 false。
- **callback:** 回调方法, 可选方法。当脚本加载是执行。
- **condition:** 返回条件 , 可选方法。为要加载的脚本返回 true。