---
layout: cover
highlighter: shiki
css: unocss
colorSchema: dark
transition: fade-out
growSize: 1.5
---
<img class="w-60 absolute top-10 left-10" src="/type-challenges-logo.svg" />

# 一起来做 <span text="#8b5cf6" fw-800 class="font-brush">TS</span> 类型体操

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    开始学习 <carbon:arrow-right class="inline animate-fade-out-right animate-count-infinite animate-duration-1.5s"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
</div>

---
transition: fade-out
layout: intro
growX: 10
growY: 90
style: 'padding-left: 8rem;'
---

# 目录

- 🎨 **背景** - 类型体操的背景，通过背景了解为什么要在项目中加入类型体操
- 📝 **套路** - 了解类型体操的运算逻辑、和类型套路
- 🧑‍💻 **实践** - 类型体操实践，解析 Typescript 内置高级类型
- 🏆 **其他** - 常用工具网站和其他

---
layout: center
growX: 50
growY: 120
growSize: 1.5
---

# 背景

<div class="number-bg">1</div>

- 什么是类型安全？
- 怎么实现类型安全？
- 什么是类型体操？

---
layout: center
growX: -10
growY: 50
growSize: 0.75
---

### 👷 什么是类型安全
<br>

<v-clicks>

- 一个简单的定义就是，类型安全就是只做该类型允许的操作。比如对于 boolean 类型，不允许加减乘除运算，只允许赋值 true、false。
> 当我们能做到类型安全时，可以大量的减少代码中潜在的问题，大量提高代码质量。
</v-clicks>

---
layout: center
growX: 100
growY: 80
growSize: 1.5
---

### 🔧 怎么实现类型安全 
> 这里介绍两种类型检查机制，分别是动态类型检查和静态类型检查。

<div flex="~ gap-6">
<div v-click="1" class="rounded-8px mt-8 slidev-content">

#### 动态类型检查

- Javascript 就是典型的动态类型检查，它在编译时，没有类型信息，到运行时才检查，导致很多隐藏 bug。

</div>

<div v-click="2" class="rounded-8px mt-8 slidev-content">

#### 静态类型检查

- Typescript 作为 Javascript 的超集，采用的是静态类型检查，在编译时就有类型信息，检查类型问题，减少运行时的潜在问题。

</div>
</div>

---
layout: center
growX: -10
growY: -10
class: text-center
---

<img class="w-100 block mx-auto" src="/type-safe.svg" />

---
layout: center
growX: 50
growY: 0
---

### 🤸 什么是类型体操?
<v-click>

> 就是类型编程，对类型参数做各种逻辑运算，以产生新的类型
</v-click>

<div  grid="~ cols-2 gap-4" mt-6>
<div v-click>

#### 简单的类型系统
>只基于声明的类型做类型检查

```ts
// number
function add(a: number, b: number) {
  return a + b
}

// string
function add(a: string, b: string) {
  return a + b
}
```

</div>
<div v-click>

#### 泛型类型系统
> 支持类型参数，通过给参数传参，可以动态定义类型，让类型更加灵活。

```ts
function add<T>(a: T, b: T) {
  return a + b
}

add(1, 2) // 3
add('Hello', ' world') // 'Hello world'
```

</div>
</div>

<v-clicks>

```ts
function getPropValue<T>(obj: T, key) {
  return obj[key]
}
```

</v-clicks>

---
layout: center
growX: 50
growY: -50
growSize: 1.5
---

```ts
function getPropValue<T extends Object, K extends keyof T>(
  obj: T,
  key: K
): T[K] {
  return obj[key]
}
```

---
transition: fade-out
layout: center
growX: 10
growY: 90
style: 'padding-left: 8rem;'
---

# 套路

- 9 种运算逻辑
- 4 个类型套路

<div class="number-bg">2</div>

---
layout: center
growX: 50
growY: 120
growSize: 1.5
---

## 9种运算逻辑

<div grid="~ cols-2 gap-4" m="-t-2">
<div>01. 条件：<span class="text-light-blue-400">T extends U ? X : Y</span></div>
<div>02. 约束：<span class="text-light-blue-400">extends</span></div>
<div>03. 推导：<span class="text-light-blue-400">infer</span></div>
<div>04. 联合：<span class="text-light-blue-400">｜</span></div>
<div>05. 交叉：<span class="text-light-blue-400">&</span></div>
<div>06. 索引查询：<span class="text-light-blue-400">keyof</span></div>
<div>08. 索引访问：<span class="text-light-blue-400">T[K]</span></div>
<div>09. 索引遍历：<span class="text-light-blue-400">in</span></div>
<div>09. 重映射：<span class="text-light-blue-400">as</span></div>
</div>

