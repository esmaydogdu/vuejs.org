## 什么是 Vuex?

Vuex 是一个专门为 Vue.js 应用设计的状态管理架构。它借鉴了 [Flux](https://facebook.github.io/flux/) 和 [Redux](https://github.com/rackt/redux) 的设计思想，但简化了概念和 API，并且采用了一种更加符合 Vue.js 的数据响应系统（reactivity system）的实现。

## 我为什么需要它？

当你的应用还很简单的时候，你可能并不需要 Vuex。我也并不建议在所有的场合都使用 Vuex。但是，如果你正在构建一个较大规模的 SPA，你可能已经开始思考应该如何处理 Vue 组件之外的应用结构。这就是 Vuex 要解决的问题。

我们在用 Vue.js 的时候，通常会把状态储存在组件的内部。也就是说，每一个组件都拥有一部分状态，整个应用的状态是分散在多个地方的。然而我们经常遇到的一个需求就是需要把一部分的状态共享给其它组件。通常我们会使用 Vue 或是第三方的事件系统去达到这个目的。但基于事件的问题在于，事件流会在逐渐增长的组件树中变得复杂，并且在出现问题的时候很难去发现问题的所在（典型的如事件 ping-pong，即子组件 dispatch 到父组件，再由父组件 broadcast）。

为了更好的解决在大型应用中共享状态的问题，我们需要把组件的本地状态 (component local state) 和应用状态 (application level state) 区分开来。应用级的状态不属于任何特定的组件，但每一个组件仍然可以通过 Vue 的响应系统去侦听其变化从而自动更新 DOM。通过把应用的状态管理逻辑放在同一个地方，我们就不需要在各个地方去处理各种事件，因为任何牵扯到多个组件的东西，都会放在这个地方。这样做也能使记录和检查状态的改变成为可能，甚至可以做出像 time-travel 这样的调试功能。

Vuex 也对状态管理的代码分离有一定程度的约束，但不会影响你实际代码结构的灵活性。