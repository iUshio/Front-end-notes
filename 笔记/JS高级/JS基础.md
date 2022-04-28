# JS基础

> **数据类型：**
> >**基本（值）类型：**

```js
    1.  String：任意字符串
    2.  Number：任意的数字
    3.  Boolean：true/false
    4.  undefined:undefined
    5.  null:null
```
> >
> > **对象（引用）类型：**

```js
    1. Object：任意对象
    2. Function：一种特殊的对象（可以执行）
    3. Array：一种特殊的对象（数值下标）
```

---
> **判断数据类型：**
> > `typeof`

```js
    typeof返回数据类型的字符串表达
    不能判断null(返回Object)，Array（返回Object）
```

> > `instanceof`

```js
    判断对象的具体类型（无法判断undefined）
```

> > `===`

```js
    可以判断undefined，null
```

---
> **IIFE：**
立即调用函数（Immediately-Involked Function Expression）:
>
> 作用：隐藏实现不会污染外部（全局）命名空间，举例：

```js
    <script>
    (function(){
        var a = 4
        console.log(a+3)
    })()
    var a = 4
    console.log(a)
    </script>
```

---
