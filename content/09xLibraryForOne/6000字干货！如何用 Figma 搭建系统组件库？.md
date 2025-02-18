author:: 优设网 - 学设计上优设
source:: [6000字干货！如何用 Figma 搭建系统组件库？](https://www.uisdc.com/figma-building-a-component-library)
clipped:: [[2022-10-25]]
published:: 

组件库是一个强大的提效工具，对于设计师和开发来说有了统一的标准，输出的效率也会大大提高。

随着设计工具的不断发展，Figma 逐渐成为各大公司的主流设计软件。Figma 强大的[组件库](https://www.uisdc.com/tag/%e7%bb%84%e4%bb%b6%e5%ba%93)能力，非常适合团队设计系统的建设与应用。相比 Sketch，[Figma](https://www.uisdc.com/tag/figma) 在 Auto layout、变体和实例等方面极大的提升了组件库的设计灵活度和效率。

看完本文你将会学到：

1\. Sketch 与 Figma 组件库的区别

2\. Figma 组件库搭建经验分享

基础样式：字体（分层分级技巧）、颜色（分组排列规则）、阴影（分类、三层阴影）等

组件与变体：组件分类结构化原则、变体创建命名技巧、优化变体层级、组件预览展开还是合并、开关的使用和组件的链接等

组件文档：文档结构层级

组件库发布、使用、更新

3\. Figma 组件库搭建 Tips 分享

组件库是将界面设计中的具有通用性和标准规范的基础元素和重复出现的控件进行归纳整理，通过对控件进行分类和命名，最终形成一个可快速复用，便捷维护的资源库。对于设计师和开发来说，简单上手，可复用强，稳定且高效的组件库是非常有必要的。组件库更像是一个强大的工具库，既能提高团队的协作效率，也能保证团队设计输出的统一性、高效性和延续性。

![6000字干货！如何用 Figma 搭建系统组件库？](https://image.uisdc.com/wp-content/uploads/2022/02/uisdc-tx-20220226-1.jpg)

在 Figma 之前，我们都习惯了用 Sketch 创建组件库。但当开始使用 Figma 后，发现 Figma 不仅继承了 Sketch 组件库的优点，并且更加灵活和强大。

举一个简单的例子，如果想要修改组件的文本样式或者不同组件的颜色时，在 Sketch 中，就必须提前做好所有可能的文本/图层样式，非常的费时费力。但 Figma 强大的实例 Instances 功能，无须提前做好所有的样式，可以直接在实例上修改字体、颜色、描边、投影等，但又不会干扰到父级的样式，而修改父级的样式又能修改全局，非常的方便。又比如想要去切换一个按钮的状态，或者是否带图标时，Figma 强大的变体功能可以将这些属性进行分类整合在一起，组件调用更便捷，这都是 Sketch 组件不具备的功能。

除了实例、变体功能外，跨团队使用组件库（样式、组件）、实时更新、组件库的主题颜色一键切换、组件可以增加提示语等功能，都是 Sketch 不具备的。

提到组件库，不得不提到原子构建理论。Atomic Design（原子设计）是构建 Design System 的核心指导理论。化学中，所有的物体都是由原子构成，原子组合构成分子，分子组合构成有机物，最终形成了宇宙万物。

2013 年 Brad Forst 将此理论运用在界面设计中，形成一套设计系统，包含 5 个层面：原子、分子、组织、模板、页面。那么对应设计系统来说，我们的颜色、字体、图标以及按钮、标签等都会对应到相应的原子和分子，通过组件之间的搭配组合，最终构成页面。

![6000字干货！如何用 Figma 搭建系统组件库？](https://image.uisdc.com/wp-content/uploads/2022/02/uisdc-tx-20220226-2.jpg)

按照原子设计理论的思路，首先需要将组件库的类型进行分类，然后再从基础和核心的元素入手，进行元素、组件、模块的搭建。

组件库一般由基础样式、控件和组件文档构成。基础样式包括颜色样式、文字样式、效果样式（主要是阴影），组件主要就是控件（相当于 Sketch 的 Symbols），组件文档相当于对组件的样式和状态的展示说明。

![6000字干货！如何用 Figma 搭建系统组件库？](https://image.uisdc.com/wp-content/uploads/2022/02/uisdc-tx-20220226-3.jpg)

##### 1\. 组件库：基础样式搭建

我们可以直接在文档里创建样式库，简单且灵活。当然更建议大家单独创建一个全局样式的文件，包括颜色、文字、效果等，这样做的好处是在以后进行项目切换时，可以很方便快速的进行配置和替换，且可以共用一份原始的组件，高效且有关联性。

这里要跟大家提一个概念 Design Token。Design Token 是存储样式值（如色值、字重、阴影、圆角等）的载体。Design Token 最重要的意义是做到设计与研发的样式完全打通，进行无损耗的沟通，增强系统的可维护性，同时可以约束设计侧的样式数量。但是 Figma 本身对 Token 的支持不够全面，比如圆角等，所以需要自研插件来弥补这些不足。

**全局样式：颜色样式**

颜色是页面整体风格表现的重要基本元素，它可以建立品牌的识别性，梳理页面的视觉层级关系，突出内容并平衡其他视觉元素。建议大家可以按照功能和属性，将颜色进行分组分类命名，比如主色、浅主色、中性色和功能色等，并将默认、悬浮、点击、禁用等颜色放在一组，方便大家使用。

![6000字干货！如何用 Figma 搭建系统组件库？](https://image.uisdc.com/wp-content/uploads/2022/02/uisdc-tx-20220226-4.jpg)

**全局样式：文字样式**

在文字样式中会包括：字号、字重、行高和字距等。在创建文字样式前，将文字样式分为段落样式和文本样式加以区别。将产品内的一些文字梯度以及功能描述等用表格的形式进行整理，并分别创建相应的字号和字重。需要注意的是不要单纯的将名称命名为 T0、T1 等纯符号性的名称，可以在后面加上适当的描述，比如 T0 辅助、T1 标准等文案，同时也可以在描述里添加对应的使用说明，这样当鼠标悬浮在这个样式上，会给用户带来提示性的预览。这种办法同样适用于颜色、阴影等全局样式，会更加方便大家调用且能够很好的解除新用户的使用疑虑。

![6000字干货！如何用 Figma 搭建系统组件库？](https://image.uisdc.com/wp-content/uploads/2022/02/uisdc-tx-20220226-5.jpg)

**全局样式：效果样式**

效果样式一般来说主要是常用的阴影样式，比如外阴影、内阴影等。阴影值应该遵循现实物理世界中物体的特性。因此在阴影的设定上采用了三层阴影的表达方式，让阴影更加柔和，更符合真实光源下的物体状态。物体的高度直接影响阴影，离地面越高阴影越大，模糊值越高，反之相反。

![6000字干货！如何用 Figma 搭建系统组件库？](https://image.uisdc.com/wp-content/uploads/2022/02/uisdc-tx-20220226-6.jpg)

同时，为了让组件库阴影层级更加丰富通用，我们将阴影层级划分了 S 类和 L 类两个层级。S 类阴影用于通过交互后出现的场景，其内容带来上下文信息切换，需要抢占用户注意力，更需要提供明确的边界，主要用于基础组件。L 类阴影往往用于多个共存的列表，更加强调整体的柔和性，主要用于导航、首页、模版等业务场景。同时为了能让大家更加清晰的区分阴影的层级，会将常用的一些组件和场景填充在一个表格中，方便大家查阅。

![6000字干货！如何用 Figma 搭建系统组件库？](https://image.uisdc.com/wp-content/uploads/2022/02/uisdc-tx-20220226-7.jpg)

##### 2\. Component 组件

Component 组件相当于 Sketch 的 Symbol。不同之处在于 Component 比 Symbol 更灵活更强大，我们可以用更少的组件做更多的事情，接下来会通过以下几个方面来简要介绍一下 Figma 中组件的相关知识。

**Auto layout：创建组件能用尽用**

Auto layout 是 Figma 非常强大的一个功能，创建带有自动布局的组件，通过组合这些响应组件，可以创建可跨多种设备类型工作的设计。在创建组件的时候，一定要把这个功能很好的应用，这样对于组件的拓展和应用会非常灵活。比如常用的按钮、对话框、Toast 等等组件，能用尽用。

![6000字干货！如何用 Figma 搭建系统组件库？](https://image.uisdc.com/wp-content/uploads/2022/02/uisdc-tx-20220226-8.jpg)

**组件结构化：寻找操作更容易**

结构化的基本原则是：方便检索控件（Components）、方便编辑控件、清晰地传达控件分组和状态。建议在团队或公司中定义好组件的结构，可依照自己相关的业务，将一些通用性较强的基础组件进行划分。将组件按照属性和状态放在不同的页面里，而不是将所有组件全部堆叠在一个页面。比如数据输入类下面，将常用的输入框、单复选、上传等放置到一起，这使得以下操作变得更容易：在资源面板中查找组件、相关组件之间的交换、提高公司内团队资源库的使用率。

![6000字干货！如何用 Figma 搭建系统组件库？](https://image.uisdc.com/wp-content/uploads/2022/02/uisdc-tx-20220226-9.jpg)

**强大的变体功能：构建组件库的灵魂和精髓**

谈到组件，不得不提到 Figma 强大的变体功能。用户可以通过变体功能更加方便和灵活的调用组件库，这相对于 Sketch 来说，简直是好用太多。

当你创建组件并建立起你的设计系统时，你会发现需要一些彼此相似的组件，而只有微小的差别。例如：多个按钮的组件，有不同状态和尺寸的独立组件，以及明暗模式或者有无 icon 等，都可以用变体的形式去创建。

![6000字干货！如何用 Figma 搭建系统组件库？](https://image.uisdc.com/wp-content/uploads/2022/02/uisdc-tx-20220226-10.jpg)

**超好用的变体功能——理解属性和值的概念很重要**

大家在创建变体的时候经常会有一些困惑，尤其是对于状态非常繁杂的组件，简直是无从下手，尤其是对于属性 Property 和值 Variant 更是觉得很模糊。这里有一些经验分享给大家:

首先要了解下一相关的概念，属性 Property：是组件的可变方面。例如：一个按钮组件的属性可以是尺寸、状态，或是否有 icon，可以将其理解为分类。

值 Variant：是每个属性可用的不同选项。例如：状态属性可以有默认、悬浮、点击和禁用等，可以将其理解为分类下的参数。然后再了解一下 Figma 的命名规则，Figma 使用斜线命名系统来组织资产面板和实例菜单中的组件。

组件名称中的每一个"/"都会创建一个层次。第一个"/"之前的文字将成为组件集的名称，这里需要着重注意一下。比如名称为 Button/Primary/Large/Default/False 的按钮组件将有以下属性和值。组件名称/值/值/值/值。变体名称遵循这个结构，Property1=value, Property2=value, Property3=value。

![6000字干货！如何用 Figma 搭建系统组件库？](https://image.uisdc.com/wp-content/uploads/2022/02/uisdc-tx-20220226-11.jpg)

**分门别类：变体创建的精髓**

掌握好命名规则就掌握了变体创建的精髓。教给大家一个非常好用的方法，在创建变体前，首先把需要创建变体的组件进行分类，并统一放在一个草稿上，比如说按钮的尺寸、状态、有无图标等。然后将对应的分类写出相应的值，比如尺寸对应的值就是 m 和 s，状态对应的就是默认、悬浮、点击等。分类好以后，按照上面所述属性和值的对应关系，分别将这些属性和值一一对应填在草稿上。然后再根据 Figma 的命名规则，将所有组件的名称命名完成，比如 Button/m/默认/no/yes，然后就可以直接创建了。

![6000字干货！如何用 Figma 搭建系统组件库？](https://image.uisdc.com/wp-content/uploads/2022/02/uisdc-tx-20220226-12.jpg)

**化繁为简：优化变体层级**

Figma 的变体功能很强大，可以进行很多样式的排列组合。但是我们也发现在创建变体的时候，如果按照每个状态、种类进行划分的时候，整个组件会非常的繁杂臃肿。比如 Popover，会发现在创建它的各种状态时会非常麻烦，除了箭头在各个方向的位置外，还要考虑里面元素的组合，比如纯文本、标题+文本、标题+图文、文本+按钮等等，这样组合起来的组件会非常的臃肿，也不利于设计师去选择。所以我们要学会层级的梳理，比如可以将箭头、按钮、标题图文进行一个分布组合，然后再将这些组合成一个新的组件，通过嵌套的层级关系去调整每个层级的位置关系或者剔除某些不需要的层级。

![6000字干货！如何用 Figma 搭建系统组件库？](https://image.uisdc.com/wp-content/uploads/2022/02/uisdc-tx-20220226-13.jpg)

**组件链接：组件跳一跳，规则全知道**

创建好组件以后，可以给每个组件都添加相关的链接，这个链接可以添加到组件的描述中，这样开发人员和设计人员就可以在 Inspect 中点击相关的按钮直接跳转链接了，简直不要太好用。比如组件文档链接（可以查看详细的交互规则）、线上的开发地址（可以查看线上的样式），以及直接点击右上角的跳转按钮跳转到组件文档。这样就打通了所有线上线下的样式规则，非常方便用户查阅和使用。

![6000字干货！如何用 Figma 搭建系统组件库？](https://image.uisdc.com/wp-content/uploads/2022/02/uisdc-tx-20220226-14.jpg)

**资源预览：展开还是合并更好？**

相信大家在调用组件的时候都会发现一个问题，有的变体预览是展开显示的，有的变体预览是合并在一起的，那么这个分类办法到底是怎么去划分的呢？通常来说需要大家一眼就能选择，减少用户思考的，可以考虑分开建设变体，比如常见的按钮。我们只需要预览图下的各种形态就能找到想要调用的按钮类型。如果按钮全部的集合到一个变体中，那么大家看到的只有一个按钮，对于用户来说会增加判断和选择的时间，是很不方便的。但是对于一些大家理解起来比较容易且展开后的变体样式非常多的的组件，比如 toast、表格，不需要将其各种变体分别的罗列出来，引导用户点击进去，再选择就好了。

![6000字干货！如何用 Figma 搭建系统组件库？](https://image.uisdc.com/wp-content/uploads/2022/02/uisdc-tx-20220226-15.jpg)

**开关：怎么这么好用**

大家在建设组件的时候都会发现一个问题，有的组件是开关显示的，有的是下拉显示的。这是因为如果你有一个只有两个可能选项的属性，Figma 会自动将 true/false、yes/no 和 on/off 都识别为开关。所以大家在做变体的时候，尽可能的将这种只有两个可能属性的选项显示为开关，减少用户的操作流程。

![6000字干货！如何用 Figma 搭建系统组件库？](https://image.uisdc.com/wp-content/uploads/2022/02/uisdc-tx-20220226-16.jpg)

**组件文档：组件类型和状态的展示说明**

为了方便大家能够清晰知道组件的相关属性和类别，可以为每个组件创建一个组件文档，方便大家查阅和调用。这对于刚接触到这个组件的人来说非常友好。组件文档的结构一般是由组件名称、母文档链接（交互说明）、基本样式、主要组件和相关组件构组成。在这个文档里可以查看组件的类别和相关状态，以及组成这个组件用到的其他组件，并且通过链接都可以跳转到相应的组件，非常方便。

![6000字干货！如何用 Figma 搭建系统组件库？](https://image.uisdc.com/wp-content/uploads/2022/02/uisdc-tx-20220226-17.jpg)

**组件库：发布、更新、使用**

可以将组件库发布到团队的资源库。如果要跨文件使用组件，只能通过专业版团队的团队库发布和使用。当每次有更新发布样式或主组件时，Figma 将自动通知到每一个成员，点击更新即可应用。管理员可以提前默认设置将哪些组件库开启哦，减少了新用户每次进入页面还要重新选择。

在 Assets 面板下，可以通过搜索的方式找到需要调用的组件；也可以通过展开菜单的方式找到需要的组件。将需要使用的组件直接拖动至文件中，便可使用。推荐大家使用搜索的方法，效率会更高。

![6000字干货！如何用 Figma 搭建系统组件库？](https://image.uisdc.com/wp-content/uploads/2022/02/uisdc-tx-20220226-18.jpg)

**组织版：更加强大的功能体验**

对于组织版来说，我觉得比较好用的功能就是组件统计和分支。Figma 组织版可以统计组件数量、使用团队、调用次数等，这对于组件的使用情况统计来说，非常的方便和直观。分支功能可以让每个成员单独创建主文件的分支，可以在其中探索对文件或库的样式、组件和其他方面的更改，而不会影响主文件。当更改感到满意时，你可以查看分支并将其与主文件合并。所以对于团队来说，组织版的这两个功能还是非常实用的。

**Figma 组件库搭建 Tips：全是干货，一目了然**

为了确保值与属性相匹配，每个组件都需要有相同数量的斜线。

如果你有一个只有两个可能选项的属性，Figma 将 true/false、yes/no 和 on/off 都识别为开关。

修复值的冲突错误：如果任何变体的值组合完全相同，Figma 会让你知道存在冲突。即使变体本身在视觉上不同，也会看到这个错误。

Figma 将使用左上角的变体作为默认变体，此变体将代表资产面板中的整个组件集。

如果你不确定某个组件集有哪些变体，或者它们的原始样式，你可以在原始文件中查看组件集。

使用·或者\_可隐藏不需要展示的组件。

组件内部预设元素只能减少，要增加需拆解。

不要将组件完全拆解、嵌套元素都支持修改。

使用 Autolay out，对齐自适应更智能。

使用全局样式，一键修改更方便。

跨文件使用组件，只能通过专业版团队的团队库发布和使用组件。

组件库是一个强大的提效工具，对于设计师和开发来说有了统一的标准，输出的效率也会大大提高。对于团队来说能很好的提升产品的品牌感和体验，尤其在 Figma 强大特性的帮助下，将发挥更大的作用。同时我们也一定要学会整体思考、善于总结，不断优化和完善组件的细节，将组件库的特性发挥到最大。

由于篇幅有限，关于组件库某些内容介绍的不够全面，如果有不严谨、错误的地方还望大家给与指正，欢迎大家一起学习和讨论。

欢迎关注作者的微信公众号：「百度MEUX」

![6000字干货！如何用 Figma 搭建系统组件库？](https://image.uisdc.com/wp-content/uploads/2020/10/qrbdmeux.jpg)