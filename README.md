# Learning-point
The small demo that studies knowledge point at ordinary times.
前几天做了一个小demo，关于待做事项清单的，可以实现基本的增删查改，页面稍微简洁一点。

TODOList的四个基本功能要求：

•增：添加一个item

•删：逻辑删除、真实删除均可    

 •改：允许修改已添加的事项

 •查：filter 查询过滤

四个功能的实现涉及知识点：js的DOM操作，事件，事件触发之间的逻辑关系，以及如何写入缓存，获取缓存。



HTML结构（先定结构）

```

<div id="app">

  <h1>My TODO List</h1>

        <div class="todomain">
            <ul id="U"> 
            </ul>
        </div>
       <div class="todoadd">
            <input type="text" id="T" placeholder="请输入待做事项">
            <button id="addbtn" onclick="addtolist()">ADD</button>
       </div> 
</div>

```



第一：增加，围绕功能点我打算一步步的来，先从实现增加功能出发。将增加功能实现的结果从代码的角度理解：实现增加功能，即当用户在输入文本框输入值，输完后点击ADD按钮时，我们能获取用户输入的值，并将值添加到<ul id="U"></ul>这个标签里。自动生成的元素不光是文本，文本前部有一个复选框，后有一个删除按钮。大概生成的预期代码例子如下(lable标签可加可不加：待测)：

```

<li id="model"> 
<label>
<input type="checkbox" id="t1" onclick="addline()">
<span>TodoItem的內容</span>
</label>
<button id="delbtn" onclick="delitem()">DEL</button>
</li>

```

知识点掌握：js创建元素 document.createElement("标签名")；复选框是由input标签设置属性type="checkbox"变来的，给标签设置属性利用setAttribute;给button上加文字，利用innerHTML；



向创建好的li标签里追加子元素，利用appendChild()方法。appendChild()是最常用的操作节点的方法，用于向childNodes列表的末尾添加一个节点。

实现思路:给ADD按钮添加一个点击事件onclick="addtolist()"，我们执行的操作交给函数addtolist();

js代码块

```

function addtolist(text1) {
;
//当点击添加按钮时，输入框的文本即立刻添加到上述列表，按序从上到下排列
//动态向ul中添加li元素
var text1=document.getElementById("T").value;//获取文本输入框中的内容
var Li=document.createElement("li");//创建元素li
var Checkbox=document.createElement("input");//创建复选框雏形
var span=document.createElement("span");//创建放置文本内容的span标签
var Btn=document.createElement("button");//创建删除按钮
var oUl = document.getElementsByTagName("ul")[0];//获取到Ul列表

Checkbox.setAttribute("type","checkbox");//创建复选框
Checkbox.setAttribute("id","t1");//给复选框加id名t1
Btn.setAttribute("id","delbtn");
Btn.innerHTML="DEL";//button上加文字DEL
Btn.name="DEL";/**/
span.innerHTML=text1;//向span中添加获取用户输入的文本内容
Li.appendChild(Checkbox);
Li.appendChild(span);
Li.appendChild(Btn);
oUl.appendChild(Li);//向ul追加元素li

}



```

发现问题：

问题一：文本框输入优化

添加了以上代码后，就完成了添加功能，但有一个问题，就是第二次输入时，第一次输入的内容还在文本框，不便于第二次输入。

为此我想到，要优化输入：实现当写一个text添加后，文本框清空（初始化），以便下次输入。



（一个事件触发另一个事件，此处是：点击添加按钮事件后，同时触发清空文本框事件）

解决办法：在函数addtolist里最后添加后续代码

```

//这两行代码，实现每次输完后，输入框的初始化

document.getElementById("T").value="";//把输入文本框的值赋空
document.getElementById("T").focus();//使用了HTML DOM的 focus() 用于为元素设置焦点

```

问题二：对用户的输入添加的值进行判断不为空（if语句）




发现什么都不输入，添加的话也可以，为了防止这种无意义的输入，所以我们需要对输入的值进行判断，空的话，拦截并提示。

解决办法： 用一个if语句判断一下，在方法addtolist里最开始添加if判断代码。

（js代码）

```

if (document.getElementById("T").value.length===0) {
alert("宝贝不能为空噢！");
return;
}

```

问题三：只能点击ADD按钮才能添加，有局限性。（键盘事件的监听，keycode键码,13表示enter键）



实现用户不止按下add按钮可以添加事项，按回车键也可以添加。



解决办法：给input添加一个onkeypress属性

（js代码）

```

//对按下enter键事件(keypress)的监听
document.getElementById("T").onkeypress = function (event) {
if(event.keyCode === 13){
addtolist();
}
};

```

第二，删除，﻿按删除按钮，则对应的事件（即添加时添加的标签，内容统统移除）删除。

知识点掌握：target 事件属性可返回事件的目标节点（触发该事件的节点），如生成事件的元素、文档或窗口。；removeChild()方法移除节点

实现代码（js）：

```

var oUl = document.getElementsByTagName("ul")[0];
              oUl.onclick = function(event) {
                        var event = event || window.event;
                        var target = event.target;
                        if(target.name == "DEL") {
                             target.parentNode.parentNode.removeChild(target.parentNode);
                            }
              };

```

﻿代码分析：思路（待分）





关于样式美化（css部分）

1.（先进行复选框的美化），同时复选框有被点击的特效（复选框样式自定义）


http://www.manongjc.com/article/2204.html 参考文章


主要思路：隐藏原生input，样式定义过程留给label，因为没有多少样式能够对复选框起作用。

css代码块：

```

input[type=checkbox]:checked:before {
content: "\2713";
background: #fffed5;
text-shadow: 1px 1px 1px rgba(0, 0, 0, .2);
font-size: 20px;
text-align: center;
line-height: 8px;
display: inline-block;
width: 13px;
height: 15px;
color: orange;
border: 1px solid #cdcdcd;
border-radius: 4px;
margin: -3px -3px;
text-indent: 1px;
}
input[type=checkbox]:before {
content: "\202A";
background: #ffffff;
text-shadow: 1px 1px 1px rgba(0, 0, 0, .2);
font-size: 20px;
text-align: center;
line-height: 8px;
display: inline-block;
width: 13px;
height: 15px;
color: #00904f;
border: 1px solid #cdcdcd;
border-radius: 4px;
margin: -3px -3px;
text-indent: 1px;
}

```

2. 实现效果，当选中复选框，则文字加上删除线  

其实就是一个小问题css的text-decoration属性: line-through



﻿看了文章https://blog.csdn.net/pehao/article/details/78918650  CSS 实现 checkbox/radio 选中后文本颜色改变。有所启发﻿



得出关键点:


a.使用label包含  input type='checkbox' 这样点击文本就可以勾选

b.勾选后,只有checkbox 或 radio有:selected状态所以只能设置兄弟节点或直接点. 通过将文本放在span中. 


c.使用选择器:     :checked+span  其中 +是相邻兄弟选择器 来实现样式



css代码块


```

input:checked + span {
color: initial;
font-weight: bold;
text-decoration: line-through;
}

```






ps.太傻了，考虑半天，以后搜索的时候先将现象简单描述搜一次，再用专业点的话语

3.所有的按钮样式统一，网上有好多按钮样式，自己选一套喜欢的，copy一下button的css的代码。


我采用的http://www.bootcss.com/p/buttons/

4.其他基本样式自己设置，不难。
第三，修改
当单独击中文字时，可进行修改

第四，查

















