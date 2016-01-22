最近发现一个特别变态的事情. 
= =,,,,,不会言语, 直接上代码,然后说现象。

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
![101.200.236.138/warp.html](https://raw.githubusercontent.com/xianglgd/Blog/master/3d%E5%8A%A0%E9%80%9F%2C%E5%9B%BE%E5%BD%A2%E5%B1%82/img/qrcode.jpg)
有木有发现 那个滚动区域简直卡的要死呀？？？？

为什么呢？？
电脑上打开chrome 浏览器,发现下图这样。

![没有layer](https://raw.githubusercontent.com/xianglgd/Blog/master/3d%E5%8A%A0%E9%80%9F%2C%E5%9B%BE%E5%BD%A2%E5%B1%82/img/nolayer.png)

囧,,,也没什么吗,滚动起来也蛮快的。

![打开chrome模仿手机](https://raw.githubusercontent.com/xianglgd/Blog/master/3d%E5%8A%A0%E9%80%9F%2C%E5%9B%BE%E5%BD%A2%E5%B1%82/img/scene.png)

可是，当我用chrome 模仿手机的时候,神器的事情就发生了。

尼玛，，，，，怎么创建了这么多层？？ 怪不得不卡,不卡死你才怪。 

![打开chrome模仿手机](https://raw.githubusercontent.com/xianglgd/Blog/master/3d%E5%8A%A0%E9%80%9F%2C%E5%9B%BE%E5%BD%A2%E5%B1%82/img/layer.png).

囧，，，，，为什么会这样？？？
瞧瞧告诉你,你一个div ,overflow:auto; 里面内容过多产生滚动条后,用chrome 模拟手机, 就会发现,这个div 有一个层(layer).

为何会产生层呢？？
产生层的条件不是([(产生复合层条件)网上摘取](http://div.io/topic/1348))。

1. 3D 或透视变换(perspective transform) CSS 属性
使用加速视频解码的 元素
2. 拥有 3D (WebGL) 上下文或加速的 2D 上下文的 元素
3. 混合插件(如 Flash)
4. 对自己的 opacity 做 CSS 动画或使用一个动画 webkit 变换的元素
5. 拥有加速 CSS 过滤器的元素
6. 元素有一个包含复合层的后代节点(换句话说，就是一个元素拥有一个子元素，该子元素在自己的层里)
7. 元素有一个 z-index 较低且包含一个复合层的兄弟元素(换句话说就是该元素在复合层上面渲染)

目前来看,我们这不符合任何一条呀？？？

= =,,,,,百思不得其解. 
最好只好来解决这个问题啦。解决方法如下.

1. ```<div>inDiv</div>``` 设置起 position:static;
2. .inwarp 去掉overflow:hidden;
3. 给 pageMain 添加一个3d转化.例如 transform: translate3d(0,0,0); (推荐使用这个,因为上面两个css属性,在布局的时候很可能使用到)

然后大家可以看下,正常时的效果(采用的第二种方法)
囧，，，采用第二种方法,你会发现第一个
```<div class='inwarp'>sssss<div>inDiv</div></div>```
依然会有自己的层。
并且还发现,在手机的 uc 浏览器上,两个页面滚动效果一样流畅。
 = =,这是 chrome的问题呢,还是 chrome的问题呢,还是chrome的问题呢?
 
![http://101.200.236.138/no3d.html](https://raw.githubusercontent.com/xianglgd/Blog/master/3d%E5%8A%A0%E9%80%9F%2C%E5%9B%BE%E5%BD%A2%E5%B1%82/img/nolayercode.jpg)

