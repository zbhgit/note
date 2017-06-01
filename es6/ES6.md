## ES6 学习

### let 与 const 

> 使用let声明变量注意事项

1. 其生命的变量只在其所在的代码块有效 


```
  {
    let a = 1;
    var b = 2;
  }
  console.log(a);
  console.log(b);
```

2. 使用let声明的变量在预解析的时候不会被提升

```
  console.log(a);
  var a = 1;

  console.log(b);
  let b = 2;

```

3. 使用let时的暂时性死区

```
  let d = 3;
  function fn() {
    d = 10;
    let d = 2; 
  }
  fn();
```

4. 再循环语句之内是一个父作用域，再循环体内是一个子作用域；

> const 注意情况

1.



## 数据结构  map