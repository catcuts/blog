---
title: 【vue组件开发日志】第2天：调研 PostCSS 2017-07-04
date: 2017-07-05 21:34:42
tags: vue组件开发
description: |
 &emsp;&emsp;PostCSS 用来对开发者编写的 css 文档进行自动化处理的一种工具集合，这个集合中的工具可以由开发者根据处理需求，自由选取和搭配，同时每个工具还可以进行配置，以满足更细化的要求。比如，开发者有对 css 语句自动加浏览器前缀的需求，于是选择 PostCSS 的一款插件，名为“autoprefixer”，同时，在 autoprefixer 中，还可以进行更多细节配置，如“是否保留或自动移除开发者编写的 css 语句中的不必要的前缀”等。其他满足不同需求的插件还有：“CSSNext”（让开发者使用 css4 书写 css ，自动编译成目前浏览器支持的 css 语句）、“px2rem”（顾名思义，px 单位转 rem 单位，rem 更擅长自适应布局）等。 &emsp;&emsp;有人说，PostCSS 不是预处理器，也不是后处理器，不是“未来的语法”，也不是清理或优化工具，但凡是它们能是实现的，它都能做到。这其实就是在说，PostCSS 是什么，就看你需要什么了。...
---
Hi, Welcome Back.

###  一、**PostCSS** 是什么
&emsp;&emsp;**PostCSS** 用来对开发者编写的 **css** 文档进行自动化处理的一种工具集合，这个集合中的工具可以由开发者根据处理需求，自由选取和搭配，同时每个工具还可以进行配置，以满足更细化的要求。比如，开发者有对 **css** 语句自动加浏览器前缀的需求，于是选择 **PostCSS** 的一款插件，名为“**autoprefixer**”，同时，在 **autoprefixer** 中，还可以进行更多细节配置，如“是否保留或自动移除开发者编写的 **css** 语句中的不必要的前缀”等。其他满足不同需求的插件还有：“**CSSNext**”（让开发者使用 **css4** 书写 **css** ，自动编译成目前浏览器支持的 **css** 语句）、“**px2rem**”（顾名思义，**px** 单位转 **rem** 单位，**rem** 更擅长自适应布局）等。
&emsp;&emsp;有人说，**PostCSS** 不是预处理器，也不是后处理器，不是“未来的语法”，也不是清理或优化工具，但凡是它们能是实现的，它都能做到。这其实就是在说，**PostCSS** 是什么，就看你需要什么了。

###  二、为什么要用 **PostCSS**
&emsp;&emsp;一句话，为了从不必要的繁琐易错工作中解放，为了方便地体验到新技术的特性，为了更多已被和将被发掘出来的需求。比如为了兼容浏览器而加的各种前缀，为了体验 **css4** ，为了把 **px** 自动转换为 **rem** 以更好地实现自适应布局。

###  三、如何使用 **PostCSS**
1. 明确你的需求，挑选或开发用于满足这个需求的插件；
2. 使用 **gulp** （需 **gulp-postcss**）或 **webpack** （需 **postcss-loader**） 等综合前端自动化构建工具作为 **PostCSS** 的调用者，编写 **gulp** 任务（**task**）或配置 webpack 加载器（**loader**）；
3. 配置 **PostCSS** 。3种方式：在项目的 **package.json** 中配置，或创建一个 **.postcssrc.json** ，或** .postcssrc.js** / **postcss.config.js** 。前两者都是 **json** ，后面两者允许用户使用 **js** 模块语法；
4. 配置所用插件。这要阅读插件的使用说明。

&emsp;&emsp;如此一来，当你在运行自动化构建时，**PostCSS** 将帮助你实现你所想要的。

###  四、如何在 vue 组件开发中使用 **PostCSS**
&emsp;&emsp;两种方法使用 **PostCSS** 插件：
1.  在 **webpack** 中使用：
```javascript
// webpack.config.js
module.exports = {
// 其他配置...
	plugins: [
		new webpack.LoaderOptionsPlugin({
			vue: {
			// 使用用户自定义插件
				postcss: [require('postcss-cssnext')()] //除了接受插件的数组，postcss 选项也接受...
			}
		})
	]
}
```
2.  在 **vue-loader** 中使用：
```javascript
//vue-loader.conf.js
var utils = require('./utils')
var config = require('../config')
var isProduction = process.env.NODE_ENV === 'production'
module.exports = {
	loaders: utils.cssLoaders({
		sourceMap: isProduction
			? config.build.productionSourceMap
			: config.dev.cssSourceMap,
		extract: isProduction
	}),
	postcss: [
		require('autoprefixer')({
				browsers: ['last 2 versions']
		})
	]
}
```

###  五、**PostCSS** 插件一览
-  [Autoprefixer](https://github.com/postcss/autoprefixer)
-  [CSSnext](http://cssnext.io/)
-  [px2rem](https://github.com/shihuacivis/px2rem)
-  ...

###  六、使用 **PostCSS** 的注意事项
&emsp;&emsp;（后续使用过程中更新）

###  七、周边
-  [PostCSS 插件集：PostCSS.parts: A searchable catalog of PostCSS plugins](https://www.postcss.parts/ "PostCSS.parts: A searchable catalog of PostCSS plugins")
- [CSS 特性兼容检索器：Can I Use](http://caniuse.com/)

###  八、参考
-  [PostCSS 究竟是个什么鬼？](https://happycoder.net/what-is-postcss/ "PostCSS 究竟是个什么鬼？")
-  [使用 cssnext 书写未来的 CSS](http://www.cnblogs.com/nzbin/p/5744672.html "使用 cssnext 书写未来的 CSS")
-  [PostCSS 配置方式](https://github.com/michael-ciniawsky/postcss-load-config)
-  [在 gulp 中快速使用 PostCSS](http://div.io/topic/1575)
-  [在 webpack for vue 中使用 PostCSS](https://juejin.im/post/581bfc368ac247004fe174af)
-  [在 vue-loader 中使用 PostCSS](http://www.jianshu.com/p/21d43d6ed713)
-  [vue-loader 开发指南中文版 - PostCSS](https://lvyongbo.gitbooks.io/vue-loader/content/features/postcss.html)
-  [让 CSS 更完美： PostCSS-modules](https://www.w3cplus.com/preprocessor/postcss-modules-make-css-great-again.html)
-  [CSS Modules: Welcome To the Future](https://glenmaddern.com/articles/css-modules)



