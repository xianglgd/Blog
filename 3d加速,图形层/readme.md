最近发现一个特别变态的事情. 
= =,,,,,不会言语, 之间上代码,然后说现象。

css

```
html,body{
	width: 100%;
	height: 100%;
}
 * {
  margin: 0;
  padding: 0;
}
body{
	overflow: auto;
}

#pageMain{
	overflow-y: auto;
    width: 200px;
    height: 300px;
    margin: 50px;
    border: 1px solid black;
}
div{
	position: relative;
}
.inwarp{
	position: static;
	overflow: hidden;
}
```

html

```
<div id="pageMain"></div>
```

js 只为了填充div

```
var html = "<div class='inwarp'>sssss<div>inDiv</div></div>"
var str = "";
for(var i =0 ;i <10000;i++){
	str+=html;
}
pageMain.innerHTML = str;
```

OK, 这三段代码，看似很平常。 没撒特别。
哈哈哈，，，，
但是 大家请拿出手机,扫描下面二维码. 打开网页(请用手机上的chrome浏览器)。
有木有发现 那个滚动区域简直卡的要死呀？？？？

为什么呢？？
电脑上打开chrome 浏览器,发现下图这样。

囧,,,也没什么吗,滚动起来也蛮快的。

可是，当我用chrome 模仿手机的时候,神器的事情就发生了。

尼玛，，，，，怎么创建了这么多层？？ 怪不得不卡,不卡死你才怪。 