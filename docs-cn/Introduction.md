
# 介绍

[Slate](http://slatejs.org) 是一个 _完全_ 可定制的富文本编辑框架。[GitHub ⬈](https://github.com/ianstormtaylor/slate)

通过 Slate，你可以构建出类似 [Medium](https://medium.com/)、[Dropbox Paper](https://www.dropbox.com/paper) 或者 [Canvas](https://usecanvas.com/) 这样使用直观、富交互、体验业已成为 Web 应用标杆的编辑器。同时，你也无需担心在代码实现上陷入复杂度的泥潭之中。

Slate 之所以能做到这一点，是因为它的所有逻辑都是通过一系列的插件实现的。这样，你就再也不会被某项特性 _在_ 或 _不在_ 编辑器【核心】边界之内的问题所困扰了。你可以将它理解为在 [React](https://facebook.github.io/react/) 和 [Immutable](https://facebook.github.io/immutable-js/) 基础上，一种可插拔的 `contenteditable` 实现。它也受到了 [Draft.js](https://facebook.github.io/draft-js/)，[Prosemirror](http://prosemirror.net/) 和 [Quill](http://quilljs.com/) 这些类库的启发。

_**Slate 目前还处于 beta 状态**。目前它已经可用，但你可能需要通过 pull request 修复若干复杂使用场景下的问题。_

<br/>

### Why?

为什么发明 Slate 呢？好吧…_（注意，这部分内容包含了一些[我](https://github.com/ianstormtaylor)的个人观点！）_

在发明 Slate 之前，我尝试了许多不同的富文本编辑器。我发现虽然它们在编写简单示例时基本没有问题，但一旦你想要构建一些类似 [Medium](https://medium.com/)、[Dropbox Paper](https://www.dropbox.com/paper) 或者 [Canvas](https://usecanvas.com/) 这样的内容，你就必须使用各种奇技淫巧来实现你所期望的用户体验。并且，某些体验甚至是无法实现的。在这个过程中，你的代码会变得越来越难维护。

当然，这些都是我的个人观点，并且如果这些类库满足了你的需求，放心用！不过，如果在使用它们的过程中你都遇到了相似的问题，那么也许你会喜欢上 Slate。让我来介绍一下 Slate 是如何解决这些问题的吧…


<br/>

### 原则

Slate 尝试通过一些原则来解决 "[Why?](#why)" 这一节中的问题：

1. **作为一等公民的插件。** 在 Slate 中最重要的一点是，插件是一等公民（first-class）的实体——甚至连编辑器的核心逻辑都是通过插件实现的。这意味着你能够 _完全地_ 定制编辑体验，构建出对标 Medium 和 Canvas 那样的复杂编辑器，而无需对抗各种类库的预设条件。

2. **精简 Schema 的核心。** Slate 的核心逻辑并不对你所编辑的数据结构做任何假设，这意味着你在需要应对复杂场景时不会被编辑器预置的内容所束缚（译者注：此处 Schema 可理解为类似 XML Schema 的文档结构规范）。

3. **支持嵌套的文档模型。** Slate 所使用的文档模型是一棵嵌套的、递归的树，和 DOM 本身十分接近。这使得构建表格和嵌套引用等能够满足进阶需求的复杂组件成为了可能。当然，你同样可以使用单一的层级关系以保证简单性。

4. **无状态、不可变的数据。** 通过使用 React 和 Immutable.js，我们是基于不可变数据结构，以无状态的方式构建 Slate 编辑器的。这大大降低了理解代码的难度，也节约了大量开发插件的时间。

5. **直观的 changes。** Slate 中的内容是通过 "change" 来编辑的，这是一种被设计为支持高阶使用，且极其符合直觉的概念。这样，我们就能够通过它来尽可能简单地编写插件和自定义功能了。

6. **为协同编辑准备的数据模型。** Slate 使用的数据模型——尤其是由 change 更改文档的方式——在设计时就已考虑到对协同编辑的支持。所以，如果你决定为编辑器添加协作功能，你不需要进行彻底的重构。（当然，这还需要你投入更多的努力！）

7. **明确的【核心】边界划分。** 通过插件优先的架构与精简 Schema 的内核，Slate 对于【核心】和【自定义】有着明确得多的划分，从而保证核心的编辑体验不会为各种边缘情况所困扰。

<br/>

### Demo

[**在线示例**](http://slatejs.org)页中可查看全部示例！


<br/>

### 示例

为了对如何使用 Slate 有个基础的概念，不妨查阅如下的若干示例：

- [**纯文本**](https://github.com/ianstormtaylor/slate/tree/master/examples/plain-text) — 展示了最基础的情形：一个经过美化的 `<textarea>`。
- [**富文本**](https://github.com/ianstormtaylor/slate/tree/master/examples/rich-text) — 展示了一个能满足基本功能性需求的富文本编辑器。
- [**自动 Markdown**](https://github.com/ianstormtaylor/slate/tree/master/examples/markdown-preview) — 展示了如何通过添加关键的事件 handler 来处理类似 Markdown 的快捷键。
- [**链接**](https://github.com/ianstormtaylor/slate/tree/master/examples/links) — 展示了如何将纯文本与其关联的数据 wrap 为 inline 节点。 
- [**图片**](https://github.com/ianstormtaylor/slate/tree/master/examples/images) — 展示了如何使用 void（无文本）节点来添加图片。
- [**悬浮菜单**](https://github.com/ianstormtaylor/slate/tree/master/examples/hovering-menu) — 展示了如何实现一个上下文相关的悬浮菜单。
- [**表格**](https://github.com/ianstormtaylor/slate/tree/master/examples/tables) — 展示了如何通过嵌套 block 节点来渲染更加高级的组件。
- [**粘贴 HTML**](https://github.com/ianstormtaylor/slate/tree/master/examples/paste-html) — 展示了如何使用 HTML 序列化器来支持粘贴入的 HTML 内容。
- [**代码高亮**](https://github.com/ianstormtaylor/slate/tree/master/examples/code-highlighting) — 展示了如何通过装饰器来动态标记文本。

如果你对于展示泛用性的示例有着自己的想法，请提出 pull request 吧！


<br/>

### 插件

Slate 鼓励你编写小而可复用的模块。下面这些公用的插件已经在你的项目中可用！

- [`slate-auto-replace`](https://github.com/ianstormtaylor/slate-auto-replace) 在用户输入时自动替换文本，对【智能】排版非常实用！
- [`slate-collapse-on-escape`](https://github.com/ianstormtaylor/slate-collapse-on-escape) 在 `escape` 键按下时缩起当前 selection。
- [`slate-edit-code`](https://github.com/GitbookIO/slate-edit-code) 支持形如 tab 缩进、enter 键软换行的代码编辑操作。
- [`slate-edit-list`](https://github.com/GitbookIO/slate-edit-list) 支持富交互、嵌套的列表编辑操作。
- [`slate-edit-table`](https://github.com/GitbookIO/slate-edit-table) 支持复杂的表格编辑！
- [`slate-paste-linkify`](https://github.com/ianstormtaylor/slate-paste-linkify) 在由剪贴板粘贴入 URL 时，将选中的文本转换为链接。
- [`slate-prism`](https://github.com/GitbookIO/slate-prism) 使用 [Prism.js](http://prismjs.com/) 支持代码高亮！
- [`slate-soft-break`](https://github.com/ianstormtaylor/slate-soft-break) 在 `enter` 键按下时插入一个软换行。
- [`slate-drop-or-paste-images`](https://github.com/ianstormtaylor/slate-drop-or-paste-images) 实现对用户拖拽或粘贴以插入图片的支持！
- [**在 `npm` 上查看所有插件...**](https://www.npmjs.com/browse/keyword/slate)

<br/>

### 文档

<!-- TODO 更新文档链接至中文页 -->

如果这是你第一次使用 Slate，不妨查看 [Getting Started](http://docs.slatejs.org/walkthroughs/installing-slate.html) 中的实战部分来了解 Slate 的架构和思维模型。在你熟悉之后，还可以查看完整的 [API 参考](http://docs.slatejs.org/reference/slate-react/editor.html)。

- [**实战**](http://docs.slatejs.org/walkthroughs/installing-slate.html)
- [**API 参考**](http://docs.slatejs.org/reference/slate-react/editor.html)
- [**FAQ**](http://docs.slatejs.org/general/faq.html)
- [**资源**](http://docs.slatejs.org/general/resources.html)

如果这还不够，你还可以随时阅读添加了大量 Readme 并重度注释的[源码](./src)。


<br/>

### 贡献！

非常欢迎各种形式的贡献！查看[贡献指南](./Contributing.md)来了解更多信息吧！

Slate 使用 [MIT 许可协议](./License.md)。