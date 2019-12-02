# 1-1：html

面试重要性：⭐️⭐️⭐️

需要整理的知识如下：

1、html doctype等基础知识

2、DOM相关知识

3、html5语义化相关知识

## 基础知识

`<!DOCTYPE html>` — 文档类型。混沌初分，HTML 尚在襁褓（大约是 1991/92 年），DOCTYPE 用来链接一些 HTML 编写守则，有点像自动校正等。然而现在已经没有人关心这些，只是因为历史原因必须将它们保留，但没有实际作用。现在你只需要知道这些就可以。

`<meta charset="utf-8">` — 这个元素指定了当前文档使用 UTF-8 字符编码 ，UTF-8 包括绝大多数人类已知语言的字符。基本上 UTF-8 可以处理任何文本内容，还可以避免以后出现某些问题，我们没有任何理由再选用其他编码。

***

## 面试题

** 1.DOCTYPE有什么作用？标准模式与混杂模式如何区分？它们有何意义? **

  告诉浏览器使用哪个版本的HTML规范来渲染文档。DOCTYPE不存在或形式不正确会导致HTML文档以混杂模式呈现。

  标准模式（Standards mode）以浏览器支持的最高标准运行；混杂模式（Quirks mode）中页面是一种比较宽松的向后兼容的方式显示。（如果没有声明DOCTYPE，默认就是这个模式）

** 2.meta标签 **

  提供给页面的一些元信息（名称/值对），有助于SEO。

  属性值：

  - `name`：名称/值对中的名称。author、description、keywords、generator、revised、others。 把 content 属性关联到一个名称。

  - `http-equiv`：没有name时，会采用这个属性的值。content-type、expires、refresh、set-cookie。把content属性关联到http头部

  - `content`：名称/值对中的值， 可以是任何有效的字符串。 始终要和 name 属性或 http-equiv 属性一起使用

  - `scheme`：用于指定要用来翻译属性值的方案

** 3.HTML5为什么只需要写 `<!DOCTYPE HTML>`？ **

  HTML5不基于SGML（Standard Generalized Markup Language 标准通用标记语言），因此不需要对DTD（DTD 文档类型定义）进行引用，但是需要DOCTYPE来规范浏览器行为。

  HTML4.01基于SGML，所以需要引用DTD。才能告知浏览器文档所使用的文档类型，如下：
  `<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">`

** 4.xhtml和html有什么区别 **

  html是一种基本的web网页设计语言，xhtml是基于xml的标记语言

  区别：
  - xhtml元素必须被正确的嵌套
  - xhtml元素必须被关闭
  - 标签名必须使用小写
  - xhtml必须拥有根元素

** 5.quirks模式是什么？它和standards模式有什么区别？ **

  在ie6之前版本，如果网页没有声明DTD，浏览器会向前兼容，采用兼容之前的布局方式。就是quirks模式，也叫做怪异模式。

  区别：
  - 盒模型：在w3c标准中，如果设置一个元素的宽度和高度，指的是元素内容的宽度和高度，而在quirks模式下，ie的宽度和高度还包含了padding和border；

  - 设置行内元素的高宽:在标准模式下，给行内元素设置宽高都不会生效，而在quirks模式下，则会生效，上下margin也会生效。

  - 设置百分比的宽高：在standards模式下，一个元素的宽高是由其包含的内容来决定的；如果父元素没有设置百分比的宽高，子元素设置一个百分比的宽高是无效的。而怪异模式下，子元素的百分比宽度生效，高度贼怪异（未知解答）。（附：父元素未设置宽高，子元素百分比宽高ie8以下版本一样全部生效）

  - 用margin：0 auto；设置水平居中：在标准模式下可以，而在怪异模式下则不行。


** 6.行内元素有哪些？块级元素有哪些？ 空(void)元素有那些？ **

- 行内元素：`a span img input select`

- 块级元素：`div ul ol li dl dt dd h1 p`

- 空元素：`<br> <hr> <link> <meta>`

** 7.页面导入样式时，使用link和@import有什么区别？ **

相同的地方，都是外部引用CSS方式，区别：

  1. link是xhtml标签，除了加载css外，还可以定义RSS等其他事务；@import属于CSS范畴，只能加载CSS
  2. link引用CSS时候，页面载入时同时加载；@import需要在页面完全加载以后加载，而且@import被引用的CSS会等到引用它的CSS文件被加载完才加载
  3. link是xhtml标签，无兼容问题；@import是在css2.1提出来的，低版本的浏览器不支持
  4. link支持使用javascript控制去改变样式，而@import不支持
  5. link方式的样式的权重高于@import的权重
  6. import在html使用时候需要`<style type="text/css">`标签

