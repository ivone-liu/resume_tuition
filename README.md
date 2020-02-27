## 新的一年，找到新的工作？让我们用CSS Grid属性制作一个漂亮简历！

[原文地址](https://css-tricks.com/new-year-new-job-lets-make-a-grid-powered-resume/)

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

![layout1](https://i.loli.net/2020/02/27/TsuzdKYLBhi1ClO.png)

***tips: CSS Grid提供了许多十分有用的属性，比如调整大小、页面布局以及许多简略的属性。我们通过展示一个可能的方式来让元素变得简单。去学习一些不错的代码思想来让你的CSS Grid表现得更出色。***

### 调整布局

`grid-template-areas` 属性让布局变得更简单。比如，如果你认为相比起教育背景来说雇主会对你的技能部分更加关注，你只需要在 `grid-template-areas` 区域中切换模块名称，无需其他的操作就能实现自动交换布局。

```css
.resume {
  grid-template-areas:
    "name photo"
    "work about"
    "work skills"  /* skills now moved above education */
    "community education";
}
```

![resume-02.jpg](https://i.loli.net/2020/02/27/rdIwn6WacXGbV9R.jpg)

![layout2](https://i.loli.net/2020/02/27/tr6zaPi9IuBolYO.png)

我们可以修改很少CSS代码来实现受欢迎的左侧窄列简历设计。这是对于网格来说最合适的应用场景：我们可以重新布局已命名的网格区域，在其他区域变动的时候精确保持原有的位置不变。

```css
.resume {
  grid-template-columns: 1fr 2fr;
  grid-template-areas:
    "photo education"
    "name work"
    "about work"
    "skills community";
}
```

![resume-03-1.jpg](https://i.loli.net/2020/02/27/PNr7yzfVsEGHcA1.jpg)

![layout3](https://i.loli.net/2020/02/27/Y9F2nPZtJc4WKUN.png)


### 分隔栏

如果你想在简历中添加个人资料展示，我们可以在网格模板最下面添加第三列。注意，我们在更新时需要保持列单位的一致，以便于个人资料部分能跨两列保持正常布局。

```css
.resume {
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-areas:
    "name name photo"
    "work work about"
    "work work education"
    "community references skills";
}
```

![resume-04-1.jpg](https://i.loli.net/2020/02/27/omqOv3NRdIVznJb.jpg)

![layout4](https://i.loli.net/2020/02/27/g1YOPMcrGmx7ihq.png)

***tips：在两个模块中间的间隔，可以用grid-gap属性来控制***


### 响应式

对于小尺寸屏幕来说，比如移动设备，我们可以把简历部分放在一个与屏幕等宽的列中。

```css
grid-template-columns: 1fr;
grid-template-areas:
  "photo"
  "name"
  "about"
  "work"
  "education"
  "skills"
  "community"
  "references"
}
```

然后对于较宽的屏幕我们可以使用media query来调整布局。

```css
@media (min-width: 1200px) {
  .resume {
    grid-template-areas:
      "name photo"
      "work about"
      "work education"
      "community skills";
  }
}
```

以上两种尺寸中或许还有一种情况，比如，在类似于平板来说的中等尺寸屏幕，我们或许想将所有的内容放在一个独立列中，但是个人和图片并排在顶部展示。

```css
@media (min-width: 900px) {
  .resume {
      grid-template-columns: 2fr 1fr;
      grid-template-areas:
        "name photo"
        "about about"
        "work work"
        "education education"
        "skills skills"
        "community community"
        "references references"
  }
}
```

<video id="video" controls="" preload="none">
<source id="ogv" src="https://attach-ivone.oss-cn-hongkong.aliyuncs.com/responsive_demo.mov" type="video/mov">
</video>


