# 键盘绑定

如果你不满意任何默认键盘绑定的, 你可以使用 `keyboard` 配置选项来覆盖它们。

```
Reveal.configure({
  keyboard: {
    13: 'next', // 按下 Enter 键切入下一张幻灯片
    27: function() {}, // 当 Esc 键被按下时执行的方法
    32: null // 当按下 SPACE 键时没有做任何事情（即禁用 reveal.js 默认绑定）
  }
});
```