** 8.无样式内容闪烁（FOUC）Flash of Unstyle Content **

  `@import`导入CSS文件会等到文档加载完后再加载CSS样式表。因此，在页面DOM加载完成到CSS导入完成之间会有一段时间页面上的内容是没有样式的。

  解决方法：使用link标签加载CSS样式文件。因为link是顺序加载的，这样页面会等到CSS下载完之后再下载HTML文件，这样先布局好，就不会出现FOUC问题。

** 9.介绍一下你对浏览器内核的理解？ **

  主要分成两部分：渲染引擎(Layout Engine或Rendering Engine)和JS引擎。

  渲染引擎：负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入CSS等），以及计算网页的显示方式，然后会输出至显示器或打印机。浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。

  JS引擎：解析和执行javascript来实现网页的动态效果。

  最开始渲染引擎和JS引擎并没有区分的很明确，后来JS引擎越来越独立，内核就倾向于只指渲染引擎。

** 10.常见的浏览器内核有哪些？ **

  1. Trident( MSHTML )：IE MaxThon TT The World 360 搜狗浏览器
  2. Geckos：Netscape6及以上版本 FireFox Mozilla Suite/SeaMonkey
  3. Presto：Opera7及以上(Opera内核原为：Presto，现为：Blink)
  4. Webkit：Safari Chrome

** 11.HTML5有哪些新特性,移除了那些元素？如何处理HTML5新标签的浏览器兼容问题？如何区分HTML和HTML5？ **

- 新增加了图像、位置、存储、多任务等功能。

- 新增元素：
  1. canvas
  2. 用于媒介回放的 `video` 和 `audio` 元素
  3. 本地离线存储。localStorage长期存储数据，浏览器关闭后数据不丢失；sessionStorage的数据在浏览器关闭后自动删除
  4. 语意化更好的内容元素，比如 `article footer header nav section`
  5. 位置API：Geolocation
  6. 表单控件：`calendar date time email url search`
  7. 新的技术：web worker(web worker是运行在后台的 JavaScript，独立于其他脚本，不会影响页面的性能。您可以继续做任何愿意做的事情：点击、选取内容等等，而此时 web worker 在后台运行) web socket
  8. 拖放API：drag、drop

- 移除的元素：

  1. 纯表现的元素：`basefont big center font s strike tt u`
  2. 性能较差元素：`frame frameset noframes`

- 区分：

  1. DOCTYPE声明的方式是区分重要因素
  2. 根据新增加的结构、功能来区分

** 12.简述一下你对HTML语义化的理解？ **

  1. 用正确的标签做正确的事情。
  2. html语义化让页面的内容结构化，结构更清晰，便于对浏览器，搜索引擎解析；
  3. 即使在没有样式CSS情况下也以一种文档格式显示，并且是容易阅读的；
  4. 搜索引擎的爬虫也依赖于HTML标记确定上下文和各个关键字的权重，利于SEO;
  5. 使阅读源代码的人对网站更容易将网站分块，便于阅读维护理解。

** 13. src和href的区别 **

  src是指向外部资源的位置，指向的内容会嵌入到文档中当前标签所在的位置，在请求src资源时会将其指向的资源下载并应用到文档内，如js脚本，img图片和frame等元素。当浏览器解析到该元素时，会暂停其他资源的下载和处理，知道将该资源加载、编译、执行完毕，所以一般js脚本会放在底部而不是头部。

  href是指网络资源所在位置，建立和当前元素（锚点）或当前文档（链接）之间的链接，用于超链接。

** 14.HTML5的文件离线储存怎么使用，工作原理是什么？ **

在线情况下，浏览器发现HTML头部有manifest属性，它会请求manifest文件，如果是第一次访问，那么浏览器就会根据manifest文件的内容下载相应的资源，并进行离线存储。如果已经访问过并且资源已经离线存储了，那么浏览器就会使用离线的资源加载页面。然后浏览器会对比新的manifest文件与旧的manifest文件，如果文件没有发生改变，就不会做任何操作，如果文件改变了，那么就会重新下载文件中的资源，并且进行离线存储。例如：

在页面头部加入manifest属性

