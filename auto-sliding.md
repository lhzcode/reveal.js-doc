# 自动滑动

演示文稿可以配置为通过自动滑动, 而无需用户的任何输入。为了启用这个, 你需要告诉框架幻灯片之间应该间隔多少毫秒进行切换。 

```
// 5 秒切换间隔
Reveal.configure({
  autoSlide: 5000
});
```

当启用时, 会出现让用户可以暂停和恢复自动滑动的控件。另外, 滑动可以按键盘上 `A` 键进行恢复和暂停。用户开始手动导航时就会自动暂停滑动。你可以通过 reveal.js 的配置项指定禁用控件： `autoSlideStoppable: false` 。 

你也可以在幻灯片上设置 `data-autoslide` 属性进行覆盖。 

```
<section data-autoslide="2000">
	<p>After 2 seconds the first fragment will be shown.</p>
	<p class="fragment" data-autoslide="10000">After 10 seconds the next fragment will be shown.</p>
	<p class="fragment">Now, the fragment is displayed for 2 seconds before the next slide is shown.</p>
</section>
```

要覆盖用于当自动滑动导航的方法, 你可以指定 `autoSlideMethod` 的设置项。 要仅沿顶层导航并忽略垂直幻灯片 , 这里可以设置为： `Reveal.navigateRight` 。 

每当自动幻灯片模式恢复或者暂停时, `autoslideresumed` 和 `autoslidepaused` 事件会被释放。