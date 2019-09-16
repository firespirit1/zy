## 一、jQuery中的选择器

###  1.基本选择器

> 1、#id: 根据元素的额id属性获取指定的元素
>
> 2、element:根据元素的名称获取指定的元素
>
> 3、selector1,selector2(联合选择器)：匹配所有满足条件的元素，用于将多个不同选择器获取的元素合并到一起，将其封装为jQuery对象并返回。
>
> 4、.class：根据元素的class属性获取指定的元素
>
> 5、js对象显示出来是一个标签的样式
>
> 6、jquery单个对象显示出来 是init
>
> 7、jquery集合对象显示出来是 init(?),集合中存储的是js的单个对象,通过.get()方法获取标签

### 2.层级选择器

**ancestor (**空格**) descendant ：选取祖先元素下的所有后代元素(祖先与后代)**  后代选择器

**parent > child**：选择父元素下的所有子元素（父子关系）

```
举例：
<p><span class="one">11</span></p>
$('div span')可以取到span标签
$('div>span')不能取到span标签
```

**prev + next**：选取同级元素紧邻的下一个元素，如果紧邻的不是next则取不到。

自己总结：如果prev 有好几个相同的紧连接的同级标签，那么选取除了第一个标签之外的所有的相同的同级标签并且和最后一个同级标签的下一个元素。

**prev~siblings**：选取同级元素所有的同级兄弟元素，若siblings为空的话，则取所有的同级兄弟元素



### 3.简单选择器

:first ：匹配第一个元素    *
找div当中的第一个子元素；$('div>:first')
:last ：匹配最后一个元素   *
比如有两个ul 那么匹配最后一个ul，匹配ul当中的子元素也是，先匹配最后一个ul再匹配ul最后一个子元素
:even：匹配所有偶数

:odd ：匹配所有奇数

:eq(index) ：匹配索引为index的元素（默认索引从0开始）

:gt(index)：匹配索引大于index的元素

:lt(index) ：匹配索引小于index的元素

:not(selector)：匹配除指定选择器以外的其他元素

### 4.内容选择器

:contains(text)：匹配内容包含指定文本的元素  *

:empty ：匹配内容为空的元素

:has(selector) ：匹配具有指定选择器的元素*

:parent：匹配具有子元素的元素（内容不为空的元素）

### 5.可见性选择器

**:hidden**：匹配所有隐藏元素(display:none，input type=’hidden’)  *

**:visible**：匹配所有可见元素(display:block) 

注意：隐藏域不能使用show()方法显示，除非改变type属性
<input type="hidden" value="1233455">

### 6.属性选择器*

**[attribute] ：匹配具有指定属性的元素**

**[attribute=value]：匹配属性值等于value的元素**

**[attribute!=value] ：匹配属性值不等于value*的元素**

**[attribute^=value] ：匹配属性值以value开始的元素**

**[attribute$=value] ：匹配属性值以value结尾的元素**

**[attribute\*=value] ：匹配属性值包含value的元素**

**[selectorN]：匹配包含多个属性的元素**

这里匹配的属性也可以是自定义的属性

匹配具有多个指定属性的元素举例：$('div`[`name][color]')

匹配多个属性值举例：$('input`[`type^=s][que=123]')

### 7.表单选择器



```
:input:匹配所有的表单元素
:text ：匹配所有文本框

:password：匹配所有密码框

:radio ：匹配所有单选按钮

:checkbox：匹配所有复选框

:submit ：匹配提交按钮

:reset：匹配重置按钮

:image：匹配图像域

:button：匹配按钮

:file：匹配文件域

:hidden：匹配隐藏表单
```

### 8.表单属性选择器

##  二、DOM与jQuery对象

### 1.DOM对象的定义

使用document.getElementById或document.getElementsByTagName获取的对象就是dom对象。

###  2.jQuery对象的定义

使用$符号选择的元素就是jquery对象。

### 3.DOM与jQuery对象的关系

jquery对象是对dom对象的重新封装，他们之间是可以相互转换的。

### 4.DOM与jQuery对象的相互转换

##  三、jQuery中的属性

### 1.attr属性

### 2.class属性

### 3.csss方法

### 4.offset位置

### 5.元素的尺寸

### 6.文本域值

##  四、jQuery中的属性

###  1.页面载入事件

### 2.window.onload与ready的区别

### 3.常用的事件

### 4.事件的切换