```<html manifest='cache.manifest'>```

在cache.manifest文件中编写离线存储的资源

```html
CACHE MANIFEST
#v0.11
CACHE:
js/app.js
css/style.css
NETWORK:
Resourse/logo.png
FALLBACK:
 //offline.html
```

** 15.cookies，sessionStorage和localStorage的区别？ **

  共同点：都是保存在浏览器端，且是同源的。

  区别：

  1. cookies是为了标识用户身份而存储在用户本地终端上的数据，始终在同源http请求中携带，即cookies在浏览器和服务器间来回传递，而sessionstorage和localstorage不会自动把数据发给服务器，仅在本地保存。
  2. 存储大小的限制不同。cookie保存的数据很小，不能超过4k，而sessionstorage和localstorage保存的数据大，可达到5M。
  3. 数据的有效期不同。cookie在设置的cookie过期时间之前一直有效，即使窗口或者浏览器关闭。sessionstorage仅在浏览器窗口关闭之前有效。localstorage始终有效，窗口和浏览器关闭也一直保存，用作长久数据保存。
  4. 作用域不同。cookie在所有的同源窗口都是共享；sessionstorage不在不同的浏览器共享，即使同一页面；localstorage在所有同源窗口都是共享

** 16.iframe框架有那些优缺点？ **

- 优点：

  1. iframe能够原封不动的把嵌入的网页展现出来。
  2. 如果有多个网页引用iframe，那么你只需要修改iframe的内容，就可以实现调用的每一个页面内容的更改，方便快捷。
  3. 网页如果为了统一风格，头部和版本都是一样的，就可以写成一个页面，用iframe来嵌套，可以增加代码的可重用。
  4. 如果遇到加载缓慢的第三方内容如图标和广告，这些问题可以由iframe来解决。

- 缺点：

  1. 搜索引擎的爬虫程序无法解读这种页面
  2. 框架结构中出现各种滚动条
  3. 使用框架结构时，保证设置正确的导航链接。
  4. iframe页面会增加服务器的http请求

** 17.label的作用是什么? 是怎么用的? **

  label标签用来定义表单控件间的关系,当用户选择该标签时，浏览器会自动将焦点转到和标签相关的表单控件上。label 中有两个属性是非常有用的, FOR和ACCESSKEY。

  FOR属性功能：表示label标签要绑定的HTML元素，你点击这个标签的时候，所绑定的元素将获取焦点。例如，

  `<Label FOR="InputBox">姓名</Label><input ID="InputBox" type="text">`

  ACCESSKEY属性功能：表示访问label标签所绑定的元素的热键，当您按下热键，所绑定的元素将获取焦点。例如，

  `<Label FOR="InputBox" ACCESSKEY＝"N">姓名</Label><input ID="InputBox" type="text">`

** 18.HTML5的form如何关闭自动完成功能？ **

  HTML的输入框可以拥有自动完成的功能，当你往输入框输入内容的时候，浏览器会从你以前的同名输入框的历史记录中查找出类似的内容并列在输入框下面，这样就不用全部输入进去了，直接选择列表中的项目就可以了。但有时候我们希望关闭输入框的自动完成功能，例如当用户输入内容的时候，我们希望使用AJAX技术从数据库搜索并列举而不是在用户的历史记录中搜索。

  方法：

  1. 在IE的internet选项菜单中里的自动完成里面设置
  2. 设置form输入框的autocomplete为on或者off来来开启输入框的自动完成功能

** 19.如何实现浏览器内多个标签页之间的通信? **

  - WebSocket SharedWorker
  - 也可以调用 localstorge、cookies 等本地存储方式。 localstorge 在另一个浏览上下文里被添加、修改或删除时，它都会触发一个事件，我们通过监听事件，控制它的值来进行页面信息通信。

  注意：Safari 在无痕模式下设置 localstorge 值时会抛出QuotaExceededError 的异常

** 20.webSocket如何兼容低浏览器？ **

  1. Adobe Flash Socket ActiveX HTMLFile (IE) 基于 multipart 编码发送 XHR 基于长轮询的 XHR
  2. 引用WebSocket.js这个文件来兼容低版本浏览器。

** 21.页面可见性（Page Visibility）API 可以有哪些用途？ **

  1. 通过visibility state的值得检测页面当前是否可见，以及打开网页的时间。
  2. 在页面被切换到其他后台进程时，自动暂停音乐或视频的播放。

