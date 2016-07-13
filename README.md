# stc

高性能前端工作流系统

*注*：该项目还在开发阶段，还不能在项目里直接使用。

## 改进编译性能的几种方式

* 充分利用多核 CPU
* 基于 AST/Token
* 分析依赖树
* 无感知的缓存策略

## 工作流处理步骤

处理流程分为下面 4 个步骤，其中 lint，transpile 和 dependence 里的插件是并行处理，workflow 里的插件是串行处理。

* `lint` - 代码规范检查，如：用 eslint 检查 JS 代码
* `transpile` - 转译，将非标准的 HTML/JS/CSS 转换为标准的文件，如： TypeScript，Less，Sass
* `dependence` - 依赖分析，workflow 里只处理被依赖的文件，提高编译性能
* `workflow` - 内容替换等处理，如：压缩，上 CDN

## 配置文件示例

```js
// stc.config.js

var stc = require('stc');
var uglify = require('stc-uglify');
var eslint = require('stc-eslint');

stc.lint({
    eslint: {plugin: eslint, include: /\.js$/, options: {}}
});

stc.workflow({
    uglify: {plugin: uglify, include: /\.js$/, options: {}}
});

stc.start(); // 启动工作流程

```

## 已经开发完成的插件

### lint

* [x] [stc-eslint](https://github.com/stcjs/stc-eslint) - 使用 ESLint 检查 JavaScript 代码规范
* [x] [stc-empty-file](https://github.com/stcjs/stc-empty-file) - 空文件检测
* [x] [stc-bomdetector](https://github.com/stcjs/stc-bomdetector) - 检测并移除文件 BOM 头
* [x] [stc-csslint](https://github.com/stcjs/stc-csslint) - css校验

### transpile

* [x] [stc-typescript](https://github.com/stcjs/stc-typescript) - 编译 .ts 文件到 JS
* [x] [stc-babel](https://github.com/stcjs/stc-babel) - 使用 Babel 编译 ES2015+ 特性的文件
* [x] [stc-sass](https://github.com/stcjs/stc-sass) - 使用 node-sass 编译 sass 文件
* [x] [stc-less](https://github.com/stcjs/stc-less) - less 转译为 CSS
* [x] [stc-css-autoprefixer](https://github.com/stcjs/stc-css-autoprefixer) - 使用 [Autoprefixer](https://github.com/postcss/autoprefixer) 来进行 CSS 语法的补全

### dependence

### workflow

* [x] [stc-uglify](https://github.com/stcjs/stc-uglify) - 使用 UglifyJS 压缩 JS
* [x] [stc-html-compress](https://github.com/stcjs/stc-html-compress) - 压缩模板文件，支持模板语法
* [x] [stc-css-compress](https://github.com/stcjs/stc-css-compress) - 压缩 CSS 文件，支持模板语法
* [x] [stc-css-combine](https://github.com/stcjs/stc-css-combine) - 合并 @import url 的 CSS 文件
* [x] [stc-js-combine](https://github.com/stcjs/stc-js-combine) - 合并 document.write 的 JS 文件
* [x] [stc-cdn](https://github.com/stcjs/stc-cdn) - 将静态资源上传到 CDN
* [x] [stc-replace](https://github.com/stcjs/stc-replace) - 代码替换功能
* [x] [stc-imagemin](https://github.com/stcjs/stc-imagemin) - 优化 JPG, PNG 和 GIF 等图片
* [x] [stc-inline](https://github.com/stcjs/stc-inline) - 外联资源转为内联资源，小图片转为 base64，js inline 功能

## 需要开发的插件

* [ ] LocalStorage
* [ ] 国际化
* [ ] CSS Sprite
* [ ] requirejs 代码合并
* [ ] seajs 代码合并
* [ ] 静态资源版本号
* [ ] 模板 XSS 自动修复功能
* [ ] HTML 编码规范检测
* [ ] 文件拷贝
* [ ] 文件移动
* [ ] CDN 功能上传到阿里云、七牛、又拍云的适配器
* [ ] Vue.js 代码转译
* [ ] Weex 代码转译
* [ ] 类似 webpack 将项目打包在一起的插件

## 如何开发

[如何开发？](https://github.com/stcjs/stc/wiki/%E5%A6%82%E4%BD%95%E5%BC%80%E5%8F%91%EF%BC%9F)
