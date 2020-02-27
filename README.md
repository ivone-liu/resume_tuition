## 新的一年，找到新的工作？让我们用CSS Grid属性制作一个漂亮简历！

![原文地址](https://css-tricks.com/new-year-new-job-lets-make-a-grid-powered-resume/)

许多流行的简历设计是将模块布置成网格状态来充分利用网页的空间。我们用CSS Grid来创建一个无论是打印还是在不同尺寸显示器上都看起来很优雅的简历。这样，无论是离线和在线都可以正常使用简历，这种小技巧在新的一年里可能会派上用场。

![css-grid-resume.png](https://i.loli.net/2020/02/27/UniNVJKg2urw1tx.png)

首先，我们要创建一个存放简历的容器和简历的内容模块。

```html
<article class="resume">
    <section class="name"></section>
    <section class="photo"></section>
    <section class="about"></section>
    <section class="work"></section>
    <section class="education"></section>
    <section class="community"></section>
    <section class="skills"></section>
</article>
```

开始使用Grid之前，我们添加 `display:gird` 来作为布置简历的外部元素。接下来，我会解释其他的组件应该怎样放入页面的布局当中。在这个案例中，我按照两列四行来布局。

我们使用CSS Grid的`fr`单位来指分配可用空间。我们给所有的行相等的空间（每行`1fr`），并且设置第一列的宽度为第二列的两倍（`2fr`）.


```css
.resume {
  display: grid;
  grid-template-columns: 2fr 1fr;
  grid-template-rows: 1fr 1fr 1fr 1fr;
}
```

![css-grid-tabel.jpg](https://i.loli.net/2020/02/27/8Nse9KQAZLPqCI1.jpg)

下一步我来说明这些元素在使用 `grid-template-area` 属性时如何被放入网格中。首先，我们需要使用 `grid-area` 来命名模块。名字可以随便一些，这里我们将使用与类相同的名称：

```css
.name {
    grid-area: name;
}

.photo {
    grid-area: photo;
}
```

现在到了最有趣的部分，这能让整个布局变得轻而易举：将网格放在`grid-template-areas`属性区域中。比如，我们要想让姓名(`name`)显示在简历的左上方，就需要将这部分放置在`grid-template-area`区域的左上方。由于简历的工作(`work`)介绍信息较多，所以我分成了两个区域来展示。

```css
.resume {
  grid-template-areas:
    "name photo"
    "work about"
    "work education"
    "community skills";
}
```

这是到目前我们所能看到的样子

***tips: CSS Grid提供了许多十分有用的属性，比如调整大小、页面布局以及许多简略的属性。我们通过展示一个可能的方式来让元素变得简单。去学习一些不错的代码思想来让你的CSS Grid表现得更出色。***

### 调整布局


![layout1](https://i.loli.net/2020/02/27/TsuzdKYLBhi1ClO.png)

![layout2](https://i.loli.net/2020/02/27/tr6zaPi9IuBolYO.png)

![layout3](https://i.loli.net/2020/02/27/Y9F2nPZtJc4WKUN.png)

![layout4](https://i.loli.net/2020/02/27/g1YOPMcrGmx7ihq.png)