### 模态框点击空白不关闭

方法一：

```javascript
$('#myModal').modal({backdrop: 'static', keyboard: false});

//backdrop:static时,空白处不关闭.

//keyboard:false时,esc键盘不关闭.
```

方法二：

```html
<div class="modal" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true" data-backdrop="static" data-keyboard="false">
  <div class="modal-dialog custom-dialog succ-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
        <h4>提示信息</h4>
      </div>
      <div class="modal-body">
        <div><img src="images/loading.gif"><p><span>投标成功！</span><img src="images/success.png"></p></div>
      </div>      
    </div>
  </div>
</div>
```

### 鼠标悬浮显示小手

```css
cursor:pointer;
```

### 滚动框样式

```css
.table-view {
  width: 100%;
  height: 400px;
  min-width: 736px;
  margin: 10px 0 0 0;
  overflow: auto;
  border: 1px solid rgba(228, 228, 228, 1);
}

.table-view::-webkit-scrollbar {
  width: 4px;
  /*height: 4px;*/
}

.table-view::-webkit-scrollbar-thumb {
  border-radius: 10px;
  -webkit-box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.2);
  background: rgba(0, 0, 0, 0.2);
}

.table-view::-webkit-scrollbar-track {
  -webkit-box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.2);
  border-radius: 0;
  background: rgba(0, 0, 0, 0.1);
}
```



### 超长字符串

  一、强制换行
1 word-break: break-all; 只对英文起作用，以字母作为换行依据。

2 word-wrap: break-word; 只对英文起作用，以单词作为换行依据。

3 white-space: pre-wrap; 只对中文起作用，强制换行。


word-break:break-all 和 word-wrap:break-word 都是能使其容器如DIV的内容自动换行，它们的区别在于：

1、word-break:break-all 
假设div宽度为450px，它的内容就会到450px自动换行，如果该行末端有个很长的英文单词，它会把单词截断，一部分保持在行尾，另一部分换到下一行。

2、word-wrap:break-word 
例子与上面一样，但区别就是它会把整个单词看成一个整体，如果该行末端宽度不够显示整个单词，它会自动把整个单词放到下一行，而不会把单词截断掉。

二、禁止换行 

white-space:nowrap; overflow:hidden; text-overflow:ellipsis; 
white-space:nowrap; 是禁止换行。
overflow:hidden; 是让多出的内容隐藏起来，否则多出的内容会撑破容器。
text-overflow:ellipsis; 让多出的内容以省略号...来表达。但是这个属性主要用于IE等浏览器，Opera浏览器用-o-text-overflow:ellipsis; 而Firefox浏览器没有这个功能，多出的内容只能隐藏起来。  