# Ready事件

当 reveal.js 已加载了所有非异步的依赖, 并准备开始导航时被 ```ready``` 事件被触发。 要检查 reveal.js 是否已经 ready , 你可以调用 ```Reveal.isReady()``` 方法。

```
Reveal.addEventListener( 'ready', function( event ) {
	// event.currentSlide, event.indexh, event.indexv
} );
```

请注意，我们还在 ```.reveal``` 元素上添加了 ```.ready``` 类，以便您可以使用 CSS。

