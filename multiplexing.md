# 复用

复用插件使您的听众可以在自己的手机，平板电脑或笔记本电脑上查看您正在控制的演示文稿的幻灯片。示例： https://reveal-js-multiplex-ccjbegmaii.now.sh/

复用插件需要执行以下三件事： 

1、拥有控制权的主演讲文稿 

2、客户端演示文稿跟随主演示文稿

3、Socket.io 服务器从主到客户端广播事件 

#### 主演示文稿<div id="master-presentation"></div>

只有演示者（推荐）可访问的静态文件服务器的服务。这仅需要在您（演示者）的计算机上（从您自己的计算机运行主演示文稿比较安全，因此，如果场地的Internet出现故障，它也不会停止播放。）一个示例是在主演示文稿的目录中执行以下命令： 

1. `npm install node-static`
2. `static`

如果要在主演示文稿中使用演讲注释插件，请确保已正确配置了演讲注释插件以及以下所示的配置，然后在主演示文稿的目录中执行 `node plugin / notes-server`。下面的配置将使它作为主机连接到socket.io服务器，并启动您的演讲注释/静态文件服务器。

```
Reveal.initialize({
	// 其他配置...

	multiplex: {
		// 示例值。要生成自己的内容，请参阅socket.io服务器说明
		secret: '13652805320794272084', // 从socket.io服务器获得。
赋予演示文稿的（主）控制权
		id: '1ea875674b17ca76', // 从socket.io服务器获得
		url: 'https://reveal-js-multiplex-ccjbegmaii.now.sh' // socket.io服务器的地址
	},

	// 不要忘记添加依赖项
	dependencies: [
		{ src: '//cdnjs.cloudflare.com/ajax/libs/socket.io/2.2.0/socket.io.js', async: true },
		{ src: 'plugin/multiplex/master.js', async: true },

		// 以及如果您想要演讲者笔记
		{ src: 'plugin/notes-server/client.js', async: true }

		// 其他依赖项...
	]
});
```

#### 客户端演示文稿<div id="client-presentation"></div>

从可公开访问的静态文件服务器提供服务。示例包括：GitHub Pages，Amazon S3，Dreamhost，Akamai等。越可靠，越好。然后，您的听众可以通过 http://example.com/path/to/presentation/client/index.html 访问客户端演示，并使用以下配置使他们作为客户端连接到socket.io服务器。

配置示例：

```
Reveal.initialize({
	// 其他配置项...

	multiplex: {
		// 示例值。要生成自己的内容，请参阅socket.io服务器说明
		secret: null, // null，因此客户端无法控制主演示文稿
		id: '1ea875674b17ca76', // id，从socket.io服务器获取
		url: 'https://reveal-js-multiplex-ccjbegmaii.now.sh' // socket.io服务器的位置
	},

	// 不要忘记添加依赖项
	dependencies: [
		{ src: '//cdnjs.cloudflare.com/ajax/libs/socket.io/2.2.0/socket.io.js', async: true },
		{ src: 'plugin/multiplex/client.js', async: true }

		// 其他依赖...
	]
});
```

#### Socket.io 服务器<div id="socketio-server"></div>

从主演示文稿接收 `slideChanged` 事件并将其广播到连接的客户端演示文稿的服务器。这需要公开访问。您可以使用以下命令运行自己的socket.io服务器：

1. `npm install`

2. `node plugin/multiplex`

或者，您可以在 https://reveal-js-multiplex-ccjbegmaii.now.sh/ 使用socket.io服务器。

您需要为主演示和客户端演示生成唯一的密钥和令牌对。为此，请访问 `http://example.com/token`，其中 `http://example.com` 是socket.io服务器的位置。或者，如果您要在 https://reveal-js-multiplex-ccjbegmaii.now.sh/ 上使用socket.io服务器，请访问 https://reveal-js-multiplex-ccjbegmaii.now.sh/token 。

非常欢迎您将演示文稿指向运行在 https://reveal-js-multiplex-ccjbegmaii.now.sh/ 的Socket.io服务器，但不能保证可用性和稳定性。

对于关键任务，我建议您运行自己的服务器。最简单的方法是立即安装。安装该程序后，部署您自己的复用服务器就很容易从 reveal.js 文件夹中运行以下命令：`now plugin/multiplex`。

#####  socket.io服务器作为文件静态服务器

socket.io服务器可以充当客户端演示文稿的静态文件服务器，如 https://reveal-js-multiplex-ccjbegmaii.now.sh/ 上的示例。（在两个浏览器中打开 https://reveal-js-multiplex-ccjbegmaii.now.sh/ 。在其中一个幻灯片上浏览，另一个将更新以匹配。）

配置示例：

```
Reveal.initialize({
	// 其他配置...

	multiplex: {
		// 示例值。要生成自己的内容，请参阅socket.io服务器说明。
		secret: null, // null，因此客户端无法控制主演示文稿
		id: '1ea875674b17ca76', // id，从socket.io服务器获取
		url: 'example.com:80' // 您的socket.io服务器的位置
	},

	// 不要忘记添加依赖项
	dependencies: [
		{ src: '//cdnjs.cloudflare.com/ajax/libs/socket.io/2.2.0/socket.io.js', async: true },
		{ src: 'plugin/multiplex/client.js', async: true }

		// 其他依赖...
	]
```

它还可以同时为您的主演示文稿和客户端演示文稿充当静态文件服务器的角色（只要您不想使用演讲者备注）。（在两个浏览器中打开 https://reveal-js-multiplex-ccjbegmaii.now.sh/ 。在其中一个幻灯片上浏览，另一个将更新以匹配。在第二个幻灯片上浏览，第一个将更新匹配）。这可能是不希望的，因为您不希望观众在演示时弄乱幻灯片。;）

配置示例：

```
Reveal.initialize({
	// 其他配置...

	multiplex: {
		// 示例值。要生成自己的内容，请参阅socket.io服务器说明。
		secret: '13652805320794272084', // 从socket.io服务器获得。赋予演示文稿的（主）控制权
		id: '1ea875674b17ca76', // 从socket.io服务器获得。
		url: 'example.com:80' //  您的socket.io服务器的位置
	},

	// 不要忘记添加依赖项
	dependencies: [
		{ src: '//cdnjs.cloudflare.com/ajax/libs/socket.io/2.2.0/socket.io.js', async: true },
		{ src: 'plugin/multiplex/master.js', async: true },
		{ src: 'plugin/multiplex/client.js', async: true }

		// 其他依赖...
	]
});
```

