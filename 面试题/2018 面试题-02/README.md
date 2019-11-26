# CSS 面试题

- Q: 什么是 css 盒模型
  在网页中，一个元素在网页中实际的空间大小，实际上是由：内容`content` + 外边距`margin` + 内边距`padding` + 边框`border` 构成

---

- Q: CSS 有哪些样式可以给子元素继承?
  可继承的:`1. font-size,2. font-weight, 3. line-height, 4. color, 5. cursor`等
  不可继承的一般是会改变盒子模型的:`display,margin、border、padding、height`等

---

- Q: box-sizing 常用的属性有哪些? 分别有啥作用?
  box-sizing 有两个值:content-box(W3C 标准盒模型),border-box(怪异模型),
  这个 css 主要是改变盒子模型大小的计算形式：padding + width + border 或者 将 padding 和 border 直接计算在 width 中
  用一个栗子举例,一个 div 的宽高分别 100px,border 为 5px,padding 为 5px

  ```html
  <style>
    .test {
      box-sizing: content-box;
      border: 5px solid #f00;
      padding: 5px;
      width: 100px;
      height: 100px;
    }
  </style>
  <div class="test"></div>
  <!-- 
  1. content-box的计算公式会把宽高的定义指向 content, border和 padding 另外计算,
  也就是说 content + padding + border = 120px(盒子实际大小)
  2. border-box的计算公式是总的大小涵盖这三者, content 会缩小,来让给另外两者
  content(80px) + padding(5*2px) + border(5*2px) = 100px
  -->
  ```

---

- Q: 清除浮动的方式有哪些?比较好的是哪一种?
  常用的一般为三种`.clearfix`伪元素, `clear:both`,`overflow:hidden`;
  比较好是 .clearfix:

  ```css
  /* 1. 通过父元素清除浮动，即给浮动元素的父元素添加如下样式 */
  .clearfloat:after {
    display: block;
    clear: both;
    content: "";
    visibility: hidden;
    height: 0;
  }
  .clearfloat {
    zoom: 1;
  }
  /* 2. 在浮动元素的最后元素后添加一个空元素，添加如下样式*/
  .clearfloat {
    clear: both;
  }
  ```

---

- Q: 行内元素有哪些？块级元素有哪些？ 空(void)元素有那些？
  行内元素：`a、b、span、img、input、strong、select、label、em、button、textarea`
  块级元素：`div、ul、li、dl、dt、dd、p、h1-h6、blockquote`
  空元素：即系没有内容的 HTML 元素，例如：`br、meta、hr、link、input、img`

---

- 如何使用 css 实现垂直居中，通过定位的方式+设置外边距的方式：

  ```html
  <style>
    .father {
      width: 500px;
      height: 500px;
      position: relative;
      background-color: red;
    }
    .son {
      width: 200px;
      height: 200px;
      position: absolute;
      top: 50%;
      left: 50%;
      margin-left: -100px; /*根据父元素定位，定位到父元素中间，然后先左边上边分别移动自己宽高的一半*/
      margin-top: -100px;
      background-color: yellow;
    }
  </style>
  <div class="father">
    <div class="son"></div>
  </div>
  ```

---

- Q: display:none 和 visibility:hidden 的区别？
  1. display:none 隐藏对应的元素，在文档布局中不再给它分配空间，它各边的元素会合拢，
     就当他从来不存在。
  2. visibility:hidden 隐藏对应的元素，但是在文档布局中仍保留原来的空间。

---

- CSS 中 link 和@import 的区别是？
  (1) link 属于 HTML 标签中的属性，而@import 是 CSS 提供的;
  (2) 页面被加载的时，link 会同时被加载，而@import 引用的 CSS 会等到页面被加载完再加载;
  (3) import 只在 IE5 以上才能识别，而 link 是 HTML 标签，无兼容问题;
  (4) link 方式的样式的权重 高于@import 的权重;

---

- Q: css 如何控制 div 的显示和隐藏

  ```html
  <style type="text/css">
    .container {
      width: 400px;
      height: 200px;
      border: 2px solid #ff0000;
    }
    .cu_toolbar {
      background-color: #8bb907;
      height: 100px;
      width: 100px;
      display: none;
    }
    .container:hover .cu_toolbar {
      display: block;
    }
  </style>
  <div class="container">
    <div class="cu_toolbar"></div>
  </div>
  ```

