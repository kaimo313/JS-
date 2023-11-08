## every 使用

every() 方法测试一个数组内的所有元素是否都能通过指定函数的测试。它返回一个布尔值。

- ele：表示数组中的每一个元素
- index：表示数据中元素的索引
- array：表示数组

```html
<script>
    var arr = [1, 3, 5, 7, 8];
    var result = arr.every(function (ele, index, array) {
        console.log("ele----->", ele);
        console.log("index----->", index);
        console.log("array----->", array);
        return ele > 0;
    });
    console.warn("result----->", result);
</script>
```

## 手写 every

```html
<script>
    Array.prototype.kaimoEvery = function (fn) {
        for (let i = 0; i < this.length; i++) {
            // fn 是 kaimoEvery 中传递的参数，是一个函数，this 是 arr
            let res = fn(this[i], i, this);
            if (!res) {
                return false;
            }
        }
        return true;
    };

    var result2 = arr.kaimoEvery(function (ele, index, array) {
        console.log("ele---kaimoEvery-->", ele);
        console.log("index---kaimoEvery-->", index);
        console.log("array---kaimoEvery-->", array);
        return ele > 0;
    });

    console.warn("result2---kaimoEvery-->", result2);
</script>
```
