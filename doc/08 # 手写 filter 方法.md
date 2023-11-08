## 什么是 filter

filter() 方法创建给定数组一部分的浅拷贝，其包含通过所提供函数实现的测试的所有元素。如果没有元素通过测试，则返回一个空数组。

- ele：表示数组中的每一个元素
- index：表示数据中元素的索引
- array：表示数组

```html
<script>
    var arr = [1, 3, 5, 7, 9];
    var result = arr.filter(function (ele, index, array) {
        console.log("ele----->", ele);
        console.log("index----->", index);
        console.log("array----->", array);
        return ele > 6;
    });
    console.warn("result----->", result);
</script>
```

## 手写 filter

```html
<script>
    var arr = [1, 3, 5, 7, 9];
    var result = arr.filter(function (ele, index, array) {
        console.log("ele----->", ele);
        console.log("index----->", index);
        console.log("array----->", array);
        return ele > 6;
    });
    console.warn("result----->", result);

    Array.prototype.kaimoFilter = function (fn) {
        let arr = [];
        for (let i = 0; i < this.length; i++) {
            // fn 是 kaimoFilter 中传递的参数，是一个函数，this 是 arr
            let res = fn(this[i], i, this);
            if (res) {
                arr.push(this[i]);
            }
        }
        return arr;
    };

    var result2 = arr.kaimoFilter(function (ele, index, array) {
        console.log("ele---kaimoFilter-->", ele);
        console.log("index---kaimoFilter-->", index);
        console.log("array---kaimoFilter-->", array);
        return ele > 6;
    });

    console.warn("result2---kaimoFilter-->", result2);
</script>
```