1.T extends () => infer R中的infer作用是什么

```
使用条件类型来检查 T 是否是一个函数类型时，我们可以使用 T extends () => infer R 这样的形式。这表示我们希望 TypeScript 推断函数类型 T 的返回类型，并将其赋值给 R。这样，我们就可以在条件类型中使用类型变量 R。
```

2.下面代码中type的作用是什么：import type { RawSymbol, Ref, UnwrapRefSimple } from './ref'

```
type 关键字用于导入类型声明而不导入实际的 JavaScript 对象。这被称为类型导入或仅类型导入。

使用 import type 语法时，它只会导入类型信息，而不会导入与类型相关的实际运行时代码。这意味着在导入类型之后，导入的模块将不会在编译后的 JavaScript 代码中产生任何实际的导入语句或运行时代码。

类型导入的一个常见用例是在编译时进行静态类型检查和类型推断，而不需要在运行时加载模块或执行相关的代码。这对于优化构建大小和性能非常有用。

import type { RawSymbol, Ref, UnwrapRefSimple } from './ref' 语句导入了模块 ./ref 中定义的类型 RawSymbol、Ref 和 UnwrapRefSimple。这意味着在编译时，这些类型将可用于进行类型检查、类型推断和类型注解等操作，但实际的 JavaScript 对象或模块代码将不会被导入或执行。
```

3.only unwrap nested ref

是解脱嵌套的引用，nested在计算机中是嵌套的意思

4.