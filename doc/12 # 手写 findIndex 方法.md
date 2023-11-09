## findIndex 的使用

findIndex() 方法返回数组中满足提供的测试函数的第一个元素的索引。若没有找到对应元素则返回 -1。

```html
<script>
    var arr = [1, 3, 5, 7, 8];
    var result = arr.findIndex(function (ele, index, array) {
        console.log("ele----->", ele);
        console.log("index----->", index);
        console.log("array----->", array);
        return ele > 5;
    });
    console.warn("result----->", result);
</script>

```

## 手写 findIndex

```html
<script>
    Array.prototype.kaimoFindIndex = function (fn) {
        for (let i = 0; i < this.length; i++) {
            // fn 是 kaimoFindIndex 中传递的参数，是一个函数，this 是 arr
            let res = fn(this[i], i, this);
            if (res) {
                return i;
            }
        }
        return -1;
    };

    var result2 = arr.kaimoFindIndex(function (ele, index, array) {
        console.log("ele---kaimoFindIndex-->", ele);
        console.log("index---kaimoFindIndex-->", index);
        console.log("array---kaimoFindIndex-->", array);
        return ele > 5;
    });

    console.warn("result2---kaimoFindIndex-->", result2);
</script>

```