---
title: 2018年 React Native 官方展望
author: Sophie Alpert (translator - wlfcss)
---

自从上次发布关于React Native的更新状态已经有一段时间了。

在Facebook内部，我们将React Native技术应用到更多的重要项目中。我们最受欢迎的产品之一是Marketplace，作为我们的顶级应用，每月有8亿人使用。自2015年构建以来，Marketplace已完全使用React Native构建，共计超过100个视图（页面）。

我们也在应用的许多新部分使用 React Native。如果您看了上个月的F8主题演讲，就会发现 Blood Donations、Crisis Response、Privacy Shortcuts 和 Wellness Checks 的所有新功能都是使用 React Native 构建的。Facebook 主应用以外的项目也在使用 React Native。新的 Oculus Go VR 头戴式设备对应的[移动应用程序](https://www.oculus.com/app/) 就完全使用 React Native 构建。

当然，我们也使用许多其他技术来构建我们的应用程序。[Litho](https://fblitho.com/)和[ComponentKit](https://componentkit.org/)是我们在应用程序中广泛使用的两个库;React Native 的目标从来都不是替代其他技术，专注于 React Native 自身，努力使之变得更好，但依旧希望看到其他团队从 React Native 中得到一些想法或灵感，例如将[instant reload（即时重载）](https://instagram-engineering.com/instant-feedback-in-ios-engineering-workflows-c3f6508c76c8)运用到非 JavaScript 代码中。

## 架构

当我们在2013年启动React Native项目时，React Native 项目的设计初衷是成为 JavaScript 和原生应用之间的一个异步，序列化和批处理的“桥梁”。
React DOM 将 React 的状态更新变成了命令式、可变的 DOM API 调用，如 `document.createElement(attrs)` 和 `.appendChild()`，而 React Native 则返回一个单独的 JSON 消息，它列出了要执行的一些操作，如 `[["createView", attrs], ["manageChildren", ...]]`。就像React DOM将React状态更新变成命令式的，对document.createElement（attrs）和.appendChild（）等DOM API的可变调用一样，React Native被设计为返回一个列出要执行的突变的JSON消息，如[[“createView “，attrs]，[”manageChildren“，...]]。 我们将整个系统设计为永不依赖获取同步响应，并确保列表中所有的内容都可以完全序列化为 JSON，并可以反序列化回来。这样做是为了提高灵活性：在这个架构之上，可以构建像 [Chrome 调试器](https://facebook.github.io/react-native/docs/debugging.html#chrome-developer-tools)之类的工具，这些工具可以通过 WebSocket 连接异步运行所有的 JavaScript 代码。

在过去的五年里，我们发现最初的设计原则加大了某些特性的开发难度。异步桥接（asynchronous bridge）意味着不能直接将 JavaScript 逻辑与很多原生 API 集成在一起，因为这些原生 API 是同步的。批量桥接（本地调用队列）意味着 React Native 应用程序调用本地函数会更加困难。而且串行化的桥接意味着不必要的复制，因为它不是直接在两个世界之间共享内存。对于完全使用 React Native 构建的应用程序，这些限制通常是可承受的。但对于在 React Native 与现有原生代码之间进行复杂集成的应用程序，就非常糟糕了。

**因此，Facebook 正在对 React Native 进行大规模重构，让框架变得更加灵活，并更好地与JavaScript / 原生混合应用中的原生基础设施集成。** 通过这个项目，将应用在过去 5 年中学到的知识，逐步让架构走向现代化。我们正在重构 React Native 的核心部分，大部分工作都是在底层进行的，
现有的 React Native 应用程序几乎不需要做出更改

为了使 React Native 更轻量化并能更好地适应现有的原生应用，此次重构主要从三个方面进行。首先，我们改变了线程模型：UI 更新不再需要在三个不同的线程上执行，可以在任意线程上同步调用 JavaScript 进行优先更新，同时将低优先级工作推出主线程，以便保持对 UI 的响应。其次，将[异步渲染](https://reactjs.org/blog/2018/03/01/sneak-peek-beyond-react-16.html)功能引入 React Native 中，允许执行多个渲染并简化异步数据处理。最后，简化桥接，让它更快、更轻量。原生和 JavaScript 之间的直接调用效率更高，并且可以更轻松地构建调试工具，如跨语言堆栈跟踪。

完成以上工作之后，将带来更紧密更合理的集成。现在，如果不通过复杂 hack 的手段就无法让原生导航和手势处理或原生组件（如 UICollectionView 和 RecyclerView）一起工作。在对线程模型做出更改之后，我们将可以直接构建这样的功能。

当这个项目将要完工时，Facebook 会披露更多的细节，敬请期待。

## 社区

除了Facebook 内部社区外，我们很高兴在Facebook之外拥有蓬勃发展的React Native用户和合作者。 我们希望与React Native社区有更多的沟通与支持，以此能更好地为React Native用户提供服务并让开发者更易于做出贡献。

React Native底层体系结构的更改将有利于与其他原生基础架构更加简单地进行交互操作一样，React Native在JavaScript端应该更加简单轻度，以更好地适应JavaScript生态系统，包括VM和bundler之间的通信交换。我们知道变革的步伐很难跟上，所以我们希望找到减少频繁发布新版本的方法。 最后，我们知道现有的文档缺少关于启动优化等诸多方面的内容，这些情况将在未来一年中有所改善。

如果您使用的是React Native，那么您就是我们社区的一部分; 请将您使用React Native的困惑反馈给我们。

虽然React Native只是移动开发者工具箱中的一个工具，但我们对其有充分的信心与支持 - 我们每天都在改进，去年有500名贡献者提交了超过2500次提交。