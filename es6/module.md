modules是ES6引入的最重要的一个特性

## 基本用法

可以直接在任何变量或者函数前面加上一个 export 关键字，就可以将它导出。

```
  export const sqrt = Math.sqrt;
  export function square(x) {
    return x * x
  }
  export function diag(x,y) {
    return sqrt(square(x) + square(y))
  }
```
然后再另一个文件中这样引用 

```
  import { square, diag } from 'lib';
  console.log(square(11)); // 121
  console.log(diag(4, 3));
```

还可以这样导入

``` 
  import * as lib from 'lib';
  square = lib.square;
```
但是不能这样导入，会报错

```
  import lib from 'lib';
  square = lib.square;
```


### 命令导出结合默认导出

默认导出同样可以结合命令导出来使用：
```
  export default function (obj) {
    ....
  }
  export function each(obj,iterator,context) {
    ...
  }
  export {each as forEach}
```
上面的代码导出一个默认的函数，然后又导出两个命名函数，我们可以这样引入：
```
  import _,{ each } form 'underscore'
```
注意这个逗号语法，分割了默认导出和命名导出


其实这个默认导出只是一个特殊的名字叫 default，你也可以直接使用它的名字，把它当做命名导出来用

```
import { default as foo } form 'lib'
// 等价于上面的引入
import foo from 'lib'
```

### 仅支持静态导入导出

ES6规范支持静态的导入导出，也就是必须要在编译时就能确定，在运行时才能确定是不行的，比如下面的代码就是不对的

```
  // 动态导入
  var mylib;
  if(Math.random()) {
    mylib = require('foo')
  } else {
    mylib = require('bar')
  }
  // 动态导出 
  if(Math.random()){
    exports.baz = ...;
  }
```
原因：
 * 性能，在编译阶段完成所有模块的导入，如果再运行时进行会降低速度
 * 更好的检查错误，比如对变量类型的检查

### 各种导入和导出方式总结

如下几种导出方式

```
// export 命令导出
  export var myVar1 = ...;
  export let myVar2 = ...;
  export const MY_CONST = ...;

  export function myFunc() {
      ...
  }
  export function* myGeneratorFunc() {
      ...
  }
  export class MyClass {
      ...
  }
// export default 默认导出
  export default 123;
  export default function (x) {
      return x
  };
  export default x => x;
  export default class {
      constructor(x, y) {
          this.x = x;
          this.y = y;
      }
  };

  //也可以自己列出所有导出内容
  const MY_CONST = ...;
  function myFunc() {
      ...
  }

  export { MY_CONST, myFunc };

  //或者在导出的时候给他们改个名字
  export { MY_CONST as THE_CONST, myFunc as theFunc };

  //还可以导出从其他地方导入的模块
  export * from 'src/other_module';
  export { foo, bar } from 'src/other_module';
  export { foo as myFoo, bar } from 'src/other_module';
···


导入方式

```
  // Default exports and named exports
  import theDefault, { named1, named2 } from 'src/mylib';
  import theDefault from 'src/mylib';
  import { named1, named2 } from 'src/mylib';

  // Renaming: import named1 as myNamed1
  import { named1 as myNamed1, named2 } from 'src/mylib';

  // Importing the module as an object
  // (with one property per named export)
  import * as mylib from 'src/mylib';

  // Only load the module, don’t import anything
  import 'src/mylib';
```

