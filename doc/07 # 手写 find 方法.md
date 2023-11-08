## find 的使用

`find()` 方法返回数组中满足提供的测试函数的第一个元素的值。否则返回 `undefined`。

- ele：表示数组中的每一个元素
- index：表示数据中元素的索引
- array：表示数组

```html
<script>
    var arr = [1, 3, 5, 7, 9];
    var result = arr.find(function (ele, index, array) {
        console.log("ele----->", ele);
        console.log("index----->", index);
        console.log("array----->", array);
        return ele > 6;
    });
    console.warn("result----->", result);
</script>
```


## 手写实现 find 方法

```html
<script>
    Array.prototype.kaimoFind = function (fn) {
        for (let i = 0; i < this.length; i++) {
            // fn 是 kaimoFind 中传递的参数，是一个函数，this 是 arr
            let res = fn(this[i], i, this);
            if (res) {
                return this[i];
            }
        }
    };

    var result2 = arr.kaimoFind(function (ele, index, array) {
        console.log("ele---kaimoFind-->", ele);
        console.log("index---kaimoFind-->", index);
        console.log("array---kaimoFind-->", array);
        return ele > 6;
    });

    console.warn("result2---kaimoFind-->", result2);
</script>
```
