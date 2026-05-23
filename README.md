# docusaurus-image-viewer
更好的在Docusaurus中查看图片 It's better to see the picture in Docusaurus

在本插件出现之前确实有几个实现相同功能的插件：

https://github.com/gabrielcsapo/docusaurus-plugin-image-zoom

https://github.com/inovector/docusaurus-plugin-zooming

https://github.com/tipsxBase/docusaurus-plugin-image-viewer

除此之外还有其它类似插件。但对于我来说这些并不那么顺手且修改起来不太方便，于是就自己写一个。

# 快速添加

1. 将仓库下载下来：`Code` → `Download zip`
2. 在你项目的根目录中新建文件夹`plugins`
3. 进入`plugins`文件夹，新建`image-viewer`文件夹
4. 打开下载好的压缩包，进入`docusaurus-image-viewer-main`文件夹中
5. 将里面的所有文件解压到`image-viewer`文件夹中
6. 修改`docusaurus.config.js`文件：

**注意：请不要和功能相同的插件一起使用！**

```js

// 其它内容......
  plugins: [
    // 其它内容......
    './plugins/image-viewer',  // 添加此行
    // 其它内容......
  ],

// 其它内容......

  themeConfig:
// 其它内容......
      imageViewer: {
        scale: 1.8,                    // 初始缩放大小
        enableWheelZoom: true,         // 是否启用鼠标滚轮缩放图片
        containerSelector: 'article',  // 插件生效的容器
        excludeSelector: '.avatar',    // 插件排除的容器
        minScale: 0.5,                 // 最小缩放
        maxScale: 5,                   // 最大缩放，当为 Infinity 时可无限放大
        wheelStep: 0.25,               // 滚动一次的缩放倍率
      },
// 其它内容......
```

上面的配置可以写在 `plugins` 中，不用在 `themeConfig` 中添加 ：

```js
// 其它内容......
  plugins: [
    // 其它内容......
    ['./plugins/image-viewer',{scale: 1.8, enableWheelZoom: true, containerSelector: 'article',excludeSelector: '.avatar', minScale: 0.5, maxScale: 5, wheelStep: 0.25,} ],
    // 其它内容......
  ],
// 其它内容......
```
`excludeSelector` 可以写成数组形式：

`excludeSelector: ['.avatar', '.author-avatar-container'],`


## 使用

`Esc` 键：关闭图片预览。

`0` 数字键：恢复为默认缩放值。

触屏设备上可三次快速点击关闭图片预览。

适配深色模式。

`containerSelector` 容器参考：

| 选择器字符串 | 作用范围 |
| - | - |
| `article` | 默认值，只作用于文章正文内容（文档、博客） |
| `.markdown` | 作用于所有带 `markdown` 类的容器，通常也是正文区域 |
| `main` | 作用于 `<main>` 元素，范围比 `article` 略大，可能包含某些页面级容器 |
| `.theme-doc-markdown` | Docusaurus 文档页的 `Markdown` 渲染区域（具体类名可能因主题版本而异） |
| `#__docusaurus` | 整个 Docusaurus 根节点，范围极大，会包含导航等 |
| `article, .blog-post-page` |多个选择器组合，同时覆盖文档和博客页 |
| `.container .row .col` | 更通用的内容容器，但可能误伤其他页面布局 |

如果不确定当前页面结构，可以打开浏览器开发者工具（F12），在 Elements 面板中查看目标图片所在的父级容器，找到唯一的类名或 ID 作为选择器。