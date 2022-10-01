# 教程

###### 【2022.10.01 SoTWild】

关于Typroa的基本使用方法和Markdown的基本语法很简单可以**自学**，接下来讲一些**进阶食用方法**。

------

### 文章嵌入视频：

目前嵌入**BiliBili**视频最稳定，我们建议使用这种方案。

在原版的B站网页版上，有分享链接，但新版取消了。如果你不想切回旧版，可以使用以下代码：

```html
<iframe src="//player.bilibili.com/player.html?bvid=视频BV号" scrolling="no" border="0" height="600" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>
```

可以调整`height`参数调整视频画面大小。

------

### 文章嵌入音频：

很抱歉，目前本站还未有嵌入音频功能，目前只能通过音乐超链接实现。

------

### 文字样式：

初学**Typroa**时，你也许会抱怨在**Typroa**中不能很好**设置文字样式**，这里给出解决方法：

Typroa在**一定程度上**也是一个**html解析器**，所以可以使用**html语法**进行设置。

###### 1）调整颜色：

```html
<font color="颜色">目标文字</font>
```

<font color="red">红色</font>

###### 2）调整形状：

```html
<font size = "数字">目标文字</font>
$$Latex$$
<em>斜体</em> 或 *斜体*
```

<font size = "6">变大</font>

<font size = "-6">变小</font>

$$Latex$$

<em>斜体</em>

###### 3）文字位置：

```html
<center>居中</center>
<div style="text-align: right">居右</div>
```

<center>居中</center>

<div style="text-align: right">居右</div>

###### 4）链接：

```
[文字](链接)
```

[链接](https://blog.csdn.net/bzb123321/article/details/45092415)

###### 5）图片：

```
![](路径)
```

<img src="https://ts1.cn.mm.bing.net/th/id/R-C.bf782a749ae7ccf9a7689634b030af4c?rik=Vqp4BgzXzVO1BQ&riu=http%3a%2f%2fwww.bala.cc%2fuploads%2fallimg%2f2005%2f1_200521142611_1.jpg&ehk=1VfRP74vKkoyrevcRnA%2fH7%2b0TEBffP%2fFJlHjwagQjC0%3d&risl=&pid=ImgRaw&r=0&sres=1&sresct=1" style="zoom:40%;" />

###### 组合起来：

```html
<center><span style="background:black"><b><em><u><font size = "6"><a href="https://blog.csdn.net/bzb123321/article/details/45092415" target="" title=""><font color="red">又<font size = "8">大</font>又<font size = "4">小</font>的粗斜<font color = "blue">五</font><font color = "purple">颜</font><font color = "yellow">六</font><font color = "green">色</font>底色为黑有下划线的居中链接</font></a></font></u></em></b></span></center>
```

###### 效果：

<center><b><em><u><font size = "6"><span style="background:black"><a href="https://blog.csdn.net/bzb123321/article/details/45092415" target="" title=""><font color="red">又<font size = "8">大</font>又<font size = "4">小</font>的粗斜<font color = "blue">五</font><font color = "purple">颜</font><font color = "yellow">六</font><font color = "green">色</font>底色为黑有下划线的居中链接</font></a></span></font></u></em></b></center>

------

### 下载链接：

实现比较复杂，请附带要下载的文件一并发我处理。

------

### 其他：

[如何在Typora上完整输入化学式？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/363113814)

[typora插入图片调整位置_用中文写代码的博客-CSDN博客_typora 调整图片位置](https://blog.csdn.net/buxiangxiedaima/article/details/115654998)

[使用Typora添加数学公式_姚明明的博客-CSDN博客_typora插入公式](https://blog.csdn.net/mingzhuo_126/article/details/82722455)

[【Typora】超全数学公式全集（没错，你想要的就在这里） - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/165342174)

[typora-数学符号_wait_for_eva的博客-CSDN博客_typora数学符号](https://blog.csdn.net/wait_for_eva/article/details/84307306)