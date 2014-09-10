# 多文本控件

---

显示操作多个文本

---


## 目录

  * 简介
  * 创建多个文本
  * 创建多个Html文本
  * 重新设置多个文本

### 简介

  * 多文本控件，可以非常方便的创建多个样式统一的文本，同时保留单个自定义样式
  * 多文本控件支持变化时统一动画功能
  * 多文本控件支持Html文本

### 创建多个文本

  * 直接通过addGroup(Labels,cfg) 的方式添加多个文本
  * 在items中直接指定多个文本的配置信息和坐标信息


````html

<div id="c1"></div>

````

````javascript
seajs.use(['index','achart-canvas'], function(Labels,Canvas) {
  
  var canvas = new Canvas({
    id : 'c1',
    width : 500,
    height : 200
  });

  var labels = canvas.addGroup(Labels,{
    items : [
      {x : 10,y : 20,text : "1"},
      {x : 10,y : 40,text : "2"},
      {x : 10,y : 60,text : "3"},
      {x : 10,y : 80,text : "4"},
      {x : 10,y : 100,text : "5",font : "10px Arial",stroke : "red"},
      {x : 10,y : 120,text : "6"},
      {x : 10,y : 140,text : "7"},
      {x : 10,y : 160,text : "8"}
    ],
    label : {
      font : '20px/1.5 "Helvetica Neue",Helvetica,Arial,sans-serif',
      stroke : '#333',
      x : 10,
      y : 10,
      rotate : 90
    },
    renderer : function(value,item,index){
      if(index % 2 == 0){
        item.rotate = 45;
      }
      return value;
    }
  });

});
````

### 创建html文本

  * 通过custom=true创建自定义html文本
  * 通过html设置容器的模板，模板上必须存在 class="ac-labels" 的样式
  * 通过itemTpl来设置单个文本的模板
  * renderer 可以格式化文本


````html

<div id="c2"></div>

````

````javascript
seajs.use(['index','achart-canvas'], function(Labels,Canvas) {
  
  var canvas = new Canvas({
    id : 'c2',
    width : 500,
    height : 200
  });

  var labels = canvas.addGroup(Labels,{
    items : [
      {x : 10,y : 20,text : "1",'text-anchor' : 'start'},
      {x : 10,y : 40,text : "2"},
      {x : 10,y : 60,text : "3"},
      {x : 10,y : 80,text : "4"},
      {x : 10,y : 100,text : "5"},
      {x : 10,y : 120,text : "6"},
      {x : 10,y : 140,text : "7"},
      {x : 10,y : 160,text : "8"}
    ],
    custom : true,
    label : {
      x : 10,
      y : 10,
      custom : true
    },
    renderer : function(value){
      return '<span>' + value + '</span>'
    }
  });

});
````

### 重新设置文本

  * changeLabel(label,item) 可以单个更改文本，如果animate:true，则触发动画
  * setItems(items) 可以整体替换文本
