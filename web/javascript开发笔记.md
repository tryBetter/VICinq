<h2>JavaScript学习笔记</h2>

<ul>
<li>
<b/>offsetLeft</b> : 元素在 <b>整个文档</b> 中的左侧偏移量，可以理解为 <b>左上角X坐标</b>
</li>

<li>
<b>offsetTop</b> : 元素在 <b>整个文档</b> 中的顶部偏移量，可以理解为 <b>左上角Y坐标</b>
</li>

<li>
<b>offsetParent.scrollLeft</b> : 获取元素在窗口中的水平移动距离
</li>

<li>
<b>offsetParent.scrollTop</b> : 获取元素在窗口中的垂直移动距离
</li>

<li>
<b>jquery设置css样式</b> :<br>
<ul>
<li>设置单个样式 ： <code>$("#id").css("width":"0")</code><br></li>
<li>设置多个样式 ： <code>$("#id").css({"width":"0","height":"0"})</code> </li>
</ul>
</li>

<li>
<b>jquery设置属性值</b> :<br>
<ul>
<li>设置单个属性 ： <code>$("#id").attr("src":"logo.jpg")</code><br></li>
<li>设置多个属性 ： <code>$("#id").attr({"src":"logo.jpg"})</code> </li>
</ul>
</li>

<li><b>jQuery使用自定义的动画效果</b> : <br>
<code>
$("#id").animate({<br>
  "width":"500px",<br>
  "height":"500px" //使被选中元素的宽高变化至500px;<br>})
</code>
</li>

<li><b>jQuery点击事件</b>:<code> <br>
$("#id").click(<br>
  function(){<br>
    //todo<br>
    });</code> </li>
<li><b>在iframe当中调用父窗口的函数</b> : <code><br>window.parent.functionName();</code></li>
<li><b></b> : </li>
</ul>
