# 配置项

在页面的最后，您需要通过运行以下代码来初始化显示。请注意，所有配置值都是可选的，并且将默认为以下指定的值。 

```
Reveal.initialize({

	// 是否在右下角展示控制条
	controls: true,

	// 通过提示帮助用户学习使用控件, 例如当他们第一次遇到垂直滑动时会弹出向下箭头
	controlsTutorial: true,

	// 确定控件出现的位置, "edges" 或者 "bottom-right"
	controlsLayout: 'bottom-right',

	// 向后导航箭头的可见性规则; "faded", "hidden" 或者 "visible"
	controlsBackArrows: 'faded',

	// 显示演示进度条
	progress: true,

	// 显示当前幻灯片的页码
	slideNumber: false,

	// 添加当前幻灯片的页码到URL哈希里面，重新载入页面或者复制URL会返回相同的幻灯片
	hash: false,

	// 将每一张幻灯片的变动记录到浏览器历史记录中。前提是 `hash: true`
	history: false,

	// 启用键盘快捷键进行导航
	keyboard: true,

	// 启用幻灯片概览模式
	overview: true,

	// 幻灯片的垂直居中
	center: true,

	// 在具有触摸输入的设备上启用触摸导航
	touch: true,

	// 循环演示
	loop: false,

	// 把演示的方向改为RTL
	rtl: false,

	// 参考文档中的导航模式，"default", "linear", "grid"
	navigationMode: 'default',

	// 每次演示加载时随机化幻灯片的顺序
	shuffle: false,

	// 全局打开和关闭片段
	fragments: true,

	// 是否在URL中包含当前片段，这样重新加载会回到相同的片段位置
	fragmentInURL: false,

	// 演示文稿是否以嵌入式模式运行,
	// 换而言之，包含在屏幕的有限区域内
	embedded: false,

	// 当按下问号键，是否显示帮助
	help: true,

	// 演讲注释是否对所有人可见
	showNotes: false,

	// 全局自动播放嵌入式媒体 (视频/音频/iframe)
	// - null: 有data-autoplay时，媒体会自动播放
	// - true: 无论单独设置如何，所有媒体都会自动播放
	// - false: 无论设置如何，都不会自动播放媒体
	autoPlayMedia: null,

	// 全局预加载延迟加载的iframe
	// - null: 有data-src和data-preload的iframe将在视距内加载，只有data-src的iframe会在可见时加载
	// - true: 视距内加载所有带有data-src的iframe
	// - false: 所有带有data-src的iframe仅在可见时加载
	preloadIframes: null,

	// 两个幻灯片之间自动切换的时间间隔（毫秒）
	// 当设置成 0 的时候则禁止自动切换
	// 该值可以被幻灯片上的 “data-autoslide” 属性覆盖
	autoSlide: 0,

	// 当遇到用户输入的时候停止自动切换
	autoSlideStoppable: true,

	// 当自动滑动时,使用此方法进行导航。
	autoSlideMethod: Reveal.navigateNext,

	// 指定您认为将花费的平均时间（以秒为单位）展示每张幻灯片。
	// 这用来在演讲视图中显示间隔时间
	defaultTiming: 120,

	// 是否启用通过鼠标滚轮来导航幻灯片
	mouseWheel: false,

	// 如果鼠标静止则隐藏
	hideInactiveCursor: true,

	// 鼠标多长时间后隐藏(ms)
	hideCursorTime: 5000,

	// 在移动设备上隐藏地址栏
	hideAddressBar: true,

	// 是否在一个弹出的 iframe 中打开幻灯片中的链接
	// 增加 `data-preview-link` 和 `data-preview-link="false"` 在每一个单独的链接
	previewLinks: false,

	// 切换过渡效果
	transition: 'slide', // none/fade/slide/convex/concave/zoom

	// 过渡速度
	transitionSpeed: 'default', // default/fast/slow

	// 全屏幻灯片背景的过渡效果
	backgroundTransition: 'fade', // none/fade/slide/convex/concave/zoom

	// 加载除当前可见的幻灯片之外的幻灯片数量
	viewDistance: 3,

	// 视差背景图片
	parallaxBackgroundImage: '', // e.g. "'https://s3.amazonaws.com/hakim-static/reveal-js/reveal-parallax-1.jpg'"

	// 视差背景尺寸
	parallaxBackgroundSize: '', // CSS syntax, e.g. "2100px 900px"

	// 每张幻灯片移动视差背景的像素,
	// - 除了指定自动计算
	// - 设置为 0 时,禁止沿轴运动
	parallaxBackgroundHorizontal: null,
	parallaxBackgroundVertical: null,

	// 被用来显示幻灯片的展示模式
	display: 'block'

});
```

初始化后，可以使用 ```configure``` 方法更新配置： 

```
// 关闭自动幻灯片
Reveal.configure({ autoSlide: 0 });

// 每5秒开始自动滑动
Reveal.configure({ autoSlide: 5000 });
```