# 安装

**基础安装**仅用于创作演示文稿。 **完整安装**使您可以使用所有reveal.js功能和插件，例如演讲注释、开发代码。 

## 基本安装<div id="basic-setup"></div>

reveal.js 的核心是非常容易安装。你只需要直接在浏览器下载该资源库, 并打开 index.html 文件。 

1. 从 https://github.com/hakimel/reveal.js/releases 下载最新版本的 reveal.js

2. 解压缩并用自己的 index.html 替换例子中的内容

3. 在浏览器打开 index.html 并查看它

## 完整安装<div id="full-setup"></div>

 一些 reveal.js 特征, 如额外的 Markdown 和演讲注释, 这要求演示文稿在本地 Web 服务器上运行。以下将说明如何设置服务器, 以及修改 reveal.js 代码所需的所有开发任务。 

1. 安装 [Node.js](http://nodejs.org/) (4.0.0 或更高) 

2. 克隆 reveal.js 仓库

   ```$ git clone https://github.com/hakimel/reveal.js.git```

3. 进入 reveal.js 目录

   ```$ cd reveal.js```

4. 安装依赖

   ```$ npm install```

5.  演示文稿的服务器和监视源文件的修改 

   ```$ npm start```

6. 打开 [http://localhost:8000](http://localhost:8000/) 预览演示文稿

    你可以使用 `npm start -- --port 8001` 修改端口。 

## 目录结构<div id="folder-structure"></div>

* **css/** 核心样式，如果没有这些则项目不起作用 
* **js/** 核心js，如果没有这些则项目不起作用
* **plugin/** 已经作为开发扩展 reveal.js 部件 
* **lib/**  所有第三方资源库(JavaScript, CSS, fonts) 

