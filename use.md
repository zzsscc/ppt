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

---

- 属性描述符通用键值（即数据描述符和存取描述符都有的键值）：
- 1、configurable：configurable特性表示对象的属性是否可以被删除，以及除value和writable特性外的其他特性是否可以被修改。默认值false，即不可改变
- 2、enumerable：定义了当前操作的这个属性是否可以for...in和Object.key()中被枚举。设为true时，该属性才能出现在对象的枚举属性中。默认值false，即不可被枚举
{.build.zoomIn}

<!-- slide-5 -->
<slide :class="slide-top animated zoomIn delay-200 slow" image="https://source.unsplash.com/n9WPPWiPPJw/ .anim">

:::header
数据描述符{.white.font30.text-shadow}
:::



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

<!-- slide-n -->
<slide :class="slide-top animated zoomIn delay-200 slow" image="https://source.unsplash.com/n9WPPWiPPJw/ .anim">

:::header
类的装饰器传参 {.white.text-shadow}
:::

:::column {.vertical-align}

```js {..fadeInUp..slow}
// 类的装饰器传参
export const classDecoratorWithParams = (params = 99) => (target) => {
  target.b = params
}
```

---
```js {..fadeInUp..slow}
@classDecoratorWithParams(false)
export class ClassB extends ClassA {
  constructor() {
    super()
    this.b = 1
  }

  fun = () => {
    console.info('fun中ClassB.a: ', this.b, ClassB.b) // 1, false
  }
}
console.info('ClassB.a: ', ClassB.a) // true
console.info('ClassB.b: ', ClassB.b) // false
const classB = new ClassB()
console.info('classB.b: ', classB.b) // 1
classB.fun()
```
:::