## bind 干了什么？

1. 改变 this 指向
2. 没有让函数执行，返回一个改变 this 指向后的函数

bind 难点在于参数的收集

## 手写 bind

简单实现如下：

```html
<script>
    Function.prototype.kaimoBind = function (content) {
        // 获取到 bind 里的剩余参数
        let bindArgs = Array.prototype.slice.call(arguments, 1);
        console.log("bindArgs----->", bindArgs);
        // 这里的 this 指向调用 kaimoBind 的 fn
        let that = this;
        function gn() {
            // 拿到 bind 返回函数的参数
            let gnArgs = Array.prototype.slice.call(arguments);
            console.log("gnArgs----->", gnArgs);
            // 改变 fn 的 this 指向
            return that.apply(content, bindArgs.concat(gnArgs));
        }
        return gn;
    };

    function fn(...args) {
        console.log("fn----this----->", this);
        console.log("fn----args----->", args);
        return args.join("");
    }

    let obj = {
        name: "kaimo313"
    };

    let res = fn.bind(obj, "k", "a", "i", "m", "o");
    console.log("res---bind-->", res(3, 1, 3));

    let res2 = fn.kaimoBind(obj, "k", "a", "i", "m", "o");
    console.log("res2---kaimoBind-->", res2(3, 1, 3));
</script>

```

复杂一点实现如下：

```html
<script>
    Function.prototype.kaimoBind = function (content) {
        // 获取到 bind 里的剩余参数
        let bindArgs = Array.prototype.slice.call(arguments, 1);
        console.log("bindArgs----->", bindArgs);
        // 这里的 this 指向调用 kaimoBind 的 fn
        let that = this;
        function gn() {
            // 拿到 bind 返回函数的参数
            let gnArgs = Array.prototype.slice.call(arguments);
            console.log("gnArgs----->", gnArgs);
            // 改变 fn 的 this 指向
            return that.apply(content, bindArgs.concat(gnArgs));
        }
        function Mn() {}
        Mn.prototype = this.prototype;
        // gn 继承 Mn
        gn.prototype = new Mn();
        return gn;
    };

    function fn(...args) {
        console.log("fn----this----->", this);
        console.log("fn----args----->", args);
        return args.join("");
    }

    fn.prototype.kaimo = 313;

    let obj = {
        name: "kaimo313"
    };

    let res = fn.bind(obj, "k", "a", "i", "m", "o");
    console.log("res---bind-->", res(3, 1, 3));

    let res2 = fn.kaimoBind(obj, "k", "a", "i", "m", "o");
    console.log("res2---kaimoBind-->", res2(3, 1, 3));

    let res3 = new res2();
    console.log("res3----->", res3.kaimo);
</script>
```