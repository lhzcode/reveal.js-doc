# API

 ```Reveal``` 对象公开了用于控制导航和读取状态的JavaScript API： 

```
// 导航
Reveal.slide( indexh, indexv, indexf );
Reveal.left();
Reveal.right();
Reveal.up();
Reveal.down();
Reveal.prev();
Reveal.next();
Reveal.prevFragment();
Reveal.nextFragment();

// 随机幻灯片的顺序
Reveal.shuffle();

// 切换演示状态,通过 true/false 来控制 开/关
Reveal.toggleOverview();
Reveal.togglePause();
Reveal.toggleAutoSlide();

// 显示带有键盘快捷键的帮助图，可以选择 true/false
// 强制打开/关闭
Reveal.toggleHelp();

// 在运行时改变一个配置值
Reveal.configure({ controls: true });

// 返回当前的配置值
Reveal.getConfig();

// 获取当前演示文稿的缩放比例
Reveal.getScale();

// 检索之前和当前幻灯片元素
Reveal.getPreviousSlide();
Reveal.getCurrentSlide();

Reveal.getIndices();        // { h: 0, v: 0, f: 0 }
Reveal.getSlidePastCount();
Reveal.getProgress();       // (0 == 第一张, 1 == 最后一张)
Reveal.getSlides();         // 所有幻灯片的数组
Reveal.getTotalSlides();    // 幻灯片的总数

// 返回当前幻灯片的演讲注释
Reveal.getSlideNotes();

// 检查状态
Reveal.isFirstSlide();
Reveal.isLastSlide();
Reveal.isOverview();
Reveal.isPaused();
Reveal.isAutoSliding();

// 返回顶层的DOM元素
getRevealElement(); // <div class="reveal">...</div>
```

#### 自定义键盘绑定

可以使用以下 Javascript API 添加和删除自定义键绑定。自定义键绑定将覆盖默认的键盘绑定，但是依次会被 ```键盘``` 配置选项中的用户定义的绑定覆盖。 

```
Reveal.addKeyBinding( binding, callback );
Reveal.removeKeyBinding( keyCode );
```

例如：

```
// 绑定参数提供以下属性
//     keyCode：绑定到回调的键码
// 	       key：在帮助中显示的键标签
// description：在帮助中显示的操作说明
Reveal.addKeyBinding( { keyCode: 84, key: 'T', description: 'Start timer' }, function() {
	// 开始时
} )

// 绑定参数也可以是直接键码，而无需提供帮助说明
Reveal.addKeyBinding( 82, function() {
	// 重置时
} )
```

这允许插件将键绑定直接添加到 Reveal，以便他们可以 

-  利用Reveal的预处理逻辑进行按键处理（例如，暂停时忽略按键） 
-  包含在帮助中（可选） 

#### Slide Change 事件<div id="slide-changed-event"></div>

