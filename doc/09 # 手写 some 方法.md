## some 使用

some() 方法测试数组中是否至少有一个元素通过了由提供的函数实现的测试。如果在数组中找到一个元素使得提供的函数返回 true，则返回 true；否则返回 false。它不会修改数组。

- ele：表示数组中的每一个元素
- index：表示数据中元素的索引
- array：表示数组

```html
<script>
    var arr = [1, 3, 5, 7, 8];
    var result = arr.some(function (ele, index, array) {
        console.log("ele----->", ele);
        console.log("index----->", index);
        console.log("array----->", array);
        return ele > 8;
    });
    console.warn("result----->", result);
</script>
```

## 手写 some

```html
<script>
    Array.prototype.kaimoSome = function (fn) {
        for (let i = 0; i < this.length; i++) {
            // fn 是 kaimoSome 中传递的参数，是一个函数，this 是 arr
            let res = fn(this[i], i, this);
            if (res) {
                return true;
            }
        }
        return false;
    };

    var result2 = arr.kaimoSome(function (ele, index, array) {
        console.log("ele---kaimoSome-->", ele);
        console.log("index---kaimoSome-->", index);
        console.log("array---kaimoSome-->", array);
        return ele > 8;
    });

    console.warn("result2---kaimoSome-->", result2);
</script>
```