** 22.如何在页面上实现一个圆形的可点击区域？ **

  1. map+area或者svg
  2. border-radius
  3. 纯js实现，一个点不在圆上的算法

** 23.实现不使用 border 画出1px高的线，在不同浏览器的Quirks mode和CSS Compat模式下都能保持同一效果 **

  `<div style="height:1px;overflow:hidden;background:red"></div>`

** 24.网页验证码是干嘛的，是为了解决什么安全问题？ **

  1. 区分用户是计算机还是人的程序;
  2. 可以防止恶意破解密码、刷票、论坛灌水；

** 25.`title`与`h1`的区别、`b`与`strong`的区别、`i`与`em`的区别？ **

- `title`属性没有明确意义，只表示标题；`h1`表示层次明确的标题，对页面信息的抓取也有很大的影响
- `strong`标明重点内容，语气加强含义；`b`是无意义的视觉表示
- `em`表示强调文本；`i`是斜体，是无意义的视觉表示
- 视觉样式标签：`b i u s`
- 语义样式标签：`strong em ins del code`

** 26.元素的alt和title有什么异同？ **

  在alt和title同时设置的时候，alt作为图片的替代文字出现，title是图片的解释文字。

** 27. 渐进增强和优雅降级 **

  - 渐进增强：针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能，达到更好的用户体验。

  - 优雅降级：一开始就构建完整的功能，然后再针对低版本的浏览器进行兼容。

  - 区别：优雅降级是从复杂的现状开始，并试图减少用户体验的供给，而渐进增强则是从一个非常基础的，能够起作用的版本开始，并不断扩充，以适应未来环境的需要。

  - 降级（功能衰减）意味着往回看；而渐进增强则意味着朝前看，同时保证其根基处于安全地带。

    - “优雅降级”观点

    “优雅降级”观点认为应该针对那些最高级、最完善的浏览器来设计网站。而将那些被认为“过时”或有功能缺失的浏览器下的测试工作安排在开发周期的最后阶段，并把测试对象限定为主流浏览器（如 IE、Mozilla 等）的前一个版本。

    在这种设计范例下，旧版的浏览器被认为仅能提供“简陋却无妨 (poor, but passable)” 的浏览体验。你可以做一些小的调整来适应某个特定的浏览器。但由于它们并非我们所关注的焦点，因此除了修复较大的错误之外，其它的差异将被直接忽略。

    - “渐进增强”观点

    “渐进增强”观点则认为应关注于内容本身。

    内容是我们建立网站的诱因。有的网站展示它，有的则收集它，有的寻求，有的操作，还有的网站甚至会包含以上的种种，但相同点是它们全都涉及到内容。这使得“渐进增强”成为一种更为合理的设计范例。这也是它立即被 Yahoo! 所采纳并用以构建其“分级式浏览器支持 (Graded Browser Support)”策略的原因所在。

** 28. defer和async的区别 **

  defer要等到整个页面在内存中正常渲染结束（DOM结构完全生成，以及其他脚本执行完成），才会执行。多个defer脚本会按照它们在页面出现的顺序加载。**渲染完再执行**

  async一旦下载完，渲染引擎就会中断渲染，执行这个脚本以后，再继续渲染。多个async脚本是不能保证加载顺序的。**下载完就执行**


** 29.viewport 所有属性？ **

  1. width :设置layout viewport的宽度，为一个正整数，或字符串'device-width';
  2. initial-scale:设置页面的初始缩放值，为一个数字，可以带小数。
  3. minimum-scale:允许用户的最小缩放值，为一个数字，可以带小数。
  4. maximum-scale:允许用户的最大缩放值，为一个数字，可以带小数。
  5. height:设置layout viewport的高度，这个属性对我们并不重要，很少使用
  6. user-scalable:是否允许用户进行缩放，值为‘no’或者‘yes’。(安卓中还支持：target-densitydpi，表示目标设备的密度等级，作用是决定css中的1px 代表多少物理像素)
  8. target-densitydpi:值可以为一个数值或者 high-dpi 、 medium-dpi、 low-dpi、 device-dpi 这几个字符串中的一个


** 30.media属性？screen？All？max-width?min-width? **

  media 属性规定被链接文档将显示在什么设备上。media 属性用于为不同的媒介类型规定不同的样式。Screen计算机默认屏幕，all适用于所有设备，max-width超过最大宽度就不执行，min-width必须大于最小宽度才执行。

