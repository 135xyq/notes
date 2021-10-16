# jquery

## jquery代码书写位置的三种

```javascript
        $(document).ready(function() {
            var box = document.getElementById('box');
            console.log(box);
        });
        
        
        $().ready(function() {
            var box = document.getElementById('box');
            console.log(box);
        });
        
        
        $(function() {
            var box = document.getElementById('box');
            console.log(box);
        })
```
dom元素加载完就会触发ready

### jquery的特点：
1. 强大的选择器
```javascript
    <script>
        var $h1 = $('h1');
        console.log($h1);
    </script>
```
2. 链式操作

    原生js取到的dom对象和jquery取到的不一样。  
    原生js取到的对象不能使用jquery里面的方法。  
    jquery取到的对象也不能使用使用原生的js方法。

### 原生js和jquery元素之间可以相互转化：  
原生js转jquery： $(dom对象);   
jquery转原生js： $jquery对象[0];

jquery取到的永远是一个数组

## [jquery选择器](https://www.jquery123.com/category/selectors/)

### 基础选择器
```javascript
    <div id="box">不错</div>
    <div class="className">你好</div>
    <p>p标签</p>
    <script>
        $('*').css('border', '2px solid black'); //通配符选择器
        $('#box').css('background', 'red'); //ID选择器
        $('.className').css('background', 'green'); //class选择器
        $('p').css('background', 'blue'); //标签选择器
    </script>
```
### 层级选择器：可参考CSS3选择器
    <div class="wrapper">
        <div class="content">啊这</div>
        <p>不错</p>
    </div>
    <script>
        $('.wrapper p').css('color', 'green');
    </script>
```
### 属性选择器：
```javascript
    <div name="t">不错</div>
    <div title="j">就这</div>
    <div title="j-t">啊这</div>
    <div title="jr">棒</div>
    <div title="ttj">强</div>
    <div title="qgrp">加油</div>
    <div title="qgp">冲</div>
    <p id="xyq">很好</p>
    <script>
        $('[name]').css('background', 'red'); //选择所有带name属性的元素
        $('[title=j]').css('background', 'green'); //选择title属性值为j的元素
        $('div[title!=j]').css('background', 'blue'); //选择有title属性值不为j的元素   
        $('div[title|=j]').css('background', 'red'); //选择有title属性值以j前缀开始（- 隔开的）的元素   j-
        $('div[title^=j]').css('background', 'yellow'); //选择有title属性值以j开始的元素
        $('div[title$=j]').css('background', 'hotpink'); //选择有title属性值以j结束的元素
        $('div[title*=gr]').css('background', 'purple'); //选择有title属性值包含gr字符串的元素
        $('div[title~=gr]').css('background', 'purple'); //选择有title属性值包含gr单词（单词之间用空格隔开）的元素
    </script>
```
### [基础过滤选择器](https://www.jquery123.com/category/selectors/basic-filter-selectors/)



### [DOM操作](https://www.jquery123.com/category/manipulation/)：



腾讯云
对象存储

## 自定义插件：
### 1 .给jquery对象本身扩展方法
```javascript
$.extend( {
    函数名：function(){
        函数体    
    }
});
```
使用：$.函数名();

### 2. 给jquery DOM对象扩展方法
```javascript
$.fn.extend( {
    函数名：function(){
        //$(this)指向调用该方法的对象
        $(this).jquery方法;
        
        return $(this);//满足链式调用
    }
});
```
 或者：
```javascript
 $.fn.函数名 = function(){
        //$(this)指向调用该方法的对象
        $(this).jquery方法;
        
        return $(this);//满足链式调用
 }
```
 使用：
 $(dom对象).函数名();

attr 方法和 prop 方法都是用来设置属性值的，区别在于 attr 方法用于设置一般属性，而 prop 用来设置特殊属性。如果是自定义属性，使用 attr 方法来进行设置。当然，设置自定义属性，还可以使用 jquery 中提供的 data 方法。


hide（）方法可以隐藏元素  
show() 方法可以展示元素  
hover() 方法可以设置hover 需传递两个参数，是两个函数，第一个函数处理·移入，第二个函数处理移出

user-select:none；禁止选中 CSS

$(dom).load(html页面) ：可以在一个页面中加载其他页面