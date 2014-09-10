# achart-labels [![spm version](http://spmjs.io/badge/achart-labels)](http://spmjs.io/package/achart-labels)

---

多个文本排列和显示多个文本的扩展（代码片段）
  
  * [wiki 文档](wiki/)
  * [demo](examples/)

---

## Install

```
$ spm install achart-labels --save
```

## Usage

```js
var Labels = require('achart-labels');

```

## Labels

  * 用于展示多个文本，统一设置文本状态，并支持自定义样式
  * 支持文本的更新和更新过程中的动画
  * 支持自定义html显示文本
  * Labels 继承自 [Plot.Item](http://spmjs.io/docs/achart-plot/#plot-item),继承一切属性和方法


### 配置项

  * items: 多个文本选项，每个文本选项的配置参考 [label配置信息](http://spmjs.io/docs/achart-canvas/#text)
  * label: 所有文本共享的配置信息，参考[label配置信息](http://spmjs.io/docs/achart-canvas/#text)
  * renderer: 格式化文本的函数，函数原型 function(text,item,index)
  * custom: 是否使用自定义文本，如果是true，那么就使用html显示文本
  * html: custom = true时使用的容器的模板 ,必须存在 class = "ac-labels"
  * itemTpl : custom =true时，单个label的模板，必须存在 class = "ac-label"
  * animate : 改变时是否执行动画
  * duration ：执行动画的时间，默认为400ms


### 方法

  * addLabel(item) 添加文本
  * setItems(items) 重置文本
  * changeLabel(label,item) 更改文本


## ShowLabels 

  * 用于内部显示多个文本分组的代码片段，可以通过mixin的方式引入显示多个文本的功能

### 配置项

  * labels 上面 Labels类的配置项

### 方法

  * renderLabels() 渲染labels，入口函数
  * addLabel(text,point) 添加文本
  * resetLabels(items) 重置文本
  * removeLabels() 清除文本

[更详尽的API](http://acharts.github.io/acharts-api/api/index.html#!/api/Chart.Labels)