---

- Q: CSS 属性是否区分大小写？

  不区分

---

- Q: 对行内元素设置 margin-top 和 margin-bottom 是否起作用
  答：不起作用。（需要注意行内元素的替换元素 img、input，他们是行内元素，但是可以为其设置宽高，并且 margin 属性也是对其起作用的，有着类似于 Inline-block 的行为）。看具体效果：

---

- Q: CSS 选择器有哪些？哪些属性可以继承？
  1. CSS 选择符：id 选择器(#myid)、类选择器(.myclassname)、标签选择器(div, h1, p)、相邻选择器(h1 + p)、子选择器（ul > li）、后代选择器（li a）、通配符选择器（\*）、属性选择器（a[rel=”external”]）、伪类选择器（a:hover, li:nth-child）
  2. 可继承的属性：font-size, font-family, color
  3. 不可继承的样式：border, padding, margin, width, height
  4. 优先级（就近原则）：!important > [ id > class > tag ] && !important 比内联优先级高

---

- Q: CSS 优先级算法如何计算？
  元素选择符： 1
  class 选择符： 10
  id 选择符：100
  元素标签：1000
  !important 声明的样式优先级最高，如果冲突再进行计算。
  如果优先级相同，则选择最后出现的样式。
  继承得到的样式的优先级最低。

---

- Q: SS3 新增伪类有那些?
  p:first-of-type 选择属于其父元素的首个元素
  p:last-of-type 选择属于其父元素的最后元素
  p:only-of-type 选择属于其父元素唯一的元素
  p:only-child 选择属于其父元素的唯一子元素
  p:nth-child(2) 选择属于其父元素的第二个子元素
  :enabled :disabled 表单控件的禁用状态。
  :checked 单选框或复选框被选中。

---

- Q: 如何居中 div？如何居中一个浮动元素？如何让绝对定位的 div 居中？

  ```html
  <style>
    div {
      border: 1px solid red;
      margin: 0 auto;
      height: 50px;
      width: 80px;
    }
    /* 浮动元素的上下左右居中： */
    .fl {
      border: 1px solid red;
      float: left;
      position: absolute;
      width: 200px;
      height: 100px;
      left: 50%;
      top: 50%;
      margin: -50px 0 0 -100px;
    }
    /* 绝对定位的左右居中： */
    .fl {
      border: 1px solid black;
      position: absolute;
      width: 200px;
      height: 100px;
      margin: 0 auto;
      left: 0;
      right: 0;
    }
    /* 也可以使用flex布局 */
  </style>
  <div class="fl"></div>
  ```

---

- Q: display 有哪些值？说明他们的作用?
  inline（默认）–内联
  none–隐藏
  block–块显示
  table–表格显示
  list-item–项目列表
  inline-block 行内块

---

- Q: position 的值？
  static（默认）：按照正常文档流进行排列；
  relative（相对定位）：不脱离文档流，参考自身静态位置通过 top, bottom, left, right 定位；
  absolute(绝对定位)：参考距其最近一个不为 static 的父级元素通过 top, bottom, left, right 定位；
  fixed(固定定位)：所固定的参照对像是可视窗口。

---

- Q: CSS3 有哪些新特性？
  RGBA 和透明度
  background-image background-origin(content-box/padding-box/border-box) background-size background-repeat
  word-wrap（对长的不可分割单词换行）word-wrap：break-word
  文字阴影：text-shadow： 5px 5px 5px #FF0000;（水平阴影，垂直阴影，模糊距离，阴影颜色）
  font-face 属性：定义自己的字体
  圆角（边框半径）：border-radius 属性用于创建圆角
  边框图片：border-image: url(border.png) 30 30 round
  盒阴影：box-shadow: 10px 10px 5px #888888
  媒体查询：定义两套 css，当浏览器的尺寸变化时会采用不同的属性

---

- Q: 请解释一下 CSS3 的 flexbox（弹性盒布局模型）,以及适用场景？
  该布局模型的目的是提供一种更加高效的方式来对容器中的条目进行布局、对齐和分配空间。在传统的布局方式中，block 布局是把块在垂直方向从上到下依次排列的；而 inline 布局则是在水平方向来排列。弹性盒布局并没有这样内在的方向限制，可以由开发人员自由操作。
  试用场景：弹性布局适合于移动前端开发，在 Android 和 ios 上也完美支持。

---

- Q: 用纯 CSS 创建一个三角形的原理是什么？
  首先，需要把元素的宽度、高度设为 0。然后设置边框样式。

  ```css
  width: 0;
  height: 0;
  border-top: 40px solid transparent;
  border-left: 40px solid transparent;
  border-right: 40px solid transparent;
  border-bottom: 40px solid #ff0000;
  ```

---

- Q: 一个满屏品字布局如何设计?
  第一种真正的品字：
  三块高宽是确定的；
  上面那块用 margin: 0 auto;居中；
  下面两块用 float 或者 inline-block 不换行；
  用 margin 调整位置使他们居中。
  第二种全屏的品字布局:
  上面的 div 设置成 100%，下面的 div 分别宽 50%，然后使用 float 或者 inline 使其不换行。

---

- Q: 常见的兼容性问题？

  1. 不同浏览器的标签默认的 margin 和 padding 不一样。\*{margin:0;padding:0;}
     IE6 双边距 bug：块属性标签 float 后，又有横行的 margin 情况下，在 IE6 显示 margin 比设置的大。hack：display:inline;将其转化为行内属性。
  2. 渐进识别的方式，从总体中逐渐排除局部。首先，巧妙的使用“9”这一标记，将 IE 浏览器从所有情况中分离出来。接着，再次使用“+”将 IE8 和 IE7、IE6 分离开来，这样 IE8 已经独立识别。
  3. 渐进识别的方式，从总体中逐渐排除局部。首先，巧妙的使用“9”这一标记，将 IE 浏览器从所有情况中分离出来。接着，再次使用“+”将 IE8 和 IE7、IE6 分离开来，这样 IE8 已经独立识别。

  ```css
   {
    background-color: #f1ee18; /*所有识别*/
    .background-color: #00deff\9; /*IE6、7、8识别*/
    +background-color: #a200ff; /*IE6、7识别*/
    _background-color: #1e0bd1; /*IE6识别*/
  }
  ```

  4. 设置较小高度标签（一般小于 10px），在 IE6，IE7 中高度超出自己设置高度。hack：给超出高度的标签设置 overflow:hidden;或者设置行高 line-height 小于你设置的高度。
  5. IE 下，可以使用获取常规属性的方法来获取自定义属性,也可以使用 getAttribute()获取自定义属性；Firefox 下，只能使用 getAttribute()获取自定义属性。解决方法:统一通过 getAttribute()获取自定义属性。
  6. Chrome 中文界面下默认会将小于 12px 的文本强制按照 12px 显示,可通过加入 CSS 属性 -webkit-text-size-adjust: none; 解决。
  7. 超链接访问过后 hover 样式就不出现了，被点击访问过的超链接样式不再具有 hover 和 active 了。解决方法是改变 CSS 属性的排列顺序:L-V-H-A ( love hate ): a:link {} a:visited {} a:hover {} a:active {}

---

- Q: 为什么要初始化 CSS 样式
  因为浏览器的兼容问题，不同浏览器对有些标签的默认值是不同的，如果没对 CSS 初始化往往会出现浏览器之间的页面显示差异。

---

- Q: display:none 与 visibility：hidden 的区别？
  display：none 不显示对应的元素，在文档布局中不再分配空间（回流+重绘）
  visibility：hidden 隐藏对应元素，在文档布局中仍保留原来的空间（重绘）

---

- Q: 设置元素浮动后，该元素的 display 值是多少？
  自动变成 display:block

---

- Q: 移动端的布局用过媒体查询吗？
  通过媒体查询可以为不同大小和尺寸的媒体定义不同的 css，适应相应的设备的显示。

  ```css
  <head>里边<link rel=”stylesheet” type=”text/css” href=”xxx.css” media=”only screen and (max-device-width:480px)”>
  CSS : @media only screen and (max-device-width:480px) {/css样式/}
  ```

---

- Q: 使用 CSS 预处理器吗？
  Less sass

---

- Q: CSS 优化、提高性能的方法有哪些？
  避免过度约束
  避免后代选择符
  避免链式选择符
  使用紧凑的语法
  避免不必要的命名空间
  避免不必要的重复
  最好使用表示语义的名字。一个好的类名应该是描述他是什么而不是像什么
  避免！important，可以选择其他选择器
  尽可能的精简规则，你可以合并不同类里的重复规则

---

- Q: 浏览器是怎样解析 CSS 选择器的？
  CSS 选择器的解析是从右向左解析的。若从左向右的匹配，发现不符合规则，需要进行回溯，会损失很多性能。若从右向左匹配，先找到所有的最右节点，对于每一个节点，向上寻找其父节点直到找到根元素或满足条件的匹配规则，则结束这个分支的遍历。两种匹配规则的性能差别很大，是因为从右向左的匹配在第一步就筛选掉了大量的不符合条件的最右节点（叶子节点），而从左向右的匹配规则的性能都浪费在了失败的查找上面。
  而在 CSS 解析完毕后，需要将解析的结果与 DOM Tree 的内容一起进行分析建立一棵 Render Tree，最终用来进行绘图。在建立 Render Tree 时（WebKit 中的「Attachment」过程），浏览器就要为每个 DOM Tree 中的元素根据 CSS 的解析结果（Style Rules）来确定生成怎样的 Render Tree。

---

- Q: 在网页中的应该使用奇数还是偶数的字体？为什么呢？
  使用偶数字体。偶数字号相对更容易和 web 设计的其他部分构成比例关系。Windows 自带的点阵宋体（中易宋体）从 Vista 开始只提供 12、14、16 px 这三个大小的点阵，而 13、15、17 px 时用的是小一号的点。（即每个字占的空间大了 1 px，但点阵没变），于是略显稀疏。

---

- Q: margin 和 padding 分别适合什么场景使用？

  何时使用 margin：
  需要在 border 外侧添加空白
  空白处不需要背景色
  上下相连的两个盒子之间的空白，需要相互抵消时。

  何时使用 padding：
  需要在 border 内侧添加空白
  空白处需要背景颜色
  上下相连的两个盒子的空白，希望为两者之和。
  兼容性的问题：在 IE5 IE6 中，为 float 的盒子指定 margin 时，左侧的 margin 可能会变成两倍的宽度。通过改变 padding 或者指定盒子的 display：inline 解决。

---

- Q: 元素竖向的百分比设定是相对于容器的高度吗？
  当按百分比设定一个元素的宽度时，它是相对于父容器的宽度计算的，但是，对于一些表示竖向距离的属性，例如 padding-top , padding-bottom , margin-top , margin-bottom 等，当按百分比设定它们时，依据的也是父容器的宽度，而不是高度。

---

- Q: 全屏滚动的原理是什么？用到了 CSS 的哪些属性？
  原理：有点类似于轮播，整体的元素一直排列下去，假设有 5 个需要展示的全屏页面，那么高度是 500%，只是展示 100%，剩下的可以通过 transform 进行 y 轴定位，也可以通过 margin-top 实现
  overflow：hidden；transition：all 1000ms ease；

---

- Q: 什么是响应式设计？响应式设计的基本原理是什么？如何兼容低版本的 IE？
  响应式网站设计(Responsive Web design)是一个网站能够兼容多个终端，而不是为每一个终端做一个特定的版本。基本原理是通过媒体查询检测不同的设备屏幕尺寸做处理。页面头部必须有 meta 声明的 viewport。

  ```html
  <meta
    name="viewport"
    content="width=device-width"
    initial-scale="1."
    maximum-scale="1"
    user-scalable="no"
  />
  ```

---

- Q: 视差滚动效果？
  视差滚动（Parallax Scrolling）通过在网页向下滚动的时候，控制背景的移动速度比前景的移动速度慢来创建出令人惊叹的 3D 效果。
  CSS3 实现:
  优点：开发时间短、性能和开发效率比较好，缺点是不能兼容到低版本的浏览器
  jQuery 实现:
  通过控制不同层滚动速度，计算每一层的时间，控制滚动效果。
  优点：能兼容到各个版本的，效果可控性好
  缺点：开发起来对制作者要求高
  插件实现方式:
  例如：parallax-scrolling，兼容性十分好

---

- Q: (::before) 和 (:after) 中双冒号和单冒号有什么区别？解释一下这 2 个伪元素的作用
  单冒号(:)用于 CSS3 伪类，双冒号(::)用于 CSS3 伪元素。
  ::before 就是以一个子元素的存在，定义在元素主体内容之前的一个伪元素。并不存在于 dom 之中，只存在在页面之中。
  :before 和 :after 这两个伪元素，是在 CSS2.1 里新出现的。起初，伪元素的前缀使用的是单冒号语法，但随着 Web 的进化，在 CSS3 的规范里，伪元素的语法被修改成使用双冒号，成为::before ::after

---

- Q: 你对 line-height 是如何理解的？
  行高是指一行文字的高度，具体说是两行文字间基线的距离。CSS 中起高度作用的是 height 和 line-height，没有定义 height 属性，最终其表现作用一定是 line-height。
  单行文本垂直居中：把 line-height 值设置为 height 一样大小的值可以实现单行文字的垂直居中，其实也可以把 height 删除。
  多行文本垂直居中：需要设置 display 属性为 inline-block。

---

- Q: 怎么让 Chrome 支持小于 12px 的文字？

  ```CSS
  p{font-size:10px;-webkit-transform:scale(0.8);} //0.8是缩放比例
  ```

---

- Q: 让页面里的字体变清晰，变细用 CSS 怎么做？
  -webkit-font-smoothing 在 window 系统下没有起作用，但是在 IOS 设备上起作用-webkit-font-smoothing：antialiased 是最佳的，灰度平滑。

---

- Q: position:fixed;在 android 下无效怎么处理？

  ```HTML
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no"/>
  ```

---

- Q: 如果需要手动写动画，你认为最小时间间隔是多久，为什么？
  多数显示器默认频率是 60Hz，即 1 秒刷新 60 次，所以理论上最小间隔为 1/60＊1000ms ＝ 16.7ms。

---

- Q: li 与 li 之间有看不见的空白间隔是什么原因引起的？有什么解决办法？
  行框的排列会受到中间空白（回车空格）等的影响，因为空格也属于字符,这些空白也会被应用样式，占据空间，所以会有间隔，把字符大小设为 0，就没有空格了。
  解决方法：
  可以将<li>代码全部写在一排
  浮动 li 中 float：left
  在 ul 中用 font-size：0（谷歌不支持）；可以使用 letter-space：-3px

---

- Q: display:inline-block 什么时候会显示间隙？
  有空格时候会有间隙 解决：移除空格
  margin 正值的时候 解决：margin 使用负值
  使用 font-size 时候 解决：font-size:0、letter-spacing、word-spacing

---

- Q: 有一个高度自适应的 div，里面有两个 div，一个高度 100px，希望另一个填满剩下的高度
  外层 div 使用 position：relative；高度要求自适应的 div 使用 position: absolute; top: 100px; bottom: 0; left: 0

---

- Q: ng、jpg、gif 这些图片格式解释一下，分别什么时候用。有没有了解过 webp？
  png 是便携式网络图片（Portable Network Graphics）是一种无损数据压缩位图文件格式.优点是：压缩比高，色彩好。 大多数地方都可以用。
  jpg 是一种针对相片使用的一种失真压缩方法，是一种破坏性的压缩，在色调及颜色平滑变化做的不错。在 www 上，被用来储存和传输照片的格式。
  gif 是一种位图文件格式，以 8 位色重现真色彩的图像。可以实现动画效果.
  webp 格式是谷歌在 2010 年推出的图片格式，压缩率只有 jpg 的 2/3，大小比 png 小了 45%。缺点是压缩的时间更久了，兼容性不好，目前谷歌和 opera 支持。

---

- style 标签写在 body 后与 body 前有什么区别？
  页面加载自上而下 当然是先加载样式。
  写在 body 标签后由于浏览器以逐行方式对 HTML 文档进行解析，当解析到写在尾部的样式表（外联或写在 style 标签）会导致浏览器停止之前的渲染，等待加载且解析样式表完成之后重新渲染，在 windows 的 IE 下可能会出现 FOUC 现象（即样式失效导致的页面闪烁问题）

---

- Q: CSS 属性 overflow 属性定义溢出元素内容区的内容会如何处理?
  参数是 scroll 时候，必会出现滚动条。
  参数是 auto 时候，子元素内容大于父元素时出现滚动条。
  参数是 visible 时候，溢出的内容出现在父元素之外。
  参数是 hidden 时候，溢出隐藏。

---

- Q: 阐述一下 CSS Sprites
  将一个页面涉及到的所有图片都包含到一张大图中去，然后利用 CSS 的 background-image，background- repeat，background-position 的组合进行背景定位。利用 CSS Sprites 能很好地减少网页的 http 请求，从而大大的提高页面的性能；CSS Sprites 能减少图片的字节。
