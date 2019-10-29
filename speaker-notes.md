# 演讲注释

reveal.js 附带一个演讲注释插件，可用于在单独的浏览器窗口中显示每张幻灯片的注释。备注窗口还为您提供了下一张幻灯片的预览，因此即使您没有写任何备注也可能会有所帮助。按键盘上的»S«键打开注释窗口。 

一旦打开演讲视图，演讲计时器就会启动。您可以随时通过单击/点击将其重置为00:00:00 

注释是通过将 `<aside>` 元素添加到幻灯片中来定义的，如下所示。如果您更喜欢使用 Markdown 编写笔记，则可以将 `data-markdown` 属性添加到 aside 元素 

或者，您可以在幻灯片的 `data-notes` 属性中添加注释。就像 `<section data-notes =“重要的事情"> </ section>` 。 

当在本地使用时，此功能要求从[本地Web服务器运行](full-setup.md)Reveal.js。

```
<section>
	<h2>Some Slide</h2>

	<aside class="notes">
		Oh hey, these are some notes. They'll be hidden in your presentation, but you can see them if you open the speaker notes window (hit »S« on your keyboard).
	</aside>
</section>
```

如果您使用外部Markdown插件，则可以在特殊的分隔符的帮助下添加注释： 

```
<section data-markdown="example.md" data-separator="^\n\n\n" data-separator-vertical="^\n\n" data-separator-notes="^Note:"></section>

# Title
## Sub-title

Here is some content...

Note:
This will only display in the notes window.
```

#### 共享并打印演讲注释<div id="share-and-print-speaker-notes"></div>

注释仅在演讲视图内对演讲者可见。如果您希望与他人共享笔记，则可以将 `showNotes` 配置值设置为 `true` 来初始化 reveal.js。注释将出现在演示文稿的底部。

启用 `showNotes` 时，[导出到PDF](pdf-export.md) 时也会包含注释。默认情况下，注释打印在幻灯片顶部的框中。如果您希望将它们打印在单独的页面上，请在幻灯片后将设置 `showNotes:“ separate-page”`。 

####  演讲注释时钟和计时器

演讲注释窗口还将显示：

- 自演示开始以来经过的时间。如果将鼠标悬停在此部分上方，将显示计时器重置按钮。 
- 当前的时间
- （可选）定速计时器，用于指示演示文稿的当前进度是否在正确的时间（绿色显示），如果不是，则演示者是否应该加快速度（以红色显示）还是可以放慢速度（蓝色）。 

可以通过在 `Reveal` 配置块中通过 `defaultTiming` 参数进行配置来启用定步计时器，该参数指定每张幻灯片的秒数。经验上来说120是比较合理的。也可以通过设置 `data-timing` 属性为每个幻灯片 `<section>` 给出时间。两个值均以秒为单位

#### 服务端演讲注释<div id="server-side-speaker-notes"></div>

在某些情况下，可能需要在与您要呈现的设备不同的设备上运行注释。基于Node.js的注释插件使您可以相同的注释。该注释保持与其客户端对应的注释定义相同。通过添加以下依赖项来包括所需的脚本： 

```
Reveal.initialize({
	// ...

	dependencies: [
		{ src: 'socket.io/socket.io.js', async: true },
		{ src: 'plugin/notes-server/client.js', async: true }
	]
});
```

然后：

1、安装 [Node.js](http://nodejs.org/)  （4.0.0或更高）

2、运行 `npm install`

3、运行 `node plugin/notes-server `