每次更改幻灯片（无论状态如何）都会触发一次 ```slidechanged``` 事件。 事件对象保存当前幻灯片的索引值以及对先前和当前幻灯片HTML节点的引用。

 一些库，例如 MathJax（请参阅  [#226](https://github.com/hakimel/reveal.js/issues/226#issuecomment-10261609) ），会因幻灯片的变换和显示状态而混淆。通常，可以通过从此回调中调用其 update 或 render 函数来解决此问题。 

```
Reveal.addEventListener( 'slidechanged', function( event ) {
	// event.previousSlide, event.currentSlide, event.indexh, event.indexv
} );
```

#### 演示状态<div id="presentation-state"></div>

演示文稿的当前状态可以通过使用的 `getState` 方法获取。 `state` 对象包含所有需要的信息，这些信息可以复原第一次调用 ```getState``` 时的状态。这有一点像快照。它可以很容易地字符串化和持久化或通过网络发送一个简单的对象。 

```
Reveal.slide( 1 );
// we're on slide 1

var state = Reveal.getState();

Reveal.slide( 3 );
// we're on slide 3

Reveal.setState( state );
// we're back on slide 1
```

#### 幻灯片状态<div id="slide-states"></div>

如果在幻灯片 ```<section>``` 上设置 ```data-state =“ somestate”``` ，则打开该幻灯片时，“ somestate” 将作为文档元素上的作为类的一个应用。这使您可以根据活动幻灯片对页面应用广泛的样式更改。 

此外，您还可以通过JavaScript监听状态变化 ：

```
Reveal.addEventListener( 'somestate', function() {
	// TODO: Sprinkle magic
}, false );
```

#### 幻灯片背景<div id="slide-backgrounds"></div>

默认情况下，幻灯片仅包含在屏幕的有限区域内，以便适合任何显示屏并统一缩放。您可以通过在 ```<section>``` 元素中添加 ```data-background``` 属性来在幻灯片区域之外应用整页背景。支持四种不同类型的背景：纯色，图像，视频和 iframe。 

##### 纯色背景

支持所有CSS颜色格式，包括十六进制值，关键字 ， `rgba()` 或 `hsl()`. 

```
<section data-background-color="#ff0000">
	<h2>Color</h2>
</section>
```

##### 图片背景

默认情况下，调整背景图像的大小以覆盖整个页面。可用选项 ：

| 属性                     | 默认值    | 描述                                                         |
| ------------------------ | --------- | ------------------------------------------------------------ |
| data-background-image    |           | 要显示的图像的URL。幻灯片打开时，GIF重新启动。               |
| data-background-size     | cover     | 参见MDN上的 [background-size](https://developer.mozilla.org/docs/Web/CSS/background-size) |
| data-background-position | center    | 参见MDN上的 [background-position](https://developer.mozilla.org/docs/Web/CSS/background-position) |
| data-background-repeat   | no-repeat | 参见MDN上的 [background-repeat](https://developer.mozilla.org/docs/Web/CSS/background-repeat) |
| data-background-opacity  | 1         | 背景图片的透明度为0-1比例。0是透明的，1是完全不透明的。      |

```
<section data-background-image="http://example.com/image.png">
	<h2>Image</h2>
</section>
<section data-background-image="http://example.com/image.png" data-background-size="100px" data-background-repeat="repeat">
	<h2>This background image will be sized to 100px and repeated</h2>
</section>
```

##### 视频背景

自动在幻灯片后面播放全尺寸视频。

| 属性                        | 默认值 | 描述                                                       |
| --------------------------- | ------ | ---------------------------------------------------------- |
| data-background-video       |        | 单个视频源，或以逗号分隔的视频源列表。                     |
| data-background-video-loop  | false  | 重复播放视频的标识                                         |
| data-background-video-muted | false  | 音频静音的标识                                             |
| data-background-size        | cover  | 使用`cover` 进行全屏和一些裁切，或者使用`contain` 作为宽屏 |
| data-background-opacity     | 1      | 背景视频的透明度为0-1比例。0是透明的，1是完全不透明的。    |

```
<section data-background-video="https://s3.amazonaws.com/static.slid.es/site/homepage/v1/homepage-video-editor.mp4,https://s3.amazonaws.com/static.slid.es/site/homepage/v1/homepage-video-editor.webm" data-background-video-loop data-background-video-muted>
	<h2>Video</h2>
</section>
```

##### 背景过渡

默认情况下，背景过渡使用淡入淡出动画。通过将 ```backgroundTransition：'slide'``` 传递给 ```Reveal.initialize（）```调用，可以将其更改为线性滑动过渡。或者，您可以在具有背景的任何部分上设置 ```data-background-transition``` 来覆盖该特定转换。 

#### 视差背景<div id="parallax-background"></div>

 如果要使用视差滚动背景，请在初始化 reveal.js 时在下面设置前两个属性（其他两个是可选的） 

```
Reveal.initialize({

	// 视差背景图片
	parallaxBackgroundImage: '', // 例如： "https://s3.amazonaws.com/hakim-static/reveal-js/reveal-parallax-1.jpg"

	// 视差背景大小
	parallaxBackgroundSize: '', // CSS 语法, 例如： "2100px 900px" - 目前只支持px (不要使用 % 或 auto)

	// 每张幻灯片移动视差背景的像素数
	// - 除非指定，否则自动计算
	// - 设置为0以禁用沿轴的移动
	parallaxBackgroundHorizontal: 200,
	parallaxBackgroundVertical: 50

});
```

确保背景尺寸比屏幕尺寸大得多，以便进行一些滚动。[查看示例](http://revealjs.com/?parallaxBackgroundImage=https%3A%2F%2Fs3.amazonaws.com%2Fhakim-static%2Freveal-js%2Freveal-parallax-1.jpg&parallaxBackgroundSize=2100px%20900px)。 

#### 幻灯片切换<div id="slide-transitions"></div>

使用 ``` transition ``` 配置设置全局演示过渡。您可以使用 ```data-transition``` 属性覆盖特定幻灯片的全局过渡： 

```
<section data-transition="zoom">
	<h2>This slide will override the presentation transition and zoom!</h2>
</section>

<section data-transition-speed="fast">
	<h2>Choose from three transition speeds: default, fast or slow!</h2>
</section>
```

 您也可以为同一张幻灯片使用不同的进入和离开过渡： 

```
<section data-transition="slide">
    The train goes on …
</section>
<section data-transition="slide">
    and on …
</section>
<section data-transition="slide-in fade-out">
    and stops.
</section>
<section data-transition="fade-in slide-out">
    (Passengers entering and leaving)
</section>
<section data-transition="slide">
    And it starts again.
</section>
```

您也可以从这些值当中选择： `none`, `fade`, `slide`, `convex`, `concave` 和`zoom`.

#### 内部链接<div id="internal-links"></div>

幻灯片之间的链接很容易。 下面第一个例子是针对某一张幻灯片进行链接, 而第二个, 则用 ID 属性进行链接至另一张幻灯片 ```<section id="some-slide"> ```

```
<a href="#/2/2">Link</a>
<a href="#/some-slide">Link</a>
```

你还可以添加相对导航链接, 类似于内置在 `reveal.js` 的控件, 可以在任何元素上附加以下其中一个 class 。需要注意的是, 在它的基础上, 当前的幻灯片一个有效的导航路线的每个元素将会被自动给予 `enabled` 类。

```
<a href="#" class="navigate-left">
<a href="#" class="navigate-right">
<a href="#" class="navigate-up">
<a href="#" class="navigate-down">
<a href="#" class="navigate-prev"> <!-- 之前幻灯片垂直或水平滑动 -->
<a href="#" class="navigate-next"> <!-- 下一个幻灯片垂直或水平滑动 -->
```

#### 片段<div id="fragments"></div>

片段被用于突出幻灯片上单个元素。这类 ```片段``` 的每个元素都将在下一个幻灯片之前显示。这里有个例子：  http://revealjs.com/#/fragments 

默认片段风格是启动了淡入淡出效果。这种风格可以通过在片段中添加不同类而被改变不同效果。

```
<section>
	<p class="fragment grow">grow</p>
	<p class="fragment shrink">shrink</p>
	<p class="fragment fade-out">fade-out</p>
	<p class="fragment fade-up">fade-up (also down, left and right!)</p>
	<p class="fragment fade-in-then-out">fades in, then out when we move to the next step</p>
	<p class="fragment fade-in-then-semi-out">fades in, then obfuscate when we move to the next step</p>
	<p class="fragment highlight-current-blue">blue only once</p>
	<p class="fragment highlight-red">highlight-red</p>
	<p class="fragment highlight-green">highlight-green</p>
	<p class="fragment highlight-blue">highlight-blue</p>
</section>
```

 可以通过包装将多个片段顺序应用于同一元素 ,  这将在第一步中淡出文本，而在第二步中淡出 。

```
<section>
	<span class="fragment fade-in">
		<span class="fragment fade-out">I'll fade in, then out</span>
	</span>
</section>
```

片段的显示顺序可以通过 `data-fragment-index` 属性来控制。

```
<section>
	<p class="fragment" data-fragment-index="3">Appears last</p>
	<p class="fragment" data-fragment-index="1">Appears first</p>
	<p class="fragment" data-fragment-index="2">Appears second</p>
</section>
```

#### 片段事件<div id="fragment-events"></div>

当任一幻灯片片段显示或隐藏时 `reveal.js` 将派发一个事件。

一些库, 如 `MathJax` （见 [#505](https://github.com/hakimel/reveal.js/issues/505)）, 被最初隐藏的片段元素弄糊涂了 。 通常，可以通过从此回调调用其update或render函数来解决此问题。 

```
Reveal.addEventListener( 'fragmentshown', function( event ) {
	// event.fragment = the fragment DOM element
} );
Reveal.addEventListener( 'fragmenthidden', function( event ) {
	// event.fragment = the fragment DOM element
} );
```

#### 代码语法高亮<div id="code-syntax-highlighting"></div>

默认情况下, Reveal 配置了 [highlight.js](https://highlightjs.org/) 来支持代码语法高亮。 要启用语法突出显示，您将必须加载突出显示插件([plugin/highlight/highlight.js](https://github.com/hakimel/reveal.js/blob/master/plugin/highlight/highlight.js)) 和Highlight.js CSS主题（Reveal随附于Monokai主题中： [lib/css/monokai.css](https://github.com/hakimel/reveal.js/blob/master/lib/css/monokai.css) ）。 

```
Reveal.initialize({
	// More info https://github.com/hakimel/reveal.js#dependencies
	dependencies: [
		{ src: 'plugin/highlight/highlight.js', async: true },
	]
});
```

 下面是一个带有 clojure 代码的示例，该示例将突出显示语法。存在 ```data-trim``` 属性时，会自动删除周围的空格。HTML将默认转义。为了避免这种情况，例如，如果您正在使用 ```<mark>``` 来调用一行代码，请将 ```data-noescape``` 属性添加到 ```<code>``` 元素。 

```
<section>
	<pre><code data-trim data-noescape>
(def lazy-fib
  (concat
   [0 1]
   <mark>((fn rfib [a b]</mark>
        (lazy-cons (+ a b) (rfib b (+ a b)))) 0 1)))
	</code></pre>
</section>
```

#### 行号和高亮<div id=""></div>

要启用行号，请将 ```data-line-number``` 添加到您的 ```<code>``` 标记中。如果要突出显示特定行，则可以使用相同属性提供逗号分隔的行号列表。例如，在以下示例中，第4行和第8-11行突出显示： 

```
<pre><code class="hljs" data-line-numbers="4,8-11">
import React, { useState } from 'react';
 
function Example() {
  const [count, setCount] = useState(0);
 
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
</code></pre>
```

#### 幻灯片页码<div id="slide-number"></div>

如果要显示当前幻灯片的页码，可以使用 ```slideNumber``` 和 ```showSlideNumber``` 配置值来显示。

```
// 使用默认格式显示幻灯片编号
Reveal.configure({ slideNumber: true });

// 可以使用以下变量配置幻灯片页码格式：
//  "h.v": 	水平 . 垂直 幻灯片页码 (default)
//  "h/v": 	水平 / 垂直 幻灯片页码
//    "c": 	幻灯片页码
//  "c/t": 	幻灯片页码 / 总幻灯片
Reveal.configure({ slideNumber: 'c/t' });

// 您可以提供一个功能来完全自定义数字：
Reveal.configure({ slideNumber: function() {
    // 忽略垂直幻灯片的页码
    return [ Reveal.getIndices().h ];
}});

// 使用“showSlideNumber”值控制显示哪些幻灯片页码：
//     "all": 显示所有视图（默认）
// "speaker": 只显示演讲注释视图上的幻灯片页码
//   "print": 只显示打印为PDF的幻灯片页码
Reveal.configure({ showSlideNumber: 'speaker' });
```

#### 预览模式<div id="overview-mode"></div>

按 `“ESC”` 或 `“O”` 键来打开和关闭概览模式。当你在这种模式下, 你仍然可以在幻灯片之间导航, 因此你的演示文稿需要在千分尺以上。 预览模式有以下几个API钩子：

```
Reveal.addEventListener( 'overviewshown', function( event ) { /* ... */ } );
Reveal.addEventListener( 'overviewhidden', function( event ) { /* ... */ } );

// 以编程方式切换概览模式
Reveal.toggleOverview();
```

#### 全屏模式<div id="fullscreen-mode"></div>

只要按下键盘上的 `F` 键来全屏显示你的演示文稿。按 `Esc` 键退出全屏模式。

#### 嵌入式媒体<div id="embedded-media"></div>

 如果希望在幻灯片显示时自动开始播放，请将 ```data-autoplay``` 添加到您的媒体元素： 

```
<video data-autoplay src="http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4"></video>
```

如果要全局启用或禁用自动播放，对于所有嵌入式媒体，可以使用 `autoPlayMedia` 配置选项。如果将其设置为 `true` ，则无论单独的 `data-autoplay` 属性如何，所有媒体都将自动播放。如果使用 `autoPlayMedia：false` 初始化，媒体不会自动播放。 

请注意，当您离开幻灯片时，嵌入式HTML5  `<video>` / `<audio>` 和YouTube / Vimeo iframe会自动暂停。可以通过在元素上添加 `data-ignore` 属性来禁用此功能。 

####  嵌入式iframe

reveal.js 自动将两个 [post messages](https://developer.mozilla.org/en-US/docs/Web/API/Window.postMessage) 推送到嵌入式iframe。`slide: start` 当包含 iframe 的幻灯片变得可见，`slide: stop` 当隐藏时。 

#### 延伸元素<div id="stretching-elements"></div>

有时需要使某个元素（例如图像或视频）伸展以在给定幻灯片中占用尽可能多的空间。这可以通过将 `.stretch` 类添加到元素中来完成，如下所示： 

```
<section>
	<h2>This video will use up the remaining space on the slide</h2>
    <video class="stretch" src="http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4"></video>
</section>
```

局限性：

- 幻灯片的直接后代才能被拉伸
- 每个幻灯片部分只能拉伸一个后代


#### Resize 事件<div id="resize-event"></div>

当 reveal.js 更改幻灯片的比例时，它会触发一个调整大小事件。您可以订阅事件以相应地调整元素的大小。 

```
Reveal.addEventListener( 'resize', function( event ) {
	// event.scale, event.oldScale, event.size
} );
```

#### postMessage API<div id="postmessage-api"></div>

该框架具有内置的 postMessage API，当与另一个窗口内的演示文稿进行通信时可以使用该API。以下是一个示例，显示了如何在给定的窗口中制作一个 reveal.js 实例，继续进行幻灯片2：

```
<window>.postMessage( JSON.stringify({ method: 'slide', args: [ 2 ] }), '*' );
```

当Reveal.js在iframe中运行时，可以选择将其所有事件冒泡给父级。冒泡事件是带有三个字段的字符串化 JSON：namespace，eventName和state。从父窗口订阅它们的方法如下： 

```
window.addEventListener( 'message', function( event ) {
	var data = JSON.parse( event.data );
	if( data.namespace === 'reveal' && data.eventName ==='slidechanged' ) {
		// Slide changed, see data.state for slide number
	}
} );
```

可以使用配置标志打开或关闭此跨窗口消息传递。 

```
Reveal.initialize({
	// ...

	// 通过 window.postMessage 暴露 reveal.js API
	postMessage: true,

	// 通过 postMessage 派发 reveal.js 的事件给父窗口
	postMessageEvents: false
});
```

