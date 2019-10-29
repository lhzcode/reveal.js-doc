# 插件

插件应通过调用 `Reveal.registerPlugin('myPluginID', MyPlugin)`在reveal.js 中注册。注册的插件实例可以选择暴露一个“ init”函数，recovery.js 将调用该函数来对其进行初始化。

当 reveal.js 通过 `Reveal.initialize()` 启动时，它将遍历所有已注册的插件并调用其"init"方法。如果"init"方法返回Promise，则 reveal.js 将在启动序列完成之前等待该promise完成，然后再触发ready事件。这是一个插件的示例，该插件在reveal.js 可以继续之前进行一些异步工作： 

```
let MyPlugin = {
	init: () =>  new Promise( resolve => setTimeout( resolve, 3000 ) )
};
Reveal.registerPlugin( 'myPlugin', MyPlugin );
Reveal.addEventListener( 'ready', () => console.log( 'Three seconds later...' ) );
Reveal.initialize();
```

如果 init 方法*未返回* Promise，则该插件将立即视为已准备就绪，并且不会阻止 Reveal.js 的启动顺序。

#### 检索插件

如果要检查是否已注册特定插件，则可以使用 `Reveal.hasPlugin`方法并传递插件ID，例如：`Reveal.hasPlugin('myPlugin')`。如果要检索插件实例，则可以使用`Reveal.getPlugin('myPlugin')`

