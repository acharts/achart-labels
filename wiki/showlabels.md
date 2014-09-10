# 控件使用多个文本

---

控件内部使用多个文本，例如坐标轴有多个文本

---

## 目录

  * 简介
  * 做了什么
  * 如何使用

### 简介

  * Labels 控件提供了批量添加多个文本和改变文本的功能，但是在一个图形分组中使用多个文本时，需要一些共性的操作

    1. 坐标轴中的文本，在坐标轴变化时，文本跟着进行动画，文本的数目也会发生改变
    2. 折线图中的文本也会跟随折线图上点的变化而变化

  * 这些共性的代码我们写在了ShowLabels这个代码片段中，只要有多个文本排列需求的类都可以很容易的 mixin（将属性复制到类的prototype)中

### 做了什么

  * 提供了一个配置项 labels 来配置Labels 控件需要的配置项
  * renderLabels 方法作为渲染多个文本的入口函数
  * removeLabels 方法负责 移除前的清理工作
  * addLabel(text,point) 可以很方便的将文本和坐标点转换成图形上的文本
  * resetLabels(items) 会批量重置文本，并且会触发动画

### 如何使用

  1. 通过 `Util.mixin([ShowLabels])` 引入使用多个文本的功能
  2. 在renderUI 中调用 renderLabels 方法
  3. 将内部的文本通过 addLabel(text,point) 功能添加到Labels对象中
  4. 整体发生改变时调用 resetLabels(items);
  5. 在remove函数中 调用 removeLabels();


````html

<div id="c3"></div>

````

````javascript
seajs.use(['index','achart-canvas','achart-util','achart-plot'], function(Labels,Canvas,Util,Plot) {
  
  var canvas = new Canvas({
    id : 'c3',
    width : 500,
    height : 500
  });

  var A = function(cfg){
    A.superclass.constructor.call(this,cfg);
  };

  A.ATTRS = {
    min : 0,
    step : 20,
    max : 100
  };

  Util.extend(A,Plot.Item);

  Util.mixin(A,[Labels.ShowLabels]);
  
  Util.augment(A,{

    renderUI : function(){
      A.superclass.renderUI.call(this);
      this.renderLabels(); //调用入口文件
      this._initLabels();
    },
    _initLabels : function(){
      var _self = this,
        min = _self.get('min'),
        step = _self.get('step'),
        max = _self.get('max');
  
      for(var i = min; i <= max ; i= i + step){
        _self.addLabel('('+i+','+i+')',{x : i,y : i});
      }
    },
    remove : function(){
      this.removeLabels();//清理文本
      A.superclass.remove.call(this);
    }

  });

  var a = canvas.addGroup(A,{
      min : 50,
      step : 50,
      max : 450,
      labels : {
        label : {
          font : '20px/1.5 "Helvetica Neue",Helvetica,Arial,sans-serif',
          stroke : '#333',
          "text-anchor" : "middle",
          x : 10,
          y : 10,
          rotate : 90
        }
      }
    });

});
````

## 更多

  * 更多的使用，可以查看坐标轴、折线图以及饼图中多个文本的使用
  