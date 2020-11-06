#### 管理多个单页应用（多页面配置）

单页面应用可以理解为webpack的标准模式，直接在entry中指定单页应用的入口即可。

多页应用按照功能模块划分成多个单页面应用，每个单页应用生成一个HTML文件，可以使用AutoWebPlugin来完成简单自动化的构建，但是前提是项目的，目录结构必须遵守预设的规范。需要注意的是：

- 每个页面都有公共的代码，可以将这些代码抽离出来，避免重复的加载。比如，每个页面都引用了同一套css样式表
- 随着业务的不断扩展，页面可能会不断的追加，所以一定要让入口的配置足够灵活，避免每次添加新页面还需要修改构建配置

项目源码结构如下：

```
├── pages
│   ├── index
│   │   ├── index.css // 该页面单独需要的 CSS 样式
│   │   └── index.js // 该页面的入口文件
│   └── login
│       ├── index.css
│       └── index.js
├── common.css // 所有页面都需要的公共 CSS 样式
├── google_analytics.js
├── template.html
└── webpack.config.js
```

从目录结构中可以看出以下几点要求：

1. 所有单页应用的代码都需要放到一个目录下：例如pages目录下
2. 一个单页应用一个单独的文件夹，例如最后胜出index.html相关的代码都在index目录下
3. 每个单页应用的目录下都有一个index.js文件作为入口执行文件

安装

```bash
npm i web-webpack-plugin --save-dev
```

webpack配置文件修改如下:

```javascript
const { AutoWebPlugin } = require("web-webpack-plugin")
//使用本文的
```