---
layout: center
---

#### 条件：T extends U ? X : Y
> 条件判断和 js 逻辑相同，都是如果满足条件就返回 x 否则返回 y。

```ts
// 如果 T 是 2 的子类型，那么类型是 true，否则类型是 false。
type isTwo<T> = T extends 2 ? true : false
type res = isTwo<1> // false
```

---
layout: center
growX: -30
growY: 50
growSize: 1.5
---

#### 约束：extends

```ts {all|1|all}
function getPropValue<T extends Object, K extends keyof T>(
  obj: T,
  key: K
): T[K] {
  return obj[key]
}
```

```ts {0|6|all}
// 通过 T extends Length 约束了 T 的类型，必须是包含 length 属性，且 length 的类型必须是 number。
interface Length {
  length: number
}

function fn1<T extends Length>(arg: T): number {
  return arg.length
}
```

---
layout: center
growX: 110
growY: -10
---

#### 推导：infer
> 类似 js 的正则匹配，都满足公式条件时，可以提取公式中的变量，直接返回或者再次加工都可以。

```ts
// 提取元组类型的第一个元素：
// extends 约束类型参数只能是数组类型，因为不知道数组元素的具体类型，所以用 unknown。
// extends 判断类型参数 T 是不是 [infer F, ...infer R] 的子类型，如果是就返回 F 变量，如果不是就不返回
type First<T extends unknown[]> = T extends [infer F, ...infer R] ? F : never
type res2 = First<[1, 2, 3]> // 1
```

---
layout: center
growX: 90
growY: 90
growSize: 1.5
---

#### 联合： ｜

```ts
type Union = 1 | 2 | 3
```

<br>

#### 交叉： &

```ts
// 交叉代表对类型做合并
type ObjType = { a: number } & { c: boolean }
```

---
layout: center
---

#### 索引查询：keyof T
> 用于获取某种类型的所有键，其返回值是联合类型

```ts
type k = keyof {
  name: string
  age: number
} // 'name' | 'age'
```

---
layout: center
growX: 50
growY: 100
growSize: 1.1
---

#### 索引访问：T[K]
> 用于访问索引，得到索引对应的值的联合类型。

```ts
// 对象类型
interface obj {
  name: string
  age: number
}

type value = obj[keyof obj] // string | number

// 数组类型
type arr = [string, number]
type value2 = arr[1] // number
type value3 = arr[number] // string | number
```

---
layout: center
growX: 110
growY: 110
---

#### 索引遍历：in
> 用于遍历联合类型

```ts
const obj = {
  name: 'hyden',
  age: 18,
}

type T5 = {
  [P in keyof typeof obj]: any // [P in 'name' | 'age']: any
}

/*
{
  name: any
  age: any
}
*/
```

---
layout: center
growX: 50
growY: 160
growSize: 1.5
---

#### 重映射： as
> 用于修改类型

<div flex gap-4>
<div v-click>

```ts
// 通过索引查询 keyof，索引访问 T[k]，索引遍历 in，重映射 as，返回全新的 key、value 构成的新的映射类型
type MapType<T> = {
  [Key in keyof T as `${Key & string}${Key & string}${Key & string}`]: [
    T[Key],
    T[Key],
    T[Key]
  ]
}

type res = MapType<{ a: number; b: string }>
/**
 * {
 *   aaa: [number, number, number]
 *   bbb: [string, string, string]
 * }
 */
```

</div>

<div v-click>

```ts
const obj = {
  name: 'hyden',
  age: 18,
} as const

/**
 * {
 *  readonly name: "hyden";
 *  readonly age: 18;
 * }
 */
```

</div>
</div>

---
layout: center
---

## 4个运算套路

- 模式匹配做提取
- 重新构造做变换
- 递归复用做循环
- 数组长度做计数

---
layout: intro
growX: 10
growY: 90
style: 'padding-left: 8rem;'
---

#### 模式匹配做提取

```ts
// 1、
type mid<T extends string> = T extends `${infer L}${infer M}${infer R}` ? M : ''

type m = mid<'abc'> // b
```

<br>

<div v-click>

```ts
// 2、
type GetParameters<Func extends Function> = Func extends (
  ...args: infer Args
) => unknown
  ? Args
  : never

type ParametersResult = GetParameters<(name: string, age: number) => string>
```

</div>

---
layout: center
growX: 50
growY: 120
---

#### 重新构造做变换
> 想要变化就需要重新构造新的类型，并且可以在构造新类型的过程中对原类型做一些过滤和变换

