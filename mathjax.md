# MathJax

如果要在演示文稿中显示数学方程式，则可以通过包含此插件来轻松实现。该插件是 [MathJax](http://www.mathjax.org/)  库的一个非常轻量的封装。要使用它，您需要将其作为 reveal.js 依赖项包括在内，在[此处找到有关依赖项的更多信息](dependencies.md)。

该插件默认使用[LaTeX](http://en.wikipedia.org/wiki/LaTeX)，但可以通过 `math` 配置对象进行调整。请注意，MathJax是从远程服务器加载的。如果要脱机使用它，则需要下载该库的副本并调整 `mathjax` 配置值。

以下是如何配置插件的示例。如果您不想更改这些值，则根本不需要包括math 配置对象。

```
Reveal.initialize({
	// 其他配置 ...

	math: {
		mathjax: 'https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js',
		config: 'TeX-AMS_HTML-full'  // 参见 http://docs.mathjax.org/en/latest/config-files.html
		// 将其他选项传递给 `MathJax.Hub.Config()`
		TeX: { Macros: macros }
	},

	dependencies: [
		{ src: 'plugin/math/math.js', async: true }
	]
});
```

如果需要[使用HTTPS](http://docs.mathjax.org/en/latest/start.html#secure-access-to-the-cdn)或提供稳定的[特定版本](http://docs.mathjax.org/en/latest/configuration.html#loading-mathjax-from-the-cdn)，请阅读MathJax的文档。

#### Markdown的MathJax

如果要在以Markdown编写的演示文稿中包含数学，则需要将公式包装在反引号中。这样可以防止LaTeX和Markdown之间的语法冲突。例如：

```
`$$ J(\theta_0,\theta_1) = \sum_{i=0} $$`
```

