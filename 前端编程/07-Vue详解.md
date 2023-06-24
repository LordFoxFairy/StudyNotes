# VUE：前端体系，前后端分离

## 文档

* [Vue.js](https://v3.cn.vuejs.org/guide/introduction.html)
* [技术胖大佬-Vue3.x系列视频](https://www.bilibili.com/video/BV19z4y1k7Ux?p=2&spm_id_from=pageDriver)
* [狂神说大佬-Vue系列视频](https://www.bilibili.com/video/BV18E411a7mC?spm_id_from=333.999.0.0)
* [Vue Router](https://router.vuejs.org/zh/installation.html)

## 概述

Vue (读音 /vjuː/，类似于 **view**) 是一套用于构建用户界面的**渐进式框架**。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。

**Vue的核心库只关注视图层**，不仅易于上手，还便于与第三方库(如: `vue-router: 跳转`，`vue-resource: 通信`，`vuex:管理)`或既有项目整合。

另一方面，当与==[现代化的工具链](https://v3.cn.vuejs.org/guide/single-file-component.html)==以及各种==[支持类库](https://github.com/vuejs/awesome-vue#components--libraries)==结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。

---

- **Soc原则：关注点分离原则**
- Vue 的核心库只关注视图层，方便与第三方库或既有项目整合。
- HTML + CSS + JS : 视图 ： 给用户看，刷新后台给的数据
- 网络通信 ： axios
- 页面跳转 ： vue-router
- 状态管理：vuex
- Vue-UI : ICE , Element UI

## 前端知识体系

### 前端三要素

- HTML (结构) :超文本标记语言(Hyper Text Markup Language) ，决定网页的结构和内容。
- CSS (表现) :层叠样式表(Cascading Style sheets) ，设定网页的表现样式。
- JavaScript (行为) :是一种弱类型脚本语言，其源代码不需经过编译，而是由浏览器解释运行,用于控制网页的行为。

### 表现层（CSS）

#### CSS层叠样式表

CSS层叠样式表是一门标记语言，并不是编程语言，因此不可以自定义变量，不可以引用等，换句话说就是不具备任何语法支持，它主要缺陷如下：

- 语法不够强大，比如**无法嵌套书写**，导致模块化开发中需要书写很多重复的选择器；
- **没有变量和合理的样式复用机制**，使得逻辑上相关的属性值必须以字面量的形式重复输出，导致**难以维护**；这就导致了我们在工作中无端增加了许多工作量。为了解决这个问题，前端开发人员会使用一种称之为【CSS预处理器】的工具,提供CSS缺失的样式层复用机制、减少冗余代码，提高样式代码的可维护性。大大的提高了前端在样式上的开发效率。

#### 什么是CSS预处理器

CSS 预处理器定义了一种新的语言，其基本思想是，用一种专门的编程语言，为CSS增加了一些编程的特性，将CSS作为目标生成文件，然后开发者就只要使用这种语言进行CSS的编码工作。转化成通俗易谨的话来说就是**“用一种专门的编程语言，进行Web页面样式设计，再通过编译器转化为正常的CSS 文件，以供项目使用”**。
**常用的CSS预处理器有哪些**

- SASS：基于Ruby，通过服务端处理，功能强大。解析效率高。需要学习Ruby语言，上手难度高于LESS。
- LESS：基于NodeJS，通过客户端处理，使用简单。功能比SASS简单，解析效率也低于SASS，但在实际开发中足够了，所以我们后台人员如果需要的话，建议使用LESS。

### 行为层（JavaScript）

JavaScript**一门弱类型脚本语言，其源代码在发往客户端运行之前不需要经过编译，而是将文本格式的字符代码发送给浏览器，由浏览器解释运行。**

#### Native 原生JS开发

原生JS开发，也就是让我们按照【ECMAScript】标准的开发方式，简称ES，特点是所有浏览器都支持。截至到当前，ES标准以发布如下版本：

- ES3
- ES4（内部，未正式发布）
- ES5（全浏览器支持）
- ES6（常用，当前主流版本：webpack打包成为ES5支持）
- ES7
- ES8
- ES9（草案阶段）

区别就是逐步增加新特性。

#### TypeScript微软的标准

TypeScript是一种由微软开发的自由和开源的编程语言。它是JavaScript的一个超集， 而且本质上向这个语言添加了可选的静态类型和基于类的面向对象编程。由安德斯·海尔斯伯格(C#、Delphi、TypeScript之父； .NET创立者) 主导。该语言的特点就是除了具备ES的特性之外还纳入了许多不在标准范围内的新特性，所以会导致很多浏览器不能直接支持TypeScript语法， 需要编译后(编译成JS) 才能被浏览器正确执行。

### javascript框架

- **JQuery**：大家熟知的JavaScript库，优点就是简化了DOM操作，缺点就是DOM操作太频繁，影响前端性能；在前端眼里使用它仅仅是为了兼容IE6，7，8；
- **Angular**：Google收购的前端框架，由一群Java程序员开发，其特点是将后台的MVC模式搬到了前端并增加了**模块化开发**的理念，与微软合作，采用了TypeScript语法开发；对后台程序员友好，对前端程序员不太友好；最大的缺点是版本迭代不合理（如1代–>2 代，除了名字，基本就是两个东西；截止发表博客时已推出了Angular6）
- **React**：Facebook 出品，一款高性能的JS前端框架；特点是提出了新概念 【**虚拟DOM**】用于减少真实 DOM 操作，在内存中模拟 DOM操作，有效的提升了前端渲染效率；缺点是使用复杂，因为需要额外学习一门【JSX】语言；
- **Vue**：一款渐进式 JavaScript 框架，所谓渐进式就是逐步实现新特性的意思，如实现模块化开发、路由、状态管理等新特性。其特点是综合了 Angular（模块化）和React(虚拟 DOM) 的优点；
- **Axios**：前端通信框架；因为 Vue 的边界很明确，就是为了处理 DOM，所以并不具备通信能力，此时就需要额外使用一个通信框架与服务器交互；当然也可以直接选择使用jQuery 提供的AJAX 通信功能；

## 前端发展史

### UI框架

- Ant-Design：阿里巴巴出品，基于React的UI框架
- ElementUI、iview、ice：饿了么出品，基于Vue的UI框架
- BootStrap： Teitter推出的一个用于前端开发的开源工具包
- AmazeUI：又叫“妹子UI”，一款HTML5跨屏前端框架

### JavaScript构建工具

- Babel： JS编译工具，主要用于浏览器不支持的ES新特性，比如用于编译TypeScript
- WebPack：模块打包器，主要作用就是打包、压缩、合并及按序加载
- 注：以上知识点已将WebApp开发所需技能全部梳理完毕

### 三端同一

#### 混合开发（Hybrid App）

主要目的是实现一套代码三端统一（PC、Android：.apk、iOS：.ipa）并能够调用到设备底层硬件（如：传感器、GPS、摄像头等），打包方式主要有以下两种：

- 云打包：HBuild -> HBuildX，DCloud 出品；API Cloud
- 本地打包： Cordova（前身是 PhoneGap）

#### 微信小程序

详见微信官网，这里就是介绍一个方便微信小程序UI开发的框架：WeUI

### 后端技术

前端人员为了方便开发也需要掌握一定的后端技术但我们Java后台人员知道后台知识体系极其庞大复杂，所以为了方便前端人员开发后台应用，就出现了Node JS这样的技术。Node JS的作者已经声称放弃Node JS(说是架构做的不好再加上笨重的node modules，可能让作者不爽了吧)开始开发全新架构的De no
既然是后台技术，那肯定也需要框架和项目管理工具， Node JS框架及项目管理工具如下：

- Express： Node JS框架
- Koa： Express简化版
- NPM：项目综合管理工具，类似于Maven
- YARN： NPM的替代方案，类似于Maven和Gradle的关系

### 主流前端框架

#### Vue.js

##### iView

iview是一个强大的基于Vue的UI库， 有很多实用的基础组件比element ui的组件更丰富， 主要服务于PC界面的中后台产品。使用单文件的Vue组件化开发模式基于npm+webpack+babel开发， 支持ES 2015高质量、功能丰富友好的API， 自由灵活地使用空间。

- [官网地址](https://www.iviewui.com/)
- [Github](https://github.com/view-design/ViewUI)
- [iview-admin](https://gitee.com/icarusion/iview-admin)

备注：属于前端主流框架，选型时可考虑使用，主要特点是**移动端支持较多**

##### Element UI

Element是饿了么前端开源维护的Vue UI组件库， 组件齐全， 基本涵盖后台所需的所有组件，文档讲解详细， 例子也很丰富。主要用于开发PC端的页面， 是一个质量比较高的Vue UI组件库。

- [官网地址](https://element.eleme.io/#/en-US)
- [Git hub](https://github.com/element-plus/element-plus)
- [vue-element-admin](https://panjiachen.github.io/vue-element-admin-site/zh/guide/)
  备注：属于前端主流框架，选型时可考虑使用，主要特点是**桌面端支持较多**

##### ICE

飞冰是阿里巴巴团队基于React/Angular/Vue的中后台应用解决方案， 在阿里巴巴内部， 已经有270多个来自几乎所有BU的项目在使用。飞冰包含了一条从设计端到开发端的完整链路，帮助用户快速搭建属于自己的中后台应用。

- [官网地址](https://ice.work/)
- [Github](https://github.com/alibaba/ice)

备注：主要组件还是以React为主， 截止2019年02月17日更新博客前**对Vue的支持还不太完善，目前尚处于观望阶段**

##### VantUI

Vant UI是有赞前端团队基于有赞统一的规范实现的Vue组件库， 提供了-整套UI基础组件和业务组件。通过Vant， 可以快速搭建出风格统一的页面，提升开发效率。

- [官网地址](https://youzan.github.io/vant-weapp/#/home)
- [Github](https://github.com/youzan/vant-weapp)

##### AtUI

at-ui是一款基于Vue 2.x的前端UI组件库， 主要用于快速开发PC网站产品。它提供了一套n pm+web pack+babel前端开发工作流程， CSS样式独立， 即使采用不同的框架实现都能保持统一的UI风格。

- [官网地址](https://aliqin.github.io/atui/)
- [Github](https://github.com/aliqin/atui)

##### CubeUl

cube-ui是滴滴团队开发的基于Vue js实现的精致移动端组件库。支持按需引入和后编译， 轻量灵活；扩展性强，可以方便地基于现有组件实现二次开发。

- [官网地址](https://didi.github.io/cube-ui/)
- [Github](https://github.com/didi/cube-ui)

混合开发

##### Flutter

Flutter是谷歌的移动端UI框架， 可在极短的时间内构建Android和iOS上高质量的原生级应用。Flutter可与现有代码一起工作， 它被世界各地的开发者和组织使用， 并且Flutter是免费和开源的。

- [官网地址](https://flutterchina.club/)
- [Github](https://github.com/flutterchina/dio)

备注：Google出品， 主要特点是快速构建原生APP应用程序， 如做混合应用该框架为必选框架

##### lonic

lonic既是一个CSS框架也是一个Javascript UI库， lonic是目前最有潜力的一款HTML 5手机应用开发框架。通过SASS构建应用程序， 它提供了很多UI组件来帮助开发者开发强大的应用。它使用JavaScript MVVM框架和Angular JS/Vue来增强应用。提供数据的双向绑定， 使用它成为Web和移动开发者的共同选择。

- [官网地址](https://ionicframework.com/)
- [官网文档](https://ionicframework.com/docs)
- [Github](https://github.com/ionic-team/ionic-framework)

#### 微信小程序

##### mpvue

mpvue是美团开发的一个使用Vue.js开发小程序的前端框架， 目前支持微信小程序、百度智能小程序，头条小程序和支付宝小程序。框架基于Vue.js， 修改了的运行时框架runtime和代码编译器compiler实现， 使其可运行在小程序环境中， 从而为小程序开发引入了Vue.js开发体验。

- [官网地址](http://mpvue.com/)
- [Github](https://github.com/Meituan-Dianping/mpvue)

备注：完备的Vue开发体验， 井且支持多平台的小程序开发， 推荐使用

##### WeUI

WeUI是一套同微信原生视觉体验一致的基础样式库， 由微信官方设计团队为微信内网页和微信小程序量身设计， 令用户的使用感知更加统一。包含button、cell、dialog、toast、article、icon等各式元素。

- [官网地址](https://weui.io/)
- [Github](https://github.com/Tencent/weui-wxss)

## 了解前后分离的演变史

**为什么需要前后分离**

### 后端为主的MVC时代

为了降低开发的复杂度， 以后端为出发点， 比如：Struts、Spring MVC等框架的使用， 就是后端的MVC时代；
**以SpringMVC流程为例**：

- 发起请求到前端控制器(`Dispatcher Servlet`)
- 前端控制器请求`HandlerMapping`查找`Handler`，可以根据xml配置、注解进行查找
- 处理器映射器`HandlerMapping`向前端控制器返回`Handler`
- 前端控制器调用处理器适配器去执行`Handler`
- 处理器适配器去执行`Handler`
- Handler执行完成给适配器返回`ModelAndView`
- 处理器适配器向前端控制器返回`ModelAndView`，`ModelAndView`是SpringMvc框架的一个底层对象，包括`Model`和`View`
- 前端控制器请求视图解析器去进行视图解析，根据逻辑视图名解析成真正的视图(JSP)
- 视图解析器向前端控制器返回View
- 前端控制器进行视图渲染，视图渲染将模型数据(在`ModelAndView`对象中)填充到request域
- 前端控制器向用户响应结果

**优点**：
MVC是一个非常好的协作模式， 能够有效降低代码的耦合度从架构上能够让开发者明白代码应该写在哪里。为了让`View`更纯粹， 还可以使用`Thyme leaf、Frree marker`等模板引擎， 使模板里无法写入Java代码， 让前后端分工更加清晰。
**缺点**：

- 前端开发重度依赖开发环境，开发效率低，这种架构下，前后端协作有两种模式：
- 第一种是前端写DEMO， 写好后， 让后端去套模板。好处是DEMO可以本地开发， 很高效。不足是还需要后端套模板，有可能套错，套完后还需要前端确定，来回沟通调整的成本比较大；
- 另一种协作模式是前端负责浏览器端的所有开发和服务器端的View层模板开发。好处是UI相关的代码都是前端去写就好，后端不用太关注，不足就是前端开发重度绑定后端环境，环境成为影响前端开发效率的重要因素。
- 前后端职责纠缠不清：模板引擎功能强大，依旧可以通过拿到的上下文变量来实现各种业务逻辑。这样，只要前端弱势一点，往往就会被后端要求在模板层写出不少业务代码，还有一个很大的灰色地带是`Controller`， 页面路由等功能本应该是前端最关注的， 但却是由后端来实现。`Controller`本身与`Model`往往也会纠缠不清，看了让人咬牙的业务代码经常会出现在`Controller`层。这些问题不能全归结于程序员的素养， 否则JSP就够了。
- 对前端发挥的局限性：性能优化如果只在前端做空间非常有限，于是我们经常需要后端合作，但由于后端框架限制，我们很难使用**【Comet】**、**【Big Pipe**】等技术方案来优化性能。

**注：在这期间(2005年以前) ， 包括早期的JSP、PHP可以称之为Web 1.0时代。在这里想说一句， 如果你是一名Java初学者， 请你不要再把一些陈旧的技术当回事了， 比如JSP， 因为时代在变、技术在变、什么都在变(引用扎克伯格的一句话：唯一不变的是变化本身)；当我们去给大学做实训时，有些同学会认为我们没有讲什么干货，其实不然，只能说是你认知里的干货对于市场来说早就过时了而已**

### 基于AJAX带来的SPA时代   

时间回到2005年A OAX(Asynchronous JavaScript And XML， 异步JavaScript和XML，老技术新用法)被正式提出并开始使用CDN作为静态资源存储， 于是出现了JavaScript王者归来(在这之前JS都是用来在网页上贴狗皮膏药广告的) 的SPA(Single Page Application) 单页面应用时代。

#### 优点

这种模式下， **前后端的分工非常清晰， 前后端的关键协作点是AJAX接口。**看起来是如此美妙， 但回过头来看看的话， 这与JSP时代区别不大。复杂度从服务端的JSP里移到了浏览器的JavaScript，浏览器端变得很复杂。类似Spring MVC， 这个时代开始出现浏览器端的分层架构：

#### 缺点

- 前后端接口的约定：如果后端的接口一塌糊涂，如果后端的业务模型不够稳定，那么前端开发会很痛苦；不少团队也有类似尝试，通过接口规则、接口平台等方式来做。有了和后端一起沉淀的接口规则，还可以用来模拟数据，使得前后端可以在约定接口后实现高效并行开发。
- 前端开发的复杂度控制：SPA应用大多以功能交互型为主，JavaScript代码过十万行很正常。大量JS代码的组织，与View层的绑定等，都不是容易的事情。

### 前端为主的MV\*时代

此处的MV*模式如下：

- MVC(同步通信为主) ：Model、View、Controller
- MVP(异步通信为主) ：Model、View、Presenter
- MVVM(异步通信为主)：Model、View、View Model为了降低前端开发复杂度，涌现了大量的前端框架，比如：Angular JS、React、Vue.js、Ember JS等， 这些框架总的原则是先按类型分层， 比如Templates、Controllers、Models， 然后再在层内做切分，如下图：

![image-20211209160846263](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201071257147.png)

#### 优点

- **前后端职责很清晰**：前端工作在浏览器端，后端工作在服务端。清晰的分工，可以让开发并行，测试数据的模拟不难， 前端可以本地开发。后端则可以专注于业务逻辑的处理， 输出RESTful等接口。
- **前端开发的复杂度可控**：前端代码很重，但合理的分层，让前端代码能各司其职。这一块蛮有意思的，简单如模板特性的选择，就有很多很多讲究。并非越强大越好，限制什么，留下哪些自由，代码应该如何组织，所有这一切设计，得花一本书的厚度去说明。
- **部署相对独立**：可以快速改进产品体验

#### 缺点

- 代码不能复用。比如后端依旧需要对数据做各种校验，校验逻辑无法复用浏览器端的代码。如果可以复用，那么后端的数据校验可以相对简单化。
- 全异步， 对SEO不利。往往还需要服务端做同步渲染的降级方案。
- 性能并非最佳，特别是移动互联网环境下。
- SPA不能满足所有需求， 依旧存在大量多页面应用。URL Design需要后端配合， 前端无法完全掌控。

### Node JS带来的全栈时代

前端为主的MV*模式解决了很多很多问题， 但如上所述， 依旧存在不少不足之处。随着Node JS的兴起， JavaScript开始有能力运行在服务端。这意味着可以有一种新的研发模式：

在这种研发模式下，前后端的职责很清晰。对前端来说，两个UI层各司其职：

- Front-end Ul layer处理浏览器层的展现逻辑。通过CSS渲染样式， 通过JavaScript添加交互功能， HTML的生成也可以放在这层， 具体看应用场景。
- Back-end Ul layer处理路由、模板、数据获取、Cookie等。通过路由， 前端终于可以自主把控URL Design， 这样无论是单页面应用还是多页面应用， 前端都可以自由调控。后端也终于可以摆脱对展现的强关注，转而可以专心于业务逻辑层的开发。

通过Node， WebServer层也是JavaScript代码， 这意味着部分代码可前后复用， 需要SEO的场景可以在服务端同步渲染，由于异步请求太多导致的性能问题也可以通过服务端来缓解。前一种模式的不足，通过这种模式几乎都能完美解决掉。

**与JSP模式相比， 全栈模式看起来是一种回归， 也的确是一种向原始开发模式的回归， 不过是一种螺旋上升式的回归。**

基于Node JS的全栈模式， 依旧面临很多挑战：

- 需要前端对服务端编程有更进一步的认识。比如TCP/IP等网络知识的掌握。
- Node JS层与Java层的高效通信。Node JS模式下， 都在服务器端， RESTful HTTP通信未必高效， 通过SOAP等方式通信更高效。一切需要在验证中前行。
- 对部著、运维层面的熟练了解，需要更多知识点和实操经验。
- 大量历史遗留问题如何过渡。这可能是最大最大的阻力。

> **前端想学后台很难，而我们后端程序员学任何东西都很简单**

全栈!So Easy!

### 总结

综上所述，模式也好，技术也罢，没有好坏优劣之分，只有适合不适合；前后分离的开发思想主要是基于**Soc(关注度分离原则)**，上面种种模式，都是让前后端的职责更清晰，分工更合理高效。

---

## 简单的Vue程序

### 什么是MVVM

`MVVM (Model-View-ViewModel) 是一种软件架构设计模式，由微软WPF (用于替代WinForm，以前就是用这个技术开发桌面应用程序的)和Silverlight (类似于Java Applet,简单点说就是在浏览器上运行的WPF)的架构师Ken Cooper和Ted Peters 开发，是一种简化用户界面的事件驱动编程方式。由John Gossman (同样也是WPF和Silverlight的架构师)于2005年在他的博客上发表。`

MVVM 源自于经典的MVC (ModI-View-Controller) 模式。MVVM的核心是ViewModel层，负责转换Model中的数据对象来让数据变得更容易管理和使用，其作用如下:

- 该层向上与视图层进行双向数据绑定
- 向下与Model层通过接口请求进行数据交互

![](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201122329668.png)

### 为什么要使用MVVM

MVVM模式和MVC模式一样，主要目的是分离视图(View)和模型(Model),有几大好处：

- 低耦合：视图(View)可以独立于Model变化和修改,一个ViewModel可以绑定到不同的
- View上，当View变化的时候Model可以不变，当Model变化的时候View也可以不变。
- 可复用：你可以把一些视图逻辑放在一个ViewModel里面，让很多View重用这段视图逻辑。
- 独立开发：开发人员可以专注于业务逻辑和数据的开发(ViewModel),设计人员可以专注于页面设计。
- 可测试：界面素来是比较难于测试的，而现在测试可以针对ViewModel来写。

### Vue 是 MVVM 模式的实现者

![](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201122330540.png)

- Model : 模型层，在这里表示JavaScript对象

- View : 视图层,在这里表示DOM (HTML操作的元素)

- ViewModel : 连接视图和数据的中间件，Vue.js就是MVVM中的ViewModel层的实现者在MVVM架构中，是不允许数据和视图直接通信的，只能通过ViewModel来通信，而ViewModel就是定义了一个Observer观察者

- ViewModel 能够观察到数据的变化，并对视图对应的内容进行更新

- ViewModel 能够监听到视图的变化，并能够通知数据发生改变

### 安装Vue.js

#### CDN

```html
<script src="https://unpkg.com/vue@next"></script>
```

or

```html
<script src="https://cdn.jsdelivr.net/npm/vue@next/dist/vue.global.js"></script>
```

比如：

```html
<script src="https://cdn.jsdelivr.net/npm/vue@3.2.26/dist/vue.global.js"></script>
```

#### npm

```sh
# 最新稳定版
npm install vue@next
```

Vue 还提供了编写[单文件组件](https://v3.cn.vuejs.org/guide/single-file-component.html)的配套工具。如果你想使用单文件组件，那么你还需要安装 `@vue/compiler-sfc`：

```sh
npm install -D @vue/compiler-sfc
```

### 程序实现

#### Hello Vue.js 程序

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <!-- 导入Vue.js -->
    <script src="https://cdn.jsdelivr.net/npm/vue@3.2.26/dist/vue.global.js"></script>

</head>
<body>

    <!-- 用于挂载Vue实例的 -->
    <div id="app"></div>

    <script>

        // 创建一个Vue实例
        Vue.createApp({
            // template是模板的意思，就是在JS里写html代码
            template:"Hello Vue.js"
        }).mount("#app") //这个模板需要放一个位置，也就是说挂载，挂载到`id=app`的DOM上
    </script>
</body>
</html>
```



* `Vue.createApp()` ：创建一个应用，每个 Vue 应用都是通过用 createApp 函数创建一个新的应用实例开始的；
* `const vm = app.mount()` ： vm是获取应用的**根组件**，通过vm可以获取vue里的任何数据，属性和方法；

#### 计数器程序

```html
<body>
    <div id="app" v-once>
        Counter: {{ counter }}
    </div>

    <script>
        const Counter = {
            // 声明这个变量需要在data()函数中
            data() {
                return {
                    counter: 0
                }
            },
            // mounted的是一个声明周期钩子函数，自动执行的方法。
            mounted(){
                setInterval(() => {
                    this.counter += 1   //这个this.counter指向的就是data中的counter
                    //this.$data.counter +=1   //效果相同
                },1000)
            }
        }
        Vue.createApp(Counter).mount("#app")
    </script>
</body>
```

写完这段代码，浏览页面，就可以看到计数器的效果了。现在你回想以前不用框架，原生写法时，是不是要自己编写DOM，而现在完全不用了。

```html
document.getElementById('app').innerHTML()
```

目前需要转变的一个观点，从面向DOM编程，改为**面向数据编程**。

### 防抖和节流

Vue 没有内置支持防抖和节流，但可以使用 [Lodash](https://lodash.com/) 等库来实现。

如果某个组件仅使用一次，可以在 `methods` 中直接应用防抖：

```html
<script src="https://unpkg.com/lodash@4.17.20/lodash.min.js"></script>
<script>
  Vue.createApp({
    methods: {
      // 用 Lodash 的防抖函数
      click: _.debounce(function() {
        // ... 响应点击 ...
      }, 500)
    }
  }).mount('#app')
</script>
```

但是，这种方法对于可复用组件有潜在的问题，因为它们都共享相同的防抖函数。为了使组件实例彼此独立，可以在生命周期钩子的 `created` 里添加该防抖函数:

```js
app.component('save-button', {
    created() {
        // 使用 Lodash 实现防抖
        this.debouncedClick = _.debounce(this.click, 500)
    },
    unmounted() {
        // 移除组件时，取消定时器
        this.debouncedClick.cancel()
    },
    methods: {
        click() {
            // ... 响应点击 ...
        }
    },
    template: `
    <button @click="debouncedClick">
      Save
    </button>
  `
})
```

## Vue模板语法

###  插值：`v-html`、`v-once`、`v-bind`

#### 原始HTML

双大括号会将数据解释为普通文本，而非 HTML 代码。为了输出真正的 HTML，你需要使用`v-html` 指令：

```html
<body>

    <div id="app">
        <p>使用大括号： {{rawHtml}} </p>
        <p>使用v-html： <span v-html="rawHtml"></span> </p>
    </div>

    <span v-on:click="handleItemClick" v-html="message"></span>

    <script>
        Vue.createApp({
            data(){
                return {
                    rawHtml:"<span style='color: yellow'>This is Yellow Font</span>"
                }
            }
        }).mount("#app")
    </script>
</body>
```

![image-20220113012908151](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201130131046.png)

#### 文本

数据绑定最常见的形式就是使用`{{ }}`(双大括号) 语法的文本插值：

```html
<body>
    <div id="app">
        {{ msg }}
    </div>

    <script>
        Vue.createApp({
            // 声明这个变量需要在data()函数中
            data(){
                return {
                    msg:'hello Vue.js'
                }
            },
        }).mount("#app")
    </script>
</body>
```

`{{ }}`标签将会被替代为对应组件实例中 `msg` property 的值。无论何时，绑定的组件实例上 `msg` property 发生了改变，插值处的内容都会更新。

如果不想改变标签的内容，可以通过使用 `v-once` 指令执行一次性地插值，当数据改变时，插值处的内容不会更新。

```html
<body>
    <div id="app"></div>

    <script>
        const app = Vue.createApp({
            data(){
                return {
                    counter:0
                }
            },
            methods: {
                handleItemClick() {
                    this.counter += 1
                }
            },
            template:`<button v-on:click="handleItemClick" >Counter:{{counter}}</button>`
        })

        const vm = app.mount("#app")
    </script>
</body>

```

![image-20220113014347323](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201131841035.png)

点击之后元素会自动增加，但是加入`v-once`后只会渲染一次，只会就不会再次渲染了。

```html
template:`<button v-on:click="handleItemClick" v-once>Counter:{{counter}}</button>`
```

#### Attribute

`{{}}`语法不能在 HTML attribute 中使用，然而，可以使用` v-bind 指令：

```html
<body>
    <div id="app" ></div>

    <script>
        const app = Vue.createApp({
            data(){
              return {
                  idObject:`apple`,
                  classObject:`apple`,
                  styleObject: {
                      color: 'red',
                      fontSize: '13px'
                  }
              }
            },
            template:`<span v-bind:id="idObject" v-bind:class="classObject" v-bind:style="styleObject">Value</span>`
        })

        const  vm = app.mount("#app")
    </script>
</body>
```

`v-bind`指定通过`v-bind:xxx`的形式添加属性，如果对于某一个属性添加多个值，比如`style`，可以如：

```html
`<span v-bind:style="styleObject">Value</span>`
```

```json
styleObject: {
    color: 'red',
    fontSize: '13px'
}
```

直接绑定到一个样式对象通常更好，这会让模板更清晰。如果绑定的值是 `null` 或 `undefined`，那么该 attribute 将不会被包含在渲染的元素上。[更多的样式绑定](https://v3.cn.vuejs.org/guide/class-and-style.html#%E7%BB%91%E5%AE%9A-html-class)。

####  使用 JavaScript 表达式

Vue.js 提供了完全的 JavaScript 表达式支持。

### 参数

一些指令能够接收一个“参数”，在指令名称之后以冒号表示。例如，`v-bind` 指令可以用于响应式地更新 HTML attribute：

```html
<a v-bind:href="url"> ... </a>
```

在这里 `href` 是参数，告知 `v-bind` 指令将该元素的 `href` attribute 与表达式 `url` 的值绑定。

另一个例子是 `v-on` 指令，它用于监听 DOM 事件：

```html
<a v-on:click="doSomething"> ... </a>
```

在这里参数是监听的事件名。

#### 动态参数

也可以在指令参数中使用 **JavaScript 表达式**，方法是用**方括号**括起来：

```html
<!--
注意，参数表达式的写法存在一些约束，如之后的“对动态参数表达式的约束”章节所述。
-->
<a v-bind:[attributeName]="url"> ... </a>
```

这里的 `attributeName` 会被作为一个 JavaScript 表达式进行动态求值，求得的值将会作为最终的参数来使用。例如，如果你的组件实例有一个 data property `attributeName`，其值为 `"href"`，那么这个绑定将等价于 `v-bind:href`。

同样地，你可以使用动态参数为一个动态的事件名绑定处理函数：

```html
<a v-on:[eventName]="doSomething"> ... </a>
```

在这个示例中，当 `eventName` 的值为 `"focus"` 时，`v-on:[eventName]` 将等价于 `v-on:focus`。

#### 修饰符

修饰符 (modifier) 是以半角句号 `.` 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。例如，`.prevent` 修饰符告诉 `v-on` 指令对于触发的事件调用 `event.preventDefault()`：

```html
<form v-on:submit.prevent="onSubmit">...</form>
```

### 缩写

`v-` 前缀作为一种视觉提示，用来识别模板中 Vue 特定的 attribute。当你在使用 Vue.js 为现有标签添加动态行为 (dynamic behavior) 时，v- 前缀很有帮助，然而，对于一些频繁用到的指令来说，就会感到使用繁琐。同时，在构建由 Vue 管理所有模板的单页面应用程序 [(SPA - single page application)](https://en.wikipedia.org/wiki/Single-page_application) 时，`v-` 前缀也变得没那么重要了。因此，Vue 为 `v-bind` 和 `v-on` 这两个最常用的指令，提供了特定简写：

#### `v-bind` 缩写

```html
<!-- 完整语法 -->
<a v-bind:href="url"> ... </a>

<!-- 缩写 -->
<a :href="url"> ... </a>

<!-- 动态参数的缩写 -->
<a :[key]="url"> ... </a>
```

##### `v-on` 缩写

```html
<!-- 完整语法 -->
<a v-on:click="doSomething"> ... </a>

<!-- 缩写 -->
<a @click="doSomething"> ... </a>

<!-- 动态参数的缩写 -->
<a @[event]="doSomething"> ... </a>
```

它们看起来可能与普通的 HTML 略有不同，但 `:` 与 `@` 对于 attribute 名来说都是合法字符，在所有支持 Vue 的浏览器都能被正确地解析。而且，它们不会出现在最终渲染的标记中。缩写语法是完全可选的，但随着你更深入地了解它们的作用，你会庆幸拥有它们。

> 从下一页开始，我们将在示例中使用缩写，因为这是 Vue 开发者最常用的用法。

#### 注意事项

##### 对动态参数值约定

动态参数预期会求出一个字符串，`null` 例外。这个特殊的 `null` 值可以用于显式地移除绑定。任何其它非字符串类型的值都将会触发一个警告。

##### 对动态参数表达式约定对动态参数表达式约定

动态参数表达式有一些语法约束，因为某些字符，如空格和引号，放在 HTML attribute 名里是无效的。例如：

```html
<!-- 这会触发一个编译警告 -->
<a v-bind:['foo' + bar]="value"> ... </a>
```

变通的办法是使用没有空格或引号的表达式，或用**计算属性**替代这种复杂表达式。

在 DOM 中使用模板时 (直接在一个 HTML 文件里撰写模板)，还需要避免使用大写字符来命名键名，因为浏览器会把 attribute 名全部强制转为小写：

```html
<!--
在 DOM 中使用模板时这段代码会被转换为 `v-bind:[someattr]`。
除非在实例中有一个名为“someattr”的 property，否则代码不会工作。
-->
<a v-bind:[someAttr]="value"> ... </a>
```

> 如果有多个单词的话，可以使用下划线

##### JavaScript 表达式

模板表达式都被放在沙盒中，只能访问一个受限的全局变量列表，如 `Math` 和 `Date`。你不应该在模板表达式中试图访问用户定义的全局变量。

## Vue条件语句

### `v-if`

`v-if` 指令用于条件性地渲染一块内容。这块内容只会在指令的表达式返回 truthy 值的时候被渲染。

```html
<body>
    <div id="app" ></div>

    <script>
        const app = Vue.createApp({
            data(){
              return {
                  flag:false
              }
            },
            template:`
              <p v-if="flag">好的</p>
              <p>不好的</p>
            `,
        })

        const vm = app.mount("#app")
    </script>
</body>
```

![image-20220113030921760](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201131841036.png)

通过可以和`v-else`配合使用。

```js
const app = Vue.createApp({
    data(){
        return {
            flag:true
        }
    },
    template:`
    <p v-if="flag">好的</p>
    <p v-else>不好的</p>
`,
})
```

### 在 `<template>` 元素上使用 `v-if` 条件渲染分组

因为 `v-if` 是一个指令，所以必须将它添加到一个元素上。但是如果想切换多个元素呢？此时可以把一个 `<template>` 元素当做不可见的包裹元素，并在上面使用 `v-if`。最终的渲染结果将不包含 `<template>` 元素。

```html
<template v-if="ok">
  <h1>Title</h1>
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
</template>
```

### `v-else`

`v-else` 元素必须紧跟在带 `v-if` 或者 `v-else-if` 的元素的后面，否则它将不会被识别。

### `v-else-if`

`v-else-if`，顾名思义，充当 `v-if` 的“else-if 块”，并且可以连续使用：

```html
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
```

与 `v-else` 的用法类似，`v-else-if` 也必须紧跟在带 `v-if` 或者 `v-else-if` 的元素之后。

### `v-if` 与 `v-for` 一起使用

当 `v-if` 与 `v-for` 一起使用时，`v-if` 具有比 `v-for` 更高的优先级。

> **不推荐**同时使用 `v-if` 和 `v-for`。

### `v-show`

也可以使用 v-show 指令来根据条件展示元素：

```html
<h1 v-show="ok">Hello!</h1>
```

## Vue循环语句

### `v-for` 

#### 数组

可以用 `v-for` 指令基于一个数组来渲染一个列表。`v-for` 指令需要使用 `item in items` 形式的特殊语法，其中 items 是源数据数组，而 `item` 则是被迭代的数组元素的**别名**。

```html
<body>
<div id="app"></div>

<script>
    const app = Vue.createApp({
        data() {
            return {
                items: [{num: 1,}, {num: 2}]
            }
        },
        template: `
          <p v-for="item in items">
          <span>{{ item.num }}</span>
          </p>
        `
    })

    const vm = app.mount("#app")
</script>
</body>
```

![image-20220113031931408](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201131841038.png)

在 `v-for` 块中，可以访问所有父作用域的 property。`v-for` 还支持一个可选的第二个参数，即当前项的索引。

```html
<li v-for="(item, index) in items"></li>
```

#### 对象

也可以用 `v-for` 来遍历一个对象的 property。

```html
<body>
<div id="app"></div>

<script>
    const app = Vue.createApp({
        data() {
            return {
                People: [{name: "小明", age: 18}, {name: "小红", age: 23}]
            }
        },
        template: `
          <p v-for="p in People">
          <span>{{ p.name }}的年龄是{{ p.age }}</span>
          </p>
        `
    })

    const vm = app.mount("#app")
</script>
</body>
```

![image-20220113032550391](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201131841039.png)

也可以用 `of` 替代 `in` 作为分隔符。

### 维护状态

当 Vue 正在更新使用 `v-for` 渲染的元素列表时，它默认使用“就地更新”的策略。如果数据项的顺序被改变，Vue 将不会移动 DOM 元素来匹配数据项的顺序，而是就地更新每个元素，并且确保它们在每个索引位置正确渲染。

这个默认的模式是高效的，但是**只适用于不依赖子组件状态或临时 DOM 状态 (例如：表单输入值) 的列表渲染输出**。

为了给 Vue 一个提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，你需要为每项提供一个唯一的 `key` attribute：

```html
<div v-for="item in items" :key="item.id">
  <!-- 内容 -->
</div>
```

[建议](https://v3.cn.vuejs.org/style-guide/#keyed-v-for-essential)尽可能在使用 `v-for` 时提供 `key` attribute，除非遍历输出的 DOM 内容非常简单，或者是刻意依赖默认行为以获取性能上的提升。

因为它是 Vue 识别节点的一个通用机制，`key` 并不仅与 `v-for` 特别关联。后面我们将在指南中看到，它还具有其它用途。

## 计算属性与侦听器

### 计算属性

#### 基本例子

计算属性的重点突出在`属性`两个字上(属性是名词)，首先它是个`属性`其次这个属性有`计算`的能力(计算是动词)，这里的计算就是个函数;简单点说，它就是一个能够将计算结果缓存起来的属性(将行为转化成了静态的属性)，仅此而已;可以想象为**缓存**！

比如，有时，我们想要显示一个数组经过过滤或排序后的版本，而不实际变更或重置原始数据。在这种情况下，可以创建一个计算属性，来返回过滤或排序后的数组。

```html
<body>
    <div id="app"></div>
    <script>
        const app = Vue.createApp({
            data(){
                return {
                    nums:[1,5,8,9,3,4,7,6,10]
                }
            },
            template:`
              <li v-for="num in nums">{{num}}</li>
            `
        })
    
        const vm = app.mount("#app")
    </script>
</body>
```

![image-20220113165316176](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201131841040.png)

将其进行排序，需要在`computed`方法中设置需要进行的函数，然后可以配`v-for`进行使用，但是需要注意，返回来的数据，需要通过`v-for="item in items":key="item"`才能够使用。

```html
<div id="app"></div>
<script>
    const app = Vue.createApp({
        data(){
            return {
                nums:[1,5,8,9,3,4,7,6,10]
            }
        },
        computed:{
          eventNums:function (){
              return this.nums.sort(function (a,b){
                  return a - b
              })
          }
        },
        template:`
              <li v-for="num in eventNums":key="num">{{num}}</li>
            `
    })

    const vm = app.mount("#app")
</script>
</body>
```

![image-20220113170600788](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201131841041.png)



在计算属性不适用的情况下 (例如，在嵌套的 `v-for` 循环中) 可以使用一个方法`methods`：

```html
<script>
    const app = Vue.createApp({
        data() {
            return {
                sets: [[1, 5, 8, 9, 3, 4, 7, 6, 10], [1, 5, 8, 9, 3, 4, 7, 6, 10]],
            }
        },
        methods: {
            even: function (nums) {
                return nums.sort(function (a, b) {
                    return a - b
                })
            }
        },
        template: `
          <ul v-for="nums in sets">
          	<li v-for="num in even(nums)" :key="num">{{ num }}</li>
          </ul>
        `
    })
    const vm = app.mount("#app")
</script>
```

计算属性`computed`带有缓存效果，能够减少开销。如果不希望有缓存，可以用 `method` 来替代。作一下总结：

* 方法methods：只要页面重新渲染，就会重新执行方法

* 计算属性computed: 当计算属性依赖的内容发生变更时，才会重新执行计算

#### 计算属性的 Setter

计算属性默认只有` getter`，不过在需要时也可以提供一个 `setter`：

```html
<div id="app"></div>
```

```js
const app=Vue.createApp({
    data(){
        return{
            name:'John Bob' ,
        }
    },
    methods:{
        // 1.首先点击触发了事件，将数据进行了改变
        changeName(){
            this.fullName = "hello" + " " + this.name
        }
    },
    computed:{
        // 2. 通过计算属性，将数据原地进行变化
        fullName:{
            // 4.set方法之后就是get方法
            get(){
                console.log("get方法")
                return this.name;
            },
            // 3.只有数据变化的时候，set方法才生效
            set(val){
                console.log("set方法")
                this.name = val.split(' ').join('-')
            }
        }
    },
    template:`
<h2><div @click="changeName()">{{ fullName }}</div> </h2>
`
})
const vm=app.mount("#app")
```

### 监听器/侦听器

虽然计算属性在大多数情况下更合适，但有时也需要一个自定义的侦听器。这就是为什么 Vue 通过 `watch` 选项提供了一个更通用的方法来响应数据的变化。当需要在数据变化时执行异步或开销较大的操作时，这个方式是最有用的。

watch侦听器的作用就是侦听一个data中的值的变化，变化后可以写一个方法，让其进行一些操作（业务逻辑的编写）。

```js
const app=Vue.createApp({
    data(){
        return{
            count:0
        }
    },
    methods:{
        changeCount(){
            return this.count++
        }
    },
    watch:{
        count(){
            console.log("当前count数据变化了,count="+this.count)
        }
    },
    template:`
<h2><div @click="changeCount()">{{ count }}</div> </h2>
`
})
const vm=app.mount("#app")
```

![image-20220113181549330](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201131841042.png)

**侦听器中的方法还可以接收两个参数，一个是现在的值（current），一个是变化之前的值（prev）。**我们分别接收这两个值，并打印在控制台，看一下效果。每当`count`变化的时候，该参数的函数`count`将执行。

```js
watch:{
    count(current,prev){
        console.log("当前count数据变化了")
        console.log('现在的值：',current)
        console.log('变化前的值：',prev)
    }
}
```

### 计算属性 vs 侦听器

Vue 提供了一种更通用的方式来观察和响应当前活动的实例上的数据变动：**侦听属性**。当你有一些数据需要随着其它数据变动而变动时，`watch` 很容易被滥用——特别是如果你之前使用过 AngularJS。然而，通常更好的做法是使用**计算属性**而不是命令式的 `watch` 回调。

比如：做一个加法的，有a，b两个参数，每当a和b中有变化，结果只需要使用计算属性进行处理就可以了。

## 数据双向绑定

### 概念

#### 什么是双向绑定

` Vue.js`是一个MVVM框架，即数据双向绑定,即当数据发生变化的时候,视图也就发生变化，当视图发生变化的时候，数据也会跟着同步变化。这也算是`Vue.js`的精髓之处了。

 值得注意的是，我们所说的数据双向绑定，一定是对于UI控件来说的，非UI控件不会涉及到数据双向绑定。单向数据绑定是使用状态管理工具的前提。如果我们使用`vuex`，那么数据流也是单项的，这时就会和双向数据绑定有冲突。
#### 为什么要实现数据的双向绑定

在`Vue.js` 中，如果使用`vuex` ，实际上数据还是单向的，之所以说是数据双向绑定，这是用的UI控件来说，对于我们处理表单，Vue.js的双向数据绑定用起来就特别舒服了。==即两者并不互斥，在全局性数据流使用单项,方便跟踪;局部性数据流使用双向，简单易操作。==

#### 在表单中使用双向数据绑定

你可以用`v-model`指令在表单 `<input>`、`<textarea>` 及`<select>` 元素上创建双向数据绑定。它会根据控件类型自动选取正确的方法来更新元素。尽管有些神奇，但`v-model`本质上不过是语法糖。它负责监听户的输入事件以更新数据，并对一些极端场景进行一些特殊处理。

 **注意：v-model会忽略所有元素的value、checked、selected特性的初始值而总是将Vue实例的数据作为数据来源，你应该通过JavaScript在组件的data选项中声明。**

`v-model` 在内部为不同的输入元素使用不同的 property 并抛出不同的事件：

- **text 和 textarea 元素使用 `value` property 和 `input` 事件；**
- **checkbox 和 radio 使用 `checked` property 和 `change` 事件；**
- **select 字段将 `value` 作为 prop 并将 `change` 作为事件。**

### 基础用法

#### 文本

```html
<body>
    <div id="app">
        <input type="text" v-model:value="msg" placeholder="edit me">
        <p>message:{{ msg }}</p>
    </div>
    <script>
        const app = Vue.createApp({
            data(){
                return { msg:"hello" }
            }
        })

        const vm = app.mount("#app")
    </script>
</body>
```



![image-20220113184127376](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201131841043.png)

#### 多行文本

```html
<textarea v-model="msg" placeholder="edit me"></textarea>
```

![image-20220113184706228](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201140215248.png)

插值在 textarea 中不起作用，请使用 `v-model` 来代替。

#### 复选框

* 单个复选框，绑定到布尔值

```html
<body>
    <div id="app">
       <input type="checkbox" id="checkbox" v-model:checked="flag">
    </div>
    <script>
        const app = Vue.createApp({
            data(){
                return { flag:true}
            }
        })
        const vm = app.mount("#app")
    </script>
</body>
```

![image-20220113185036804](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201140215250.png)

* 多个复选框，绑定到同一个数组

```html
<body>
    <div id="app">
        <div v-for="book in books">
            <input type="checkbox" v-bind:id="book" v-bind:value="book"  v-model="checkBook">
            <label v-bind:for="book">{{ book }}</label>
        </div>
        <span>checkd Books: {{ checkBook }}</span>
    </div>
    <script>
        const app = Vue.createApp({
            data() {
                return {
                    books: ["java", "c++", "python"],
                    checkBook:[]
                }
            }
        })
        const vm = app.mount("#app")
    </script>
</body>
```

其中`v-model`用于双向绑定对的，注意在data属性中，checkBook值为列表用于添加多个数据的。

#### 单选框

```html
<body>
    <div id="app">
       <div v-for="book in books">
           <input type="radio" v-bind:id="book" v-bind:value="book" v-model="checkBook">
           <label v-bind:for="book">{{book}}</label>
       </div>
        <span>Picked: {{ checkBook }}</span>
    </div>
    <script>
        const app = Vue.createApp({
            data() {
                return {
                    books: ["java", "c++", "python"],
                    checkBook:''
                }
            }
        })
        const vm = app.mount("#app")
    </script>
</body>
```

![image-20220113191020220](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201140215251.png)

#### 选择框

```html
<body>
    <div id="app">
        <select v-model="selected" >
            <option disabled value="">Please select one</option>
            <option v-for="(book,index) in books">{{book}}</option>
        </select>
        <span>Picked: {{ selected }}</span>
    </div>
    <script>
        const app = Vue.createApp({
            data() {
                return {
                    books: ["java", "c++", "python"],
                    selected: ''
                }
            }
        })
        const vm = app.mount("#app")
    </script>
</body>
```

注意，在选择框中使用`v-for`的时候需要在`option`里面进行使用，不然会导致出现多个选择框。

多选时 (绑定到一个数组)：

```html
<div id="app">
    <select v-model="selected" multiple>
        <option disabled value="">Please select one</option>
        <option v-for="(book,index) in books">{{book}}</option>
    </select>
    <span>Picked: {{ selected }}</span>
</div>
```

> 可以和`v-bind:value=""`配合使用。

### 修饰符

#### `.lazy`

在默认情况下，`v-model` 在每次 `input` 事件触发后将输入框的值与数据进行同步 (除了[上述](https://v3.cn.vuejs.org/guide/forms.html#vmodel-ime-tip)输入法组织文字时)。你可以添加 `lazy` 修饰符，从而转为在 `change` 事件之后进行同步：

```html
<input type="text" v-model.lazy="msg" placeholder="edit me">
```

#### `.number`

如果想自动将用户的输入值转为数值类型，可以给 `v-model` 添加 `number` 修饰符：

```html
<input v-model.number="age" type="text" />
```

当输入类型为 `text` 时这通常很有用。如果输入类型是 `number`，Vue 能够自动将原始字符串转换为数字，无需为 `v-model` 添加 `.number` 修饰符。如果这个值无法被 `parseFloat()` 解析，则返回原始的值。

#### `.trim`

如果要自动过滤用户输入的首尾空白字符，可以给 `v-model` 添加 `trim` 修饰符：

```html
<input v-model.trim="msg" />
```

## Vue组件讲解

### 组件基础

#### 概念

组件是可复用的`Vue`实例，说白了就是一组可以重复使用的模板，跟JSTL的自定义标签、Thymeleaf的`th:fragment` 等框架有着异曲同工之妙。通常一个应用会以一棵嵌套的组件树的形式来组织：

![](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201131940247.png)



#### 如何编写一个组件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
    <script src="https://cdn.jsdelivr.net/npm/vue@3.2.26/dist/vue.global.js"></script>
</head>
<body>
    <div id="app"></div>
    <script>
        const app = Vue.createApp({
            data() {return {}}
        })
        const vm = app.mount("#app")
    </script>
</body>
</html>
```

有了`app`变量，可以非常方便的自定义组件并使用了。比如现在写一个关于标题的组件，其中`myTitle`就是该组件的名称，方便调用。

```js
app.component(`myTitle`,{
    template:`<h1 style="color: yellow">我是标题</h1>`
})
```

有了这个组件，就可以在`app`的模板部分使用了，比如放在`template`的最上面，代码如下：

```js
const app = Vue.createApp({
    data() {return {}},
    template: `
    <div>
    	<myTitle/>
    </div>
`
})
app.component(`myTitle`,{
    template:`<h1 style="color: red">我是标题</h1>`
})
```

![image-20220113194716735](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201140215252.png)

#### 动态组件

 动态组件有一个关键的指令是`v-bind`,用这种方法，组件可以通过`props`取得对应的值。

首选编写一个组件，通过`props`定义参数名称，比如` props:['item','index']`，其中`item`以及`index`都是参数。

```js
app.component(`myTitle`,{
    props:['item','index'],
    template:`
<li style="color: red">{{index}}--{{item}}</li>
`
})
```

`props`是一个数组，可以接受多个值。有了`myTitle`组件后，就可以在`app`的`template`中使用了，方法如下。

```js
const app = Vue.createApp({
    data() {return {
        books:["Java","Python","C++"]
    }},
    template: `
    <div>
        <myTitle v-for="(item,index) in books"
        v-bind:item="item"
        v-bind:index="index"/>
    </div>
`
})
```

其中，`v-bind:参数名称="参数值"`就是用来传递给组件的，与组件中的`props`对应。

有的时候，在不同组件之间进行动态切换是非常有用的，比如在一个多标签的界面里：

```html
<body>
    <div id="app">
        <button v-for="tab in tabs":key="tab"
                v-bind:key="tab"
                v-on:click="currentTab = tab">
            {{tab}}
        </button>
		
        <!-- 想要更改组件，需要使用component，然后通过v-bind:is="currentTabComponent"进行修改-->
        <component v-bind:is="currentTabComponent" class="tab"></component>
    </div>
    <script>
        const app = Vue.createApp({
            data() {return {
                currentTab: 'Home',
                tabs: ['Home', 'Posts', 'Archive']
            }},
            // 跳转改变组件的
            computed:{
                currentTabComponent(){
                    return `tab-` + this.currentTab.toLowerCase()
                }
            }
        })
        
        // 组件
        app.component('tab-home', {
            template: `<div class="demo-tab">Home component</div>`
        })
        app.component('tab-posts', {
            template: `<div class="demo-tab">Posts component</div>`
        })
        app.component('tab-archive', {
            template: `<div class="demo-tab">Archive component</div>`
        })

        const vm = app.mount("#app")

    </script>
</body>
```

可以通过`$emit`方法将子组件传递给父组件。

### 通过插槽slot分发内容

> 详解：https://github.com/cunzaizhuyi/vue-slot-demo

插槽，顾名思义，就是在组件容器中添加一个一个的插槽。哈哈，就是这么生硬的解释。来张图，缓解一下~

![img](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201132142357.png)

先定义`vue`组件，

`Article.vue`

```vue
<template>
  <div>
    <h1>我是文章标题</h1>
  </div>
</template>


<script>
export default {
  name: "Article"
}
</script>

<style scoped>

</style>
```

`App.vue`

```vue
<template>
  <Article>
    {{ content }}
  </Article>
</template>

<script>
// 导入组件
import Article from "@/components/Article";

export default {
  name: 'App', //组件名称
  components: { // 添加组件
      Article
  },
  data(){ // 当前组件可以设置的数据
    return {
      content:"默认数据"
    }
  }
}
</script>
```

![image-20220114002726749](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201140215253.png)

==很明显，如果在一个组件内部写内容，其实并不会被显示==，该组件起始标签和结束标签之间的任何内容都会被抛弃，所以这就引入了插槽的功能，提前预定好位置，让父组件往里面填充内容。

所以把上面的article.vue稍微修改一下，加个插槽：

```vue
<template>
  <div>
    <h1>我是文章标题</h1>
    <div><slot>Article默认数据</slot></div>
  </div>
</template>
```

再看看结果，内容就显示出来了，而且会把默认内容给覆盖掉。这里如果你不填写内容，默认内容就会显示出来。

![image-20220114003055059](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201140215254.png)



在向具名插槽提供内容的时候，可以在一个 template元素上使用 v-slot 指令，并以v-slot 的参数的形式提供其名称。示例如下：

`App.vue`

```vue
<template>
  <Article>
    <template v-slot:content>
      {{ content }}
    </template>
    <template #footer>
      {{ footer }}
    </template>
  </Article>
</template>

<script>

import Article from "@/components/Article";

export default {
  name: 'App',
  components: {
      Article
  },
  data(){
    return {
      content:"内容默认数据",
      footer:"尾部默认数据",
    }
  }
}
</script>
```

`Article.vue`

```vue
<template>
  <div>
    <h1>我是文章标题</h1>
    <div><slot name="content">content</slot></div>
    <div><slot name="footer">footer</slot></div>
  </div>
</template>


<script>
export default {
  name: "Article"
}
</script>

<style scoped>

</style>
```

![image-20220114003525268](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201140215255.png)

## 生命周期钩子

![https://newimg.jspang.com/Vuelifecycle.png](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201140042079.png)

| 选项式 API        | 钩内 `setup`        | 含义                                                       |
| ----------------- | ------------------- | ---------------------------------------------------------- |
| `beforeCreate`    | 不需要*             | 在实例生成之前会自动执行的函数                             |
| `created`         | 不需要*             | 在实例生成之后会自动执行的函数                             |
| `beforeMount`     | `onBeforeMount`     | 在模板渲染完成之前执行的函数                               |
| `mounted`         | `onMounted`         | 在模板渲染完成之后执行的函数                               |
| `beforeUpdate`    | `onBeforeUpdate`    | 当data中的数据变化时， 会立即自动执行的函数                |
| `updated`         | `onUpdated`         | 当data中的数据发生变化，页面重新渲染完后，会自动执行的函数 |
| `beforeUnmount`   | `onBeforeUnmount`   | 当Vue应用失效时，会自动执行的函数                          |
| `unmounted`       | `onUnmounted`       | 当Vue应用失效时，且DOM完全销毁之后，会自动执行             |
| `errorCaptured`   | `onErrorCaptured`   |                                                            |
| `renderTracked`   | `onRenderTracked`   |                                                            |
| `renderTriggered` | `onRenderTriggered` |                                                            |
| `activated`       | `onActivated`       |                                                            |
| `deactivated`     | `onDeactivated`     |                                                            |

Vue3中有八个生命周期函数，这些生命周期虽然多，可以成对的去记忆，这样就有四个关键节点了：创建、渲染、更新、销毁。最主要的理解是他们是自动执行的函数。

## 绑定事件

### 方法和参数

现在有一个按钮需要，初始值为0，按下一次，就增加一个计数单位。

```html
<body>
    <div id="app">
        <button v-on:click="countClick">{{count}}</button>
    </div>
    <script>
        const app = Vue.createApp({
            data(){ return {count:0}},
            methods:{
                countClick(){
                    this.count++
                }
            }
        })
        const vm = app.mount("#app")
    </script>
```

`v-on:click="countClick"`可以触发点击事件，`countClick`为自定义的触发事件后执行方法。

如果想要传递参数，则需要在执行方法中添加括号，以及传递的参数，比如：

```
<button v-on:click="countClick(2)">{{count}}</button>
```

在编写响应事件事，是可以接受一个event参数的，这个参数就是关于响应事件的一些内容。但是需要注意，如果没有传递参数，可以直接在函数中传递event。如下：

```html
<body>
    <div id="app">
        <button v-on:click="countClick">{{count}}</button>
    </div>
    <script>
        const app = Vue.createApp({
            data(){ return {count:0}},
            methods:{
                countClick(event){
                    console.log(event)
                    this.count++
                }
            }
        })
        const vm = app.mount("#app")
    </script>
</body>
```

如果有参数设置的话，则需要通过和参数一起传递，而且event参数需要以`$event`进行传递：

```html
<body>
<div id="app">
    <button v-on:click="countClick(2,$event)">{{count}}</button>
</div>
<script>
    const app = Vue.createApp({
        data(){ return {count:0}},
        methods:{
            countClick(num,event){
                console.log(event)
                this.count++
            }
        }
    })
    const vm = app.mount("#app")
</script>
</body>
```

如果有想要调用多个方法，可以如下设置：

```html
<button @click="handleBtnClick1(),handleBtnClick2()">aaaa</button>
```

### 修饰符

#### 事件修饰符

`Vue.js` 为 v-on 提供了事件修饰符来处理 DOM 事件细节，如：`event.preventDefault()` 或 `event.stopPropagation()`。

`Vue.js` 通过由点 **.** 表示的指令后缀来调用修饰符。

* `.stop` - 阻止冒泡
* `.prevent` - 阻止默认事件
* `.capture` - 阻止捕获
* `.self` - 只监听触发该元素的事件
* `.once` - 只触发一次
* `.left` - 左键事件
* `.right` - 右键事件
* `.middle` - 中间滚轮事件

#### 按键修饰符

Vue 允许为 v-on 在监听键盘事件时添加按键修饰符：

```html
<!-- 只有在 keyCode 是 13 时调用 vm.submit() -->
<input v-on:keyup.13="submit">
```

全部的按键别名：

- `.enter`
- `.tab`
- `.delete` (捕获 "删除" 和 "退格" 键)
- `.esc`
- `.space`
- `.up`
- `.down`
- `.left`
- `.right`

系统修饰键：

- `.ctrl`
- `.alt`
- `.shift`
- `.meta`

鼠标按钮修饰符:

- `.left`
- `.right`
- `.middle`

#### .exact 修饰符

**.exact** 修饰符允许你控制由精确的系统修饰符组合触发的事件。

```html
<!-- 即使 Alt 或 Shift 被一同按下时也会触发 -->
<button @click.ctrl="onClick">A</button>

<!-- 有且只有 Ctrl 被按下的时候才触发 -->
<button @click.ctrl.exact="onCtrlClick">A</button>

<!-- 没有任何系统修饰符被按下的时候才触发 -->
<button @click.exact="onClick">A</button>
```

## Axios异步通信

### 安装

#### CDN

```html
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

or

```html
<script src="https://unpkg.com/axios@0.24.0/dist/axios.min.js"></script>
```

or

```html
<script src="https://cdn.bootcdn.net/ajax/libs/axios/0.24.0/axios.js"></script>
```

#### NPM

```sh
npm install axios -g
```

### 文档

* [axios中文文档](http://axios-js.com/zh-cn/docs/index.html)

### 使用方法

```js
Vue.axios.get(api).then((response) => {
  console.log(response.data)
})

this.axios.get(api).then((response) => {
  console.log(response.data)
})

this.$http.get(api).then((response) => {
  console.log(response.data)
})
```

**模拟Json数据：**

```json
{
  "name": "weg",
  "age": "18",
  "sex": "男",
  "url":"https://www.baidu.com",
  "address": {
    "street": "文苑路",
    "city": "南京",
    "country": "中国"
  },
  "links": [
    {
      "name": "bilibili",
      "url": "https://www.bilibili.com"
    },
    {
      "name": "baidu",
      "url": "https://www.baidu.com"
    },
    {
      "name": "cqh video",
      "url": "https://www.4399.com"
    }
  ]
}
```

### GET方法

```html
<body>
<div id="app">
    {{info}}
</div>
<script>
    const app = Vue.createApp({
        data(){
            return {
                info:"Ajax 测试"
            }
        },
        mounted(){
            axios.get("data.json")
            .then(response => (this.info = response))
            .catch(function (error){ // 请求失败处理
                console.log(error)
            })
        }
    })
    const vm = app.mount("#app")
</script>
</body>
```

可以通过 params 设置参数：

```js
axios.get("data.json",{
    params: {
        id:123
    }
})
```

### 执行多个并发请求

```js
function getUserAccount() {
  return axios.get('/user/12345');
}
 
function getUserPermissions() {
  return axios.get('/user/12345/permissions');
}
axios.all([getUserAccount(), getUserPermissions()])
  .then(axios.spread(function (acct, perms) {
    // 两个请求现在都执行完成
  }));
```

### axios API

```js
//  GET 请求远程图片
axios({
  method:'get',
  url:'http://bit.ly/2mTM3nY',
  responseType:'stream'
})
  .then(function(response) {
  response.data.pipe(fs.createWriteStream('ada_lovelace.jpg'))
});
```

## Vue-cli工具

### 安装

```sh
npm install -g @vue/cli

npm install -g @vue/cli-service-global
```

### 创建项目

```sh
vue create hello-world
```

###  使用图形化界面

```sh
vue ui
```

### 命令

```sh
# 初始化
npm install

# 运行
npm run dev
```

## webpack学习使用

### 安装并测试

```sh
npm install webpack-dev-server -g
npm install webpack -g
npm install webpack-cli -g
 
webpack -v
webpack-cli -v
```

### 使用webpack

* 创建项目

![image-20220114015658149](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201140215256.png)

* 创建一个名为modules的目录，用于放置JS模块等资源文件

![image-20220114015826855](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201140215257.png)

* 在modules下创建模块文件，如hello.js，用于编写JS模块相关代码

![image-20220114020323203](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201140215258.png)

`hello.js`

```js
// 使用export暴露一个方法sayHi

exports.sayHi = function(){
    document.write("<div>Hello Webpack</div>");
}
```

`main.js`：在modules下创建一个名为main.js的入口文件，用于打包时设置entry属性

```js
//require 导入一个模块，就可以调用这个模块中的方法了
var hello = require("./hello");
hello.sayHi();
```

* 在项目目录下创建webpack.config.js配置文件，使用webpack命令打包

![image-20220114020652387](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201140215259.png)

```js
module.exports ={
    entry:"./modules/main.js", // 程序入口
    output:{
        filename:"./js/bundle.js" // 打包输出地址
    }
};
```

* 在当前目录下，打开cmd，输入webpack进行打包

![image-20220114021222023](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201140215260.png)

![image-20220114021135885](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201140215261.png)

* 在项目目录下创建HTML页面，如index.html，导入webpack打包后的JS文件

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Java</title>
</head>
<body>
<script src="dist/js/bundle.js"></script>
</body>
</html>
```

![image-20220114021324244](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201140215262.png)

```
# 参数--watch 用于监听变化
webpack --watch
```

## Vue-router路由

### 说明

 Vue Router是Vue.js官方的路由管理器（路径跳转）。它和Vue.js的核心深度集成，让构建单页面应用变得易如反掌。包含的功能有:

- 嵌套的路由/视图表

- 模块化的、基于组件的路由配置

- 路由参数、查询、通配符

- 基于Vue.js过渡系统的视图过渡效果

- 细粒度的导航控制

- 带有自动激活的CSS class的链接

- HTML5历史模式或hash模式，在IE9中自动降级

- 自定义的滚动条行为

### 安装

#### NPM

```csharp
npm install vue-router@4
```

#### CDN

```sh
https://unpkg.com/vue-router@4
```

### 简单实例

`Vue.js + vue-router` 可以很简单的实现单页应用。

`<router-link>` 是一个组件，该组件用于设置一个导航链接，切换不同 HTML 内容。 **to** 属性为目标地址， 即要显示的内容。

以下实例中我们将 vue-router 加进来，然后配置组件和路由映射，再告诉 vue-router 在哪里渲染它们。代码如下所示：

* `App.vue`

```html
<template>
  <h1>{{title}}</h1>
  <p>
    <!--使用 router-link 组件进行导航 -->
    <!--通过传递 `to` 来指定链接 -->
    <!--`<router-link>` 将呈现一个带有正确 `href` 属性的 `<a>` 标签-->
    <router-link to="/">首页</router-link>
    |
    <router-link to="/about">关于</router-link>
    <!-- 路由出口 -->
    <!-- 路由匹配到的组件将渲染在这里 -->
    <router-view></router-view>
  </p>
</template>
```

* `Home.vue`

```vue
<template>
  <h1>我是首页</h1>
</template>
```

* `About.vue`

```vue
<template>
  <h1>我是关于页面</h1>
</template>
```

但是现在还切换不了，需要配置路由。

* 创建router.js

```js
import { createRouter } from "vue-router"

const router = createRouter({

});

export default router;
```

* 在main.js接口中引入router，就可以使用路由了

```js
// 引入模块
import router from "../router";

const app = createApp(App)
// 使用路由
app.use(router)
app.mount('#app')
```

为了实现跳转，在router.js中进行添加路由

```js
import { createRouter,createWebHashHistory } from "vue-router"
import Home from "@/components/Home";
import About from "@/components/About";

const router = createRouter({
    //  内部提供了 history 模式的实现。为了简单起见，在这里使用 hash 模式。
    history:createWebHashHistory(),
    // 配置路由
    routes:[
        {
            path:"/",           //跳转路径
            component:Home      //需要跳转的组件
        },
        {
            path:'/about',
            component:About
        }
    ]
});

export default router;
```

### router-link

请注意，我们没有使用常规的 a 标签，而是使用一个自定义组件 router-link 来创建链接。这使得 Vue Router 可以在不重新加载页面的情况下更改 URL，处理 URL 的生成以及编码。

#### to属性

```vue
// to是指定跳转的链接
<router-link to="/about">关于</router-link>

<!-- 带查询参数，下面的结果为 /register?plan=private -->
<router-link :to="{ path: 'register', query: { plan: 'private' }}">Register</router-link>
```

#### replace属性

设置 replace 属性的话，当点击时，会调用 router.replace() 而不是 router.push()，导航后不会留下 history 记录。

```vue
<router-link :to="{ path: '/abc'}" replace></router-link>
```

#### append属性

设置 append 属性后，则在当前 (相对) 路径前添加其路径。例如，我们从 /a 导航到一个相对路径 b，如果没有配置 append，则路径为 /b，如果配了，则为 /a/b

```vue
<router-link :to="{ path: 'relative/path'}" append></router-link>
```

#### tag属性

有时候想要 `<router-link>` 渲染成某种标签，例如 `<li>`。 于是我们使用 `tag` prop 类指定何种标签，同样它还是会监听点击，触发导航。

```vue
<router-link to="/foo" tag="li">foo</router-link>
<!-- 渲染结果 -->
<li>foo</li>
```

#### active-class属性

设置 链接激活时使用的 CSS 类名。可以通过以下代码来替代。

```vue
<style>
   ._active{
      background-color : red;
   }
</style>
<p>
   <router-link v-bind:to = "{ path: '/route1'}" active-class = "_active">Router Link 1</router-link>
   <router-link v-bind:to = "{ path: '/route2'}" tag = "span">Router Link 2</router-link>
</p>
```

注意这里 **class** 使用 **active-class="_active"**。

#### exact-active-class属性

配置当链接被精确匹配的时候应该激活的 class。可以通过以下代码来替代。

```vue
<p>
   <router-link v-bind:to = "{ path: '/route1'}" exact-active-class = "_active">Router Link 1</router-link>
   <router-link v-bind:to = "{ path: '/route2'}" tag = "span">Router Link 2</router-link>
</p>
```

#### event属性

声明可以用来触发导航的事件。可以是一个字符串或是一个包含字符串的数组。

```vue
<router-link v-bind:to = "{ path: '/route1'}" event = "mouseover">Router Link 1</router-link>
```

以上代码设置了 event 为 mouseover ，及在鼠标移动到 Router Link 1 上时导航的 HTML 内容会发生改变。

### router-view

router-view **将显示与 url 对应的组件**。可以把它放在任何地方，以适应你的布局。

```vue
<router-view></router-view>
```

### 命名路由

除了 `path` 之外，你还可以为任何路由提供 `name`。这有以下优点：

- 没有硬编码的 URL
- `params` 的自动编码/解码。
- 防止你在 url 中出现打字错误。
- 绕过路径排序（如显示一个）

```vue
const routes = [
  {
    path: '/user/:username',
    name: 'user',
    component: User
  }
]
```

要链接到一个命名的路由，可以向 `router-link` 组件的 `to` 属性传递一个对象：

```vue
<router-link :to="{ name: 'user', params: { username: 'erina' }}">
  User
</router-link>
```

这跟代码调用 `router.push()` 是一回事：

```vue
router.push({ name: 'user', params: { username: 'erina' } })
```

在这两种情况下，路由将导航到路径 `/user/erina`。

### 命名视图

有时候想同时 (同级) 展示多个视图，而不是嵌套展示，例如创建一个布局，有 `sidebar` (侧导航) 和 `main` (主内容) 两个视图，这个时候命名视图就派上用场了。你可以在界面中拥有多个单独命名的视图，而不是只有一个单独的出口。如果 `router-view` 没有设置名字，那么默认为 `default`。

```vue
<router-view class="view left-sidebar" name="LeftSidebar"></router-view>
<router-view class="view main-content"></router-view>
<router-view class="view right-sidebar" name="RightSidebar"></router-view>
```

一个视图使用一个组件渲染，因此对于同个路由，多个视图就需要多个组件。确保正确使用 `components` 配置 (带上 **s**)：

```vue
const router = createRouter({
  history: createWebHashHistory(),
  routes: [
    {
      path: '/',
      components: {
        default: Home,
        // LeftSidebar: LeftSidebar 的缩写
        LeftSidebar,
        // 它们与 `<router-view>` 上的 `name` 属性匹配
        RightSidebar,
      },
    },
  ],
})
```

### 嵌套命名视图

我们也有可能使用命名视图创建嵌套视图的复杂布局。这时你也需要命名用到的嵌套 `router-view` 组件。我们以一个设置面板为例：

```sh
/settings/emails                                       /settings/profile
+-----------------------------------+                  +------------------------------+
| UserSettings                      |                  | UserSettings                 |
| +-----+-------------------------+ |                  | +-----+--------------------+ |
| | Nav | UserEmailsSubscriptions | |  +------------>  | | Nav | UserProfile        | |
| |     +-------------------------+ |                  | |     +--------------------+ |
| |     |                         | |                  | |     | UserProfilePreview | |
| +-----+-------------------------+ |                  | +-----+--------------------+ |
+-----------------------------------+                  +------------------------------+
```

- `Nav` 只是一个常规组件。
- `UserSettings` 是一个视图组件。
- `UserEmailsSubscriptions`、`UserProfile`、`UserProfilePreview` 是嵌套的视图组件。

**注意**：*我们先忘记 HTML/CSS 具体的布局的样子，只专注在用到的组件上。*

`UserSettings` 组件的 `<template>` 部分应该是类似下面的这段代码:

```vue
<!-- UserSettings.vue -->
<div>
  <h1>User Settings</h1>
  <NavBar />
  <router-view />
  <router-view name="helper" />
</div>
```

那么就可以通过这个路由配置来实现上面的布局：

```vue
{
  path: '/settings',
  // 你也可以在顶级路由就配置命名视图
  component: UserSettings,
  children: [{
    path: 'emails',
    component: UserEmailsSubscriptions
  }, {
    path: 'profile',
    components: {
      default: UserProfile,
      helper: UserProfilePreview
    }
  }]
}
```

### 重定向和别名

#### 重定向

重定向也是通过 `routes` 配置来完成，下面例子是从 `/a` 重定向到 `/b`：

```js
const router = new VueRouter({
  routes: [
    { path: '/a', redirect: '/b' }
  ]
})
```

重定向的目标也可以是一个命名的路由：

```js
const router = new VueRouter({
  routes: [
    { path: '/a', redirect: { name: 'foo' }}
  ]
})
```

甚至是一个方法，动态返回重定向目标：

```js
const router = new VueRouter({
  routes: [
    { path: '/a', redirect: to => {
      // 方法接收 目标路由 作为参数
      // return 重定向的 字符串路径/路径对象
    }}
  ]
})
```

注意[导航守卫](https://router.vuejs.org/zh/guide/advanced/navigation-guards.html)并没有应用在跳转路由上，而仅仅应用在其目标上。在下面这个例子中，为 `/a` 路由添加一个 `beforeEnter` 守卫并不会有任何效果。

其它高级用法，请参考[例子 (opens new window)](https://github.com/vuejs/vue-router/blob/dev/examples/redirect/app.js)。

#### 别名

“重定向”的意思是，当用户访问 `/a`时，URL 将会被替换成 `/b`，然后匹配路由为 `/b`，那么“别名”又是什么呢？

**`/a` 的别名是 `/b`，意味着，当用户访问 `/b` 时，URL 会保持为 `/b`，但是路由匹配则为 `/a`，就像用户访问 `/a` 一样。**

上面对应的路由配置为：

```js
const router = new VueRouter({
  routes: [
    { path: '/a', component: A, alias: '/b' }
  ]
})
```

“别名”的功能让你可以自由地将 UI 结构映射到任意的 URL，而不是受限于配置的嵌套路由结构。

更多参考：https://router.vuejs.org/zh/installation.html

## Vue项目

### 初始化

在项目文件夹里执行，初始化vue项目

```shell
vue init webpack vue-demo
```

运行，访问8080端口

```sh
npm run dev
```

初始化vue项目：vue init webpack appTestName项目名

直接在IDEA的项目下（不用创建文件夹）执行

```shell
vue init webpack vue-demo
```

报错的话添加vue的环境变量：

```shell
npm config get prefix # 找到npm
```

添加环境变量 

```shell
C:\Users\xxx\AppData\Roaming\npm\node_modules@vue\cli-init\node_modules.bin
```

一个劲回车，ESlint及后面的都选择no。`npm run dev `运行，访问8080端口。

### vue项目目录结构

| 目录/文件      | 说明                                                         |
| -------------- | ------------------------------------------------------------ |
| build          | 项目构建(webpack)相关代码                                    |
| `config`       | 配置目录，包括端口号等。我们初学可以使用默认的。             |
| `node_modules` | npm 加载的项目依赖模块                                       |
| src            | 这里是我们要开发的目录，基本上要做的事情都在这个目录里。里面包含了几个目录及文件：<br/>- assets: 放置一些图片，如logo等。<br/>- components: 目录里面放了一个组件文件，可以不用。<br/>- App.vue: 项目入口文件，我们也可以直接将组件写这里，而不使用 components 目录。<br/>- main.js: 项目的核心文件。<br/> |
| static         | 静态资源目录，如图片、字体等。                               |
| test           | 初始测试目录，可删除                                         |
| .xxxx文件      | 这些是一些配置文件，包括语法配置，git配置等。                |
| `index.html`   | 首页入口文件，你可以添加一些 meta 信息或统计代码啥的。       |
| `package.json` | 项目配置文件。                                               |
| README.md      | 项目的说明文档，markdown 格式                                |

### 关系结构

#### 1) index.html

index.html只有一个`<div id="app">`

```vue
<script>document.write('<script src="./config/index.js?t=' + new Date().getTime() + '"><\/script>');</script>

<body>
  <div id="app"></div>
</body>
```

#### 2) main.js

main.js中import，并且new Vue

```vue
import Vue from 'vue'
import App from '@/App'
import router from '@/router'                 
// api: https://github.com/vuejs/vue-router
import store from '@/store' 

new Vue({
  el: '#app', // index.html中的div
  router,
  store,
  template: '<App/>',
  components: { App }
})
```

在 Vue 构造器中有一个el 参数，它是 DOM 元素中的 id。
这意味着我们接下来的改动全部在以上指定的 div 内，div 外部不受影响。

#### 3) App.vue

```vue
<template>
  <transition name="fade">
    <router-view></router-view>
  </transition>
</template>

<script>
    // 导出vue实例。相当于合并了以前的new vue和export导出组件
  export default {
  }
</script>
```

- 其中的路由视图标签是根据url要决定访问的vue
- 在main.js中提及了是使用的./router

component是导入了组件，template是使用了组件

attrgroup.vue (为了使结构清晰，删除很多代码)

```vue
<template>
<el-row :gutter="20">
    <el-col :span="6">
        <category @tree-node-click="treenodeclick"></category>
    </el-col>

    <el-col :span="18">
        <div class="mod-config">
            <el-form :inline="true" :model="dataForm" @keyup.enter.native="getDataList()">
                <el-form-item>
                    <el-button @click="getDataList()">查询</el-button>
    </el-form-item>
    </el-form>
            <el-table :data="dataList">
                <el-table-column type="selection"。。。></el-table-column>
                <el-table-column>。。。 </el-table-column>
    </el-table>

            <el-pagination 。。。></el-pagination>

            <!-- 弹窗, 新增 / 修改 -->
            <add-or-update v-if="addOrUpdateVisible" ref="addOrUpdate" @refreshDataList="getDataList"></add-or-update>

    </div>
    </el-col>
    </el-row>
</template>

<script>
    import Category from "../common/category";
    import AddOrUpdate from "./attrgroup-add-or-update";
    import RelationUpdate from "./attr-group-relation";
    export default {
        //import引入的组件需要注入到对象中才能使用。组件名:自定义的名字，一致可以省略
        components: { Category, AddOrUpdate, RelationUpdate },
        props: {},
        data() {
            return {
                catId: 0,
                dataForm: {
                    key: ""
                },
                dataList: [],
                pageIndex: 1,
                pageSize: 10,
                totalPage: 0,
                dataListLoading: false,
                dataListSelections: [],
                addOrUpdateVisible: false,
                relationVisible: false
            };
        },
        activated() {
            this.getDataList();
        },
        methods: {
```

#### vue.json

文件–首选项–用户代码片段–新建代码片段–取名vue.json

```vue
// https://www.cnblogs.com/songjilong/p/12635448.html
{
    "Print to console": {
        "prefix": "vue",
        "body": [
            "<!-- $1 -->",
            "<template>",
            "<div class='$2'>$5</div>",
            "</template>",
            "",
            "<script>",
            "//这里可以导入其他文件（比如：组件，工具js，第三方插件js，json文件，图片文件等等）",
            "//例如：import 《组件名称》 from '《组件路径》';",
            "",
            "export default {",
            "//import引入的组件需要注入到对象中才能使用",
            "components: {},",
            "data() {",
            "//这里存放数据",
            "return {",
            "",
            "};",
            "},",
            "//监听属性 类似于data概念",
            "computed: {},",
            "//监控data中的数据变化",
            "watch: {},",
            "//方法集合",
            "methods: {",
            "",
            "},",
            "//生命周期 - 创建完成（可以访问当前this实例）",
            "created() {",
            "",
            "},",
            "//生命周期 - 挂载完成（可以访问DOM元素）",
            "mounted() {",
            "",
            "},",
            "beforeCreate() {}, //生命周期 - 创建之前",
            "beforeMount() {}, //生命周期 - 挂载之前",
            "beforeUpdate() {}, //生命周期 - 更新之前",
            "updated() {}, //生命周期 - 更新之后",
            "beforeDestroy() {}, //生命周期 - 销毁之前",
            "destroyed() {}, //生命周期 - 销毁完成",
            "activated() {}, //如果页面有keep-alive缓存功能，这个函数会触发",
            "}",
            "</script>",
            "<style scoped>",
            "//@import url($3); 引入公共css类",
            "$4",
            "</style>"
        ],
        "description": "生成vue模板"
    },
    "http-get请求": {
	"prefix": "httpget",
	"body": [
		"this.\\$http({",
		"url: this.\\$http.adornUrl(''),",
		"method: 'get',",
		"params: this.\\$http.adornParams({})",
		"}).then(({ data }) => {",
		"})"
	],
	"description": "httpGET请求"
    },
    "http-post请求": {
	"prefix": "httppost",
	"body": [
		"this.\\$http({",
		"url: this.\\$http.adornUrl(''),",
		"method: 'post',",
		"data: this.\\$http.adornData(data, false)",
		"}).then(({ data }) => { });" 
	],
	"description": "httpPOST请求"
    }
}
```

> new Vue中指定了元素，元素如何渲染看template，组件决定元素样式。

## element-ui

### 快速准备

官网： https://element.eleme.cn/#/zh-CN/component/installation

安装

```shell
# 直接npm安装，在项目中执行
npm i element-ui -S

# 或者引入样式
```

使用：

在 main.js 中写入以下内容：

```vue
import ElementUI  from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css';

// 让vue使用ElementUI组件
Vue.use(ElementUI);
```

然后.vue文件中写标签

### 怎么改

main.js中有

```vue
new Vue({
  el: '#app', // 他是index.html中的div
  router,//router:router，是从上面的./router里来的 // 会替换<router-view/>
  components: { App },//App:App  属性名和属性值一样时可以简写 // 要用的组件
  template: '<App/>' // 导入的<template> <div id="app">
})

```

- el表示与index.html中的div关联，
- 在div里面要展示App，所以把App这个组件修改
- 在App.vue里说了export name 'App’是说把模板命名为App，所以我们替换他的模板
