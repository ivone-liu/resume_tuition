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

这是到目前我们所能看到的样子 [查看代码](https://github.com/ivone-liu/resume_tuition/tree/master/template_1)

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

[查看代码](https://github.com/ivone-liu/resume_tuition/tree/master/template_2)

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

[查看代码](https://github.com/ivone-liu/resume_tuition/tree/master/template_3)

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

[查看代码](https://github.com/ivone-liu/resume_tuition/tree/master/template_4)

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

[![点击查看录制的响应式布局视频](https://i.loli.net/2020/02/27/crIZCOVnbpoASYJ.png)](https://attach-ivone.oss-cn-hongkong.aliyuncs.com/responsive_demo.mov)

[点击查看录制的响应式布局视频](https://attach-ivone.oss-cn-hongkong.aliyuncs.com/responsive_demo.mov)

### 为单页打印做好准备

如果你需要将你的简历完美得打印在一张纸上，有几件事情需要牢记。最艰难的挑战是需要删除一些文字来适应单页面。

避免展示更多信息而挤压缩小字体，这会让简历阅读起来非常费力。一个很小的技巧是在开发过程中向简历元素添加临时的字体大小约束。

```css
.resume {
  /* for development only */
  width : 210mm;
  height: 297mm;
  border: 1px solid black;
}
```

通过这种A4尺寸的边框设置，能清晰的看到简历能否适应这种尺寸，如果内容会溢出边缘，这就意味着会打印到第二张纸上面。

你可以向CSS来说明打印时哪些元素会隐藏掉，像是浏览器会自动添加的日期和页码。

```css
@media print {
  /* remove any screen only styles, for example link underline */
}

@page {
  padding: 0;
  margin: 0cm;
  size: A4 portrait;
}
```

有一件事情需要强调，不同的浏览器对简历渲染出不同的字体，也就会让简历在尺寸上出现些微的不同。如果你想极为精确地打印简历，另一种选择是将简历存储为PDF文件并且在自己网站上提供文件下载。


### 浏览器支持

现代浏览器对CSS网格特性都有着很不错的支持。

IE浏览器对旧版本的CSS网格的支持需要添加额外的前缀，比如 `grid-template-columns` 就需要写为 `-ms-grid-columns`. 在 [Autoprefixer](https://autoprefixer.github.io/) 上运行编写的CSS代码，可以帮助添加这些前缀，但是手动地修改之后是必须要经过彻底地测试，因为在旧的规范中，有些属性的效果并不相同，而有些则不存在。为了让代码更好的运行，我推荐度以下Daniel Tonon的文章 -- [如何自动配置前缀](https://css-tricks.com/css-grid-in-ie-css-grid-and-the-new-autoprefixer/)。

我们可以编写一些备用代码作为一种可替代的方案，比如说用浮动布局的方法。浏览器在不能识别CSS网格属性的时候，会自动地按照备用的代码来展示。无论你是否要考虑要支持IE，一个备用方案对于确保浏览器在不支持CSS网格是能正常展示你的简历内容（特别是对于有些潜在的不确定性）有着很合理的保障。

---

即便你并不准备在线的简历，用CSS网格来做东西还是很有乐趣，能在写代码的同时探索不同的布局方式，生产一个美观的PDF文件，学习一些CSS令人惊叹的特性。

祝找工作愉快！


