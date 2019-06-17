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

<slide class="bg-black-blue aligncenter" image="https://source.unsplash.com/C1HhAQrbykQ/ .dark">

# test {.text-landing.text-shadow}

By zsc {.text-intro}

[:fa-github: Github](https://github.com/zzsscc/decorators){.button.ghost.animated.flipInX.delay-1200}

<!-- slide-2 -->
<slide class="bg-black-blue" image="https://source.unsplash.com/n9WPPWiPPJw/">

Decorators make it possible to annotate and modify classes and properties at design time.{.text-intro}

A decorator is\: {.tobuild.pulse}

- an expression {.jello}
- that evaluates to a function {.flipInX}
- that takes the target, name, and decorator descriptor as arguments {.fadeInLeft}
- and optionally returns a decorator descriptor to install on the target object {.lightSpeedIn}
{.description.build.ml5percentage}

---
装饰器允许你在类和类的属性定义的时候去注释或者修改它。装饰器是一个作用于函数的表达式，它接收三个参数 target、 name 和 descriptor ， 然后可选性的返回被装饰之后的 descriptor 对象。 {.aligncenter}

<!-- slide-3 -->
<slide :class="slide-top animated zoomIn delay-200 slow" image="https://source.unsplash.com/n9WPPWiPPJw/ .anim">

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

<!-- slide-4 -->
<slide :class="slide-top animated zoomIn delay-200 slow white" image="https://source.unsplash.com/n9WPPWiPPJw/ .anim">

:::header
属性描述符：descriptor{.white.font30.text-shadow}
:::

```md
对象中目前存在的属性描述符有2种:

1、数据描述符：描述属性的值和值是否可被赋值运算符改变

2、存取描述符：由getter、setter函数对属性的描述
````

__属性描述符必须是上述两者之一；且不可同时是两者__{.build}

<!-- slide-5 -->
<slide :class="slide-top animated zoomIn delay-200 slow white" image="https://source.unsplash.com/n9WPPWiPPJw/ .anim">

属性描述符通用键值（即数据描述符和存取描述符都有的键值）：{.white.zoomIn}

- 1、configurable：configurable特性表示对象的属性是否可以被删除，以及除value和writable特性外的其他特性是否可以被修改。默认值false，即不可改变
- 2、enumerable：定义了当前操作的这个属性是否可以for...in和Object.key()中被枚举。设为true时，该属性才能出现在对象的枚举属性中。默认值false，即不可被枚举
{.white.build.zoomIn}

<!-- slide-6 -->
<slide :class="slide-top animated zoomIn delay-200 slow white" image="https://source.unsplash.com/n9WPPWiPPJw/ .anim">

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

<!-- slide-7 -->
<slide :class="slide-top animated zoomIn delay-200 slow white" image="https://source.unsplash.com/n9WPPWiPPJw/ .anim">

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

<!-- slide-8 -->
<slide :class="slide-top animated zoomIn delay-200 slow" image="https://source.unsplash.com/n9WPPWiPPJw/ .anim">

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

<!-- slide-9 -->
<slide :class="slide-top animated" image="https://source.unsplash.com/n9WPPWiPPJw/ .anim">

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

<!-- slide-10 -->
<slide :class="slide-top animated" image="https://source.unsplash.com/n9WPPWiPPJw/ .anim">

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

<!-- slide-11 -->
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

<!-- slide-12 -->
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

<!-- slide-13 -->
<slide :class="slide-top animated white" image="https://source.unsplash.com/n9WPPWiPPJw/">

__作用于类方法的装饰器__{.white.zoomIn.font30}

与装饰类不同，对类方法的装饰本质是操作其描述符{.tobuild}

可以把此时的装饰器理解成是 Object.defineProperty(obj, prop, descriptor) 的语法糖{.tobuild}

<!-- slide-14 -->
<slide :class="slide-top animated white" image="https://source.unsplash.com/n9WPPWiPPJw/">

:::header
类方法的装饰器 {.white.text-shadow}
:::

```js {.tobuild..fadeInUp}
// 方法的装饰器
export const funDecorator = (params = { readonly: true }) => (target, prototypeKey, descriptor) => {
  /*
    此处target为类的原型对象，即方法Class.prototype
    ps：装饰器的本意是要装饰类的实例，但此时实例还未生成，所以只能装饰类的原型
    装饰器对类的行为的改变，是代码编译时发生的，而不是在运行时。这意味着，装饰器能在编译阶段运行代码。
    也就是说，装饰器本质就是编译时执行的函数。
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

<!-- slide-15 -->
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
