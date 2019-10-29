# 懒加载

在使用大量媒体或 iframe 内容进行演示时，延迟加载很重要。延迟加载意味着 Reveal.js 将仅加载最接近当前幻灯片的几张幻灯片的内容。预加载的幻灯片数量由 ```viewDistance``` 配置选项确定。

要启用延迟加载，您需要做的就是将 src 属性更改为 data-src，如下所示。图片，视频，音频和 iframe 元素均支持此功能。  

```
<section>
  <img data-src="image.png">
  <iframe data-src="http://hakim.se"></iframe>
  <video>
    <source data-src="video.webm" type="video/webm" />
    <source data-src="video.mp4" type="video/mp4" />
  </video>
</section>
```

####  iframe 延迟加载

请注意，延迟加载的 iframe 会忽略 ```viewDistance``` 配置，并且仅在包含其的幻灯片可见时才加载。隐藏幻灯片后，iframe 也将被卸载。 

当我们延迟加载视频或音频元素时，除非幻灯片变得可见，reveal.js才会开始播放该内容。但是，由于 iframe 可能包含任何内容，因此无法对其进行控制。这意味着，如果我们在幻灯片在屏幕上可见之前加载了iframe，它就可以开始在后台播放媒体和声音。 

 您可以使用 ```data-preload``` 属性覆盖此行为。下面的 iframe 将根据 ```viewDistance``` 加载。 

```
<section>
	<iframe data-src="http://hakim.se" data-preload></iframe>
</section>
```

 您还可以使用 ```preloadIframes``` 配置选项全局更改默认值。如果设置为 ```true``` ，则在```viewDistance``` 内时，无论 ``` data-preload ``` 属性如何，所有具有 ```data-src``` 属性的 iframe 都会预加载。如果设置为 ```false``` ，则所有 iframe 仅在它们可见时才会加载。 

