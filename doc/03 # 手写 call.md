## call 干了什么？

1. 改变 this 指向
2. 让函数执行

```html
<script>
    function fn(num1, num2) {
        console.log("this----->", this);
        return num1 + num2;
    }

    let obj = {
        name: "kaimo313"
    };

    let res = fn.call(obj, 1, 2);
    console.log("res----->", res);
</script>
```

## 手写 call

```html
<script>
    Function.prototype.kaimoCall = function (content) {
        // 没有东西指向 window，将 content 包装成对象
        content = content ? Object(content) : window;
        // 执行 this() 改变不了 this 指向，需要赋值给属性
        content.f = this;
        // 收集参数
        let args = [];
        for (let i = 1; i < arguments.length; i++) {
            args.push(arguments[i]);
        }
        let res = content.f(...args);
        // 再删除多余的 f 参数
        delete content.f;
        return res;
    };

    function fn(num1, num2) {
        console.log("this----->", this);
        return num1 + num2;
    }

    let obj = {
        name: "kaimo313"
    };

    let res = fn.call(obj, 1, 2);
    console.log("res----->", res);

    let res2 = fn.kaimoCall(obj, 1, 2);
    console.log("res2----->", res2);
</script>
```