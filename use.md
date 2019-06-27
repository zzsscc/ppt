title: title
speaker: zsc
url: https://github.com/zzsscc
js:
    - index.js
    - https://www.echartsjs.com/asset/theme/shine.js
css:
    - index.css
prismTheme: okaidia
plugins:
    - echarts
    - katex
    - mermaid: {theme: forest}

<slide class="bg-black-blue aligncenter" image="https://source.unsplash.com/C1HhAQrbykQ/ .dark .anim">

### js装饰器的前世今生{.text-landing.text-shadow}

By zsc {.text-intro.mt5percentage}

[:fa-github: Github](https://github.com/tc39/proposal-decorators){.button.ghost.animated.flipInX.delay-1200}

<note class="black">
TC39是ECMAscript的一部分  
是推动JavaScript发展、控制ECMAScript版本发布的技术委员会  
其会员都是公司（其中主要是浏览器厂商）  
TC39 实行的是协商一致的原则：通过一项决议必须得到每一位会员（公司代表）的赞成。
</note>

<!-- slide-2 -->
<slide class="animated bgc-silde2">

:::header
相关历史{.white.font30.text-shadow}
:::

!![](https://yehudakatz.com/content/images/2015/05/Yehuda-Katz-Slack.jpeg .size-20.alignright)

三年多以前，[Yehuda Katz](https://yehudakatz.com/) 首先提出了装饰器的概念。TypeScript 在 1.5 版本（2015）中发布了对装饰器的支持以及许多 ES6 的相关特性。 一些主流框架，如 Angular 和 MobX 等开始使用它们来增加开发者体验：这使得装饰器非常受欢迎，并给社区带来了一种已经稳定的错觉，或者觉得装饰器是ES7推出的特性。[ES2016最终特性](http://2ality.com/2016/01/ecmascript-2016.html)

Babel 第一次实现装饰器是在 v5 版本中，但由于该提案仍在不断变化，则在 Babel v6 中移除了它们。Logan Smyth 创建了一个非官方的插件(babel-plugin-transform-decorators-legacy)，它延用了 Babel 5 中装饰器的行为；在 Babel 7 的 alpha 版本发布期间该库被移至 Babel 官方的仓库中。当时该插件仍使用[旧的装饰器语法](https://github.com/tc39/proposal-decorators-previous)，因为新提案尚未明确。

<note class="black">
TC39的装饰器提案共3个  
类和类属性装饰器、函数装饰器、方法参数装饰器，后2个仍处于Stage 0中  
Decorator只是有望在ES2016推出的，实际上并没有  
Array.prototype.includes  
指数运算符  
提案达到阶段4  
也只能确保该提案将被包含在标准  
将其列入下一版本的ECMAScript是可能的  
但也不是100％肯定
</note>

<!-- slide-3 -->
<slide class="animated bgc-silde2">

:::header
相关历史{.white.font30.text-shadow}
:::

自那时起，Daniel Ehrenberg、Brian Terlson 以及 Yehuda Katz 就一起成为了该提案的共同作者，该提案几乎已被完全重写。当然并非一切事情都已确定，因为至今尚未出现符合规范的实现方式。

Babel 7.0.0 为 @babel/plugin-proposal-decorators 插件引入了新的标识：legacy 选项，其唯一有效值为 true。

<note class="black">
在 Babel 7.0.0 中如果我们不设置 legacy: true 选项  
默认情况下就不能使用该语义（相当于 legacy: false）
</note>

<!-- slide-4 -->
<slide class="animated bgc-silde2">

:::header
新提案现状{.white.font30.text-shadow}
:::

!![](https://gss0.bdstatic.com/94o3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike80%2C5%2C5%2C80%2C26/sign=d8bde17f00f79052fb124f6c6d9abcaf/d009b3de9c82d15834a6cbdd890a19d8bc3e42b2.jpg .size-40.alignleft)

新提案的装饰器现在处在[Stage 2阶段](https://github.com/tc39/proposals) {.tobuild..fadeInUp}

Babel 7.1.0 最终支持了新的装饰器提案：你可以使用 [@babel/plugin-proposal-decorators](https://babeljs.io/docs/en/babel-plugin-proposal-decorators#simple-class-decorator) 插件来提前尝试此功能 🎉{.tobuild..fadeInUp}

<!-- 在 Babel 7.1.0 中，我们引入了对这个新提案的支持，并且当 @babel/plugin-proposal-decorators 插件被使用时，默认启用。而在 Babel 7.0.0 中如果我们不设置 legacy: true 选项，默认情况下就不能使用该语义（相当于 legacy: false）{.tobuild..fadeInUp} -->

新提案同时支持使用装饰器访问实现私有字段（private fields）和私有方法（private methods）。我们尚未在 Babel 中实现此功能（在每个 class 中使用装饰器或私有元素），但我们会很快去出现它{.tobuild..fadeInUp}

__设计组正在考虑将该提案重新设计为“static decorators”__{.tobuild..fadeIn}

<note>
这里可以查看当前中各个阶段的提案
草案是规范的第一个版本  
表明委员会希望它们最终包含在标准的JavaScript编程语言中  
与最终标准中包含的特性不会有太大差别  
原则上只接受增量修改  
这个阶段开始实验如何实现  
实现形式包括polyfill  
实现引擎（提供草案执行本地支持）  
或者编译转换（例如babel）  
Object.observe是一个例子  
当它达到阶段2后，  
但最终却被撤回了。  
静态可分析性  
装饰器只能以相当固定的方式组合，使它们更具静态可分析性。
</note>

<!-- slide-5 -->
<slide class="black" image="https://source.unsplash.com/UJbHNoVPZW0/ .light">

:::header
新提案启用了JavaScript原始装饰器提议的基本功能，包括TypeScript装饰器中可用的大多数功能。但还是有一些重要的差异是他们互不兼容{.white.font20}
:::

:::steps

![](https://source.unsplash.com/uPGOEbjbVGA/800x600){.height200}

导入装饰器时，包含@作为装饰器名称的一部分

@foo.bar或@(foo)不再允许

定义装饰器的语法完全不同：使用特殊的“组合装饰器”语法而不是其他装饰器提议中的函数

TypeScript会将所有instance decorators在所有static decorators前运行，此提案将完全基于程序的顺序，无论是静态或实例

目前Babel转换的装饰器是一个处理所有变化的回调形式，而不是针对不同内置装饰器的不同回调。

目前Babel转换的装饰器将属性描述符传递给回调，并自动应用它，而@register强制您自己获取并设置属性描述符。

---

![](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1561526096438&di=278f2499eb50e809ac173a3306be3307&imgtype=0&src=http%3A%2F%2F5b0988e595225.cdn.sohucs.com%2Fimages%2F20180530%2F9da10880799b46cfb9a44e08f70fb059.jpeg){.height200}

~~参数装饰器~~

~~定义新的私有字段或方法~~

~~类装饰器访问操作类中的所有字段和方法~~

~~基于描述符~~

---

![](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1561464506961&di=bb6c76718447b23a57d247bfb24b8f06&imgtype=0&src=http%3A%2F%2Ftc.sinaimg.cn%2Fmaxwidth.800%2Ftc.service.weibo.com%2Fimg_boqiicdn_com%2F08ab73fec5a46c0903b253b249c56a0e.jpg){.height200}

__未来的内置装饰器将以更静态可分析的方式添加相同的功能__

@wrap 使用给定函数的返回值替换方法或整个类

@register 创建类后调用回调

@expose 调用一个回调给定函数，以在创建类后访问私有字段或方法

@initialize 在创建类的实例时运行给定的回调

{.tobuild..fadeInDown}

:::

<note>
不再是表达式  
该装饰者提案旨在通过努力实现双重目标来改进过去的提案：  
不仅要使用装饰器，还要编写自己的装饰器应该很容易  
装饰器应该很快，既可以在转换器中生成良好的代码，也可以在本机JS实现中快速执行  
不过虽然改变了这么多，甚至几乎重写，但是装饰器的本质没有变
</note>

<!-- slide-6 -->
<slide class="black" image="https://source.unsplash.com/UJbHNoVPZW0/ .light">

!![](https://image-static.segmentfault.com/202/537/2025373486-59537ddc13f67_articlex .size-40.alignright)

装饰模式和适配器模式都是 包装模式 (Wrapper Pattern)，它们都是通过封装其他对象达到设计的目的的，但是它们的形态有很大区别。

__适配器模式__ 我们使用的场景比较多，比如连接不同数据库的情况，你需要包装现有的模块接口，从而使之适配数据库 —— 好比你手机使用转接口来适配插座那样；

__装饰模式__ 不一样，仅仅包装现有的模块，使之 “更加华丽” ，并不会影响原有接口的功能 —— 好比你给手机添加一个外壳罢了，并不影响手机原有的通话、充电等功能；

---

更多区别参见： [设计模式——装饰模式（Decorator）](https://blog.csdn.net/zhshulin/article/details/38665187)

<!-- slide-7 -->
<slide class="black" image="http://imgsrc.baidu.com/forum/w%3D580/sign=f37267146e2762d0803ea4b790ed0849/bd85c8f9d72a60597fb3392d2534349b023bbaf5.jpg .light">

!![](https://image-static.segmentfault.com/173/954/173954262-59537dde6a914_articlex .size-40.alignleft)

以钢铁侠为例，钢铁侠本质是一个人，只是“装饰”了很多武器方才变得那么 NB，不过再怎么装饰他还是一个人{.white}

<note>
而装饰器就是实现装饰模式的一个方案
</note>

<!-- slide-8 -->
<slide class="bg-black-blue" image="https://source.unsplash.com/n9WPPWiPPJw/">

Decorators make it possible to annotate and modify classes and properties at design time.{.text-intro}

A decorator is\: {.tobuild.pulse}

- an expression {.jello}
- that evaluates to a function {.flipInX}
- that takes the target, name, and decorator descriptor as arguments {.fadeInLeft}
- and optionally returns a decorator descriptor to install on the target object {.lightSpeedIn}
{.description.build.ml5percentage}

<note class="black">
装饰器允许你在类和类的属性定义的时候去注释或者修改它  
装饰器是一个作用于函数的表达式  
它接收三个参数 target、 name 和 descriptor  
然后可选性的返回被装饰之后的 descriptor 对象
</note>

<!-- slide-9 -->
<slide :class="slide-top animated zoomIn delay-200 slow" image="https://source.unsplash.com/n9WPPWiPPJw/">

:::header
装饰器decorator依赖于ES5的Object.defineProperty方法{.white.font30.text-shadow.aligncenter}
:::

Object.defineProperty()在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回这个对象。{.white}

```md
Object.defineProperty(obj, prop, descriptor)

  obj：操作的对象
  prop：被定义或者修改的属性名称
  descriptor：将被定义或修改的属性描述符
  返回值：被传递给函数的对象
````

<note>
所做的事情就是  
descriptor 参数  
它其实也是一个对象
</note>

<!-- slide-10 -->
<slide :class="slide-top animated zoomIn delay-200 slow white" image="https://source.unsplash.com/n9WPPWiPPJw/">

:::header
属性描述符：descriptor{.white.font30.text-shadow}
:::

```md
对象中目前存在的属性描述符有2种:

1、数据描述符：描述属性的值和值是否可被赋值运算符改变

2、存取描述符：由getter、setter函数对属性的描述
````

__属性描述符必须是上述两者之一；且不可同时是两者__{.build}

<!-- slide-11 -->
<slide :class="slide-top animated zoomIn delay-200 slow white" image="https://source.unsplash.com/n9WPPWiPPJw/">

属性描述符通用键值（即数据描述符和存取描述符都有的键值）：{.white.zoomIn}

- 1、configurable：configurable特性表示对象的属性是否可以被删除，以及除value和writable特性外的其他特性是否可以被修改。默认值false，即不可改变
- 2、enumerable：定义了当前操作的这个属性是否可以for...in和Object.key()中被枚举。设为true时，该属性才能出现在对象的枚举属性中。默认值false，即不可被枚举
{.white.build.zoomIn}

<!-- slide-12 -->
<slide :class="slide-top animated zoomIn delay-200 slow white" image="https://source.unsplash.com/n9WPPWiPPJw/">

数据描述符特有的键值：{.white.zoomIn}

- 1、value：该属性对应的值，可以是任意有效的javascript值（string，number，object，function等等）。默认值undefined
- 2、writable：当且仅当writable为true时，value才能被赋值运算符改变。默认值false，即不可被改变
{.white.build.zoomIn}

---

:::column {.vertical-align}

```js {.tobuild..fadeInUp}
let o = {};
o.a = 1;
// 等同于 :
Object.defineProperty(o, "a", {
  value: 1,
  writable: true,
  configurable: true,
  enumerable: true
});
```

---

```js {.tobuild..fadeInUp}
// 另一方面，
Object.defineProperty(o, "a", {value: 1});
// 等同于 :
Object.defineProperty(o, "a", {
  value: 1,
  writable: false,
  configurable: false,
  enumerable: false
});
```

:::

<!-- slide-13 -->
<slide :class="slide-top animated zoomIn delay-200 slow white" image="https://source.unsplash.com/n9WPPWiPPJw/">

存取描述符特有的键值：{.white.zoomIn}

- 1、get：一个给属性提供getter的方法，如果没有getter则为undefined。当访问该属性时get方法会执行，方法执行时没有参数传入，但会传入this对象（由于继承关系，此this不一定是定义该属性的对象）
- 2、set：一个给属性提供setter的方法，如果没有setter则为undefined。当属性值修改时set方法会执行，该方法将接收唯一参数，即该属性新的参数值
{.white.build.zoomIn}

---

:::column {.vertical-align}

```js {.tobuild..fadeInUp}
let obj = {}
let num = 30
Object.defineProperty(obj, 'id', {
    configurable: true,
    enumerable: true,
    get: () => num,
    set: (newValue) => {
        num = newValue
    }
})
console.info(obj.id, num) // 30 30
obj.id = 20
console.info(obj.id, num) // 20 20
num = 40
console.info(obj.id, num) // 40 40
```

:::

<!-- slide-14 -->
<slide :class="slide-top animated zoomIn delay-200 slow" image="https://source.unsplash.com/n9WPPWiPPJw/">

:::header
最简单的作用于类的装饰器 {.white.text-shadow}
:::

:::column {.vertical-align}

```js {..fadeInUp..slow}
// 类的装饰器
export const classDecorator = (target) => {
  // 此处的target为类本身
  target.a = true // 给类添加一个静态属性
}
```

---

```js {..fadeInUp..slow}
@classDecorator
export class ClassA {
  constructor() {
    this.a = 1
  }
}
const classA = new ClassA()
const classA = new ClassA()
console.info(`
  ClassA.a: ${ClassA.a},
  classA.a:' ${classA.a}
`) // true, 1
```

:::

<!-- slide-15 -->
<slide :class="slide-top animated" image="https://source.unsplash.com/n9WPPWiPPJw/">

:::header
类的装饰器传参 {.white.text-shadow}
:::

```js {.tobuild..fadeInUp}
// 类的装饰器传参
export const classDecoratorWithParams = (params = 99) => (target) => {
  target.b = params
}
```

---

```js {.tobuild..fadeInUp}
@classDecoratorWithParams(false)
export class ClassB extends ClassA {
  constructor() {
    super()
    this.b = 1
  }

  fun = () => {
    console.info('fun中ClassB.b: ', this.b, ClassB.b) // 1, false
  }
}
console.info('ClassB.a: ', ClassB.a) // true
console.info('ClassB.b: ', ClassB.b) // false
const classB = new ClassB()
console.info('classB.b: ', classB.b) // 1
classB.fun()
```

<!-- slide-16 -->
<slide :class="slide-top animated" image="https://source.unsplash.com/n9WPPWiPPJw/">

:::header
给修饰类添加实例属性 {.white.text-shadow}
:::

```js {.tobuild..fadeInUp}
// 类的装饰器（给类添加实例属性）
export const classDecoratorAddPrototype = prototypeList => (target) => {
  target.prototype = { ...target.prototype, ...prototypeList }
  target.prototype.logger = () => console.info(`${target.name} 被调用`) // target.name即获得类的名
}
```

---

```js {.tobuild..fadeInUp}
@classDecoratorAddPrototype({ fn() { console.info('fnfnfn') } })
export class ClassC {
  constructor() {
    this.a = 1
  }
}
// console.info('ClassC.fn: ', ClassC.fn()) // 报错，fn不在ClassC的静态属性上
const classC = new ClassC()
classC.fn()
classC.logger()
```

<!-- slide-17 -->
<slide :class="slide-top animated zoomIn delay-200 slow white" image="https://source.unsplash.com/n9WPPWiPPJw/">

在redux中我们经常使用react-redux的connect装饰器即为作用于类的装饰器{.white.zoomIn}

```js {.tobuild..fadeInUp}
connect([mapStateToProps], [mapDispatchToProps], [mergeProps], [options])
export default class MyComponent extends React.Component {}

// 相当于
class MyComponent extends React.Component {}
export default connect([mapStateToProps], [mapDispatchToProps], [mergeProps], [options])(MyComponent)
```

__接收一个组件作为输入，输出一个新的组件的组件。__{.build}

<!-- slide-18 -->
<slide :class="slide-top animated white" image="https://source.unsplash.com/n9WPPWiPPJw/">

:::header
react的高级组件是类的装饰器 {.white.text-shadow}
:::

```js {.tobuild..fadeInUp}
export default (params = {}) => WrappedComponent => class HOC extends Component {
  constructor(props) {
    super(props)
    this.state = {
      activeIndex: -1
    }
  }
  validateSubmit() {
    return false
  }
  render() {
    return (
      <div className="wrap">
        <div>
          the same
        </div>
        <WrappedComponent
          activeIndex={this.state.activeIndex}
          validateSubmit={() => this.validateSubmit()}
          ...
        />
      </div>
    )
  }
}
```

```js {.tobuild..fadeInUp}
@HOC({...default})
@inject('someStore')
@observer class Page extends Component {
  handle = async () => {
    if (!this.props.validateSubmit()) return
  }
  render() {
    const { activeIndex } = this.props
    return (
      <div className="footer" onClick={this.handle}>
        activeIndex
      </div>
    )
  }
}
```

<!-- slide-19 -->
<slide :class="slide-top animated white" image="https://source.unsplash.com/n9WPPWiPPJw/">

__作用于类属性、方法的装饰器__{.white.zoomIn.font30}

与装饰类不同，对类属性、方法的装饰本质是操作其描述符{.tobuild}

可以把此时的装饰器理解成是 Object.defineProperty(obj, prop, descriptor) 的语法糖{.tobuild}

<!-- slide-20 -->
<slide :class="slide-top animated white" image="https://source.unsplash.com/n9WPPWiPPJw/">

:::header
类方法的装饰器 {.white.text-shadow}
:::

```js {.tobuild..fadeInUp}
// 方法的装饰器
export const funDecorator = (params = { readonly: true }) => (target, prototypeKey, descriptor) => {
  /*
    此处target为类的原型对象，即方法Class.prototype
   */
  /*
    prototypeKey为要装饰的方法(属性名)
   */
  /*
    descriptor为要修饰的方法(属性名)的描述符，即(默认值为)：
    {
      value: specifiedFunction,
      enumerable: false,
      configurable: true,
      writable: true
    }
   */

  // 实现一个传参的readonly，修改描述符的writable
  descriptor.writable = !params.readonly
  // 返回这个新的描述符
  return descriptor
}

/*
  调用funDecorator(Class.prototype, prototypeKey, descriptor)
  相当于
  Object.defineProperty(Class.prototype, prototypeKey, descriptor)
  */
```

---

```js {.tobuild..fadeInUp}
export class ClassD {
  constructor() {
    this.a = 1
  }

  @funDecorator()
  fun = (tag) => {
    this.a = 2
    console.info(`this.a ${tag}`, this.a)
  }
}
const classD = new ClassD()
classD.fun('first')

// 报错，无法改变classD.fun，因为他的描述符descriptor.writable已经被装饰器修改为false
try {
  classD.fun = (tag) => {
    console.info(`this.a changed ${tag}`)
  }
  classD.fun('sec')
} catch (err) {
  throw new Error(err)
}
```

<note>
假如我们修饰的是实例方法，第一个参数将是原型对象，也就是 Class.prototype。  
假如是这个静态方法，则第一个参数是构造器 constructor。  
装饰器对类的行为的改变，是代码编译时发生的，而不是在运行时  
这意味着，装饰器能在编译阶段运行代码。  
也就是说，装饰器本质就是编译时执行的函数。
</note>

<!-- slide-21 -->
<slide :class="slide-top animated white" image="https://source.unsplash.com/n9WPPWiPPJw/">

:::header
增强类方法的装饰器 {.white.text-shadow}
:::

```js {.tobuild..fadeInUp}
export const funEnhanceDecorator = (params = {}) => (target, prototypeKey, descriptor) => {
  // 默认需要showLoading
  const { showLoading = true } = params
  const oldValue = descriptor.value
  descriptor.value = async function A(...args) {
    try {
      showLoading && console.info('加载中')
      const result = await oldValue.apply(this, args)
      console.info('hide')
      return result
    } catch (err) {
      console.info('hide')
      console.error(err)
      return null
    }
  };
  return descriptor
}
```

---

```js {.tobuild..fadeInUp}
export class ClassE {
  constructor() {
    this.result = {}
  }

  afun = (params) => {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        resolve(params.id)
      }, 2000)
    })
  }

  @funEnhanceDecorator()
  async fun(params = {}) {
    const result = await this.afun(params)
    console.info(result)
  }
}
const classE = new ClassE()
classE.fun({ id: 100 })
```

<!-- slide-22 -->
<slide :class="slide-top animated white" image="https://source.unsplash.com/n9WPPWiPPJw/">

:::header
执行顺序： {.white.text-shadow}
:::

有多个参数装饰器时：从最后一个参数依次向前执行

方法和方法参数中参数装饰器先执行。

类装饰器总是最后执行。

方法和属性装饰器，谁在前面谁先执行。因为参数属于方法一部分，所以参数会一直紧紧挨着方法执行。

<!-- slide-23 -->
<slide :class="slide-top">

:::header
参考文章 {.text-shadow}
:::

[tc39 github](https://github.com/tc39/proposal-decorators)

[Decorator 装饰器 | 淘宝前端团队](https://segmentfault.com/p/1210000009968000/read)

[Decorators in ES7](http://www.liuhaihua.cn/archives/115548.html)

[TypeScript装饰器](https://blog.csdn.net/weixin_33859844/article/details/88281455)

[JS 装饰器，一篇就够](https://segmentfault.com/a/1190000014495089)

<!-- slide-24 -->
<slide :class="aligncenter">

## 谢谢大家 {.animated.tada}