```ts
// 类型首字母大写
type CapitalizeStr<Str extends string> =
  Str extends `${infer First}${infer Rest}` ? `${Uppercase<First>}${Rest}` : Str

type CapitalizeResult = CapitalizeStr<'hyden'> // Hyden
```

---
layout: intro
growX: 10
growY: 90
style: 'padding-left: 8rem;'
---

#### 递归复用做循环
> TS 类型编程本身不支持循环，但是可以通过递归完成不确定数量的类型编程，达到循环的效果

```ts
// 1、数组类型
type ReverseArr<Arr extends unknown[]> = Arr extends [
  infer First,
  ...infer Rest
]
  ? [...ReverseArr<Rest>, First]
  : Arr

type ReverseArrResult = ReverseArr<[1, 2, 3, 4, 5]> // [5, 4, 3, 2, 1]
```

```ts
// 2、字符串类型
type ReverseStr<Str extends string> = Str extends `${infer First}${infer Rest}`
  ? `${ReverseStr<Rest>}${First}`
  : Str

type ReverseStrResult = ReverseStr<'hyden'> // nedyh
```

---
layout: quote
---

#### 数组长度做计数
> TS 类型编程本身也是不支持做加减乘除运算的，但是可以通过递归构造指定长度的数组，然后取数组长度的方式来完成数值的加减乘除。

```ts
// 构建指定长度的数组
type BuildArray<
  Length extends number,
  Un = unknown,
  Arr extends unknown[] = []
> = Arr['length'] extends Length ? Arr : BuildArray<Length, Un, [...Arr, Un]>

// 数组长度做加法
type Add<Num1 extends number, Num2 extends number> = [
  ...BuildArray<Num1>,
  ...BuildArray<Num2>
]['length']

// res: 5
type AddResult = Add<2, 3> // 5
```

---
layout: center
growX: 50
growY: 120
growSize: 1.5
---

# 类型体操实践
- 实现一些 TS 内置高级类型
- 实现一些常用的类型工具

<div class="number-bg">3</div>

---

## 实现一些 TS 内置高级类型

- partial 把索引变为可选

```ts
type TPartial<T> = {
  [P in keyof T]?: T[P]
}

type PartialRes = TPartial<{ name: 'hyden'; age: 18 }>
```

<br>

- Required 把索引变为必选

```ts
type TRequired<T> = {
  [P in keyof T]-?: T[P]
}

type RequiredRes = TRequired<{ name?: 'hyden'; age?: 18 }>
```

---
growX: -10
growY: 50
growSize: 0.75
---

- Readonly 把索引变为只读

```ts
type TReadonly<T> = {
  readonly [P in keyof T]: T[P]
}

type ReadonlyRes = TReadonly<{ name?: 'hyden'; age?: 18 }>
```

<br>

- Pick 保留过滤索引

```ts
type TPick<T, K extends keyof T> = {
  [P in K]: T[P]
}

type PickRes = TPick<{ name: 'hyden'; age: 18 }, 'name'>
```

---
growX: 50
growY: -40
growSize: 1.5
---

- Record 创建映射类型

```ts
type TRecord<K extends keyof any, T> = {
  [P in K]: T
}

type RecordRes = TRecord<'hello' | 'world', string>
```

<br>

- Exclude 删除联合类型的一部分

```ts
type TExclude<T, U> = T extends U ? never : T

type ExcludeRes = TExclude<'aa' | 'bb' | 'cc', 'aa'>
```

More: [Utility Types](https://www.typescriptlang.org/docs/handbook/utility-types.html)

---
layout: center
growX: -10
growY: -10
---

## 一些工具方法 [^1]

- 判断两个类型是否相等

```ts
type Equal<X, Y> = (<T>() => T extends X ? 1 : 2)
  extends <T>() => T extends Y ? 1 : 2
  ? true
  : false
```

- 判断是否是 any [^2]

```ts
type isAny<T> = 0 extends 1 & T ? true : false
```

[^1]: [More](https://github.com/type-challenges/type-challenges)
[^2]: [Link](https://stackoverflow.com/questions/49927523/disallow-call-with-any/49928360#49928360)


---
layout: center
growX: 50
growY: 0
---

# 其他

- TS 内置高级类型：[Utility Types](https://www.typescriptlang.org/docs/handbook/utility-types.html)
- TS 类型体操练习 [Type Challenges](https://github.com/type-challenges/type-challenges)
- TS 类型的工具库 [Zod](https://zod.dev/)
- TS 在线编译器 [TS Playground](https://www.typescriptlang.org/play)

---
layout: intro
class: text-center pb-5
growX: 50
growY: 120
---

# Thank You!

Slides on 东方
