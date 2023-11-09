## reduce 使用

reduce() 方法对数组中的每个元素按序执行一个提供的 reducer 函数，每一次运行 reducer 会将先前元素的计算结果作为参数传入，最后将其结果汇总为单个返回值。

第一次执行回调函数时，不存在“上一次的计算结果”。如果需要回调函数从数组索引为 0 的元素开始执行，则需要传递初始值。否则，数组索引为 0 的元素将被用作初始值，迭代器将从第二个元素开始执行（即从索引为 1 而不是 0 的位置开始）。

- callbackfn 函数
    - accumulator：上一次调用 `callbackFn` 的结果。在第一次调用时，如果指定了 initialValue 则为指定的值，否则为 `array[0]` 的值。
    - currentValue：当前元素的值。在第一次调用时，如果指定了 initialValue，则为 `array[0]` 的值，否则为 `array[1]`。
    - currentIndex：currentValue 在数组中的索引位置。在第一次调用时，如果指定了 initialValue 则为 0，否则为 1。
    - array：调用了 `reduce()` 的数组本身。
- initialValue（可选）：第一次调用回调时初始化 accumulator 的值。如果指定了 initialValue，则 callbackFn 从数组中的第一个值作为 currentValue 开始执行。如果没有指定 initialValue，则 accumulator 初始化为数组中的第一个值，并且 callbackFn 从数组中的第二个值作为 currentValue 开始执行。在这种情况下，如果数组为空（没有第一个值可以作为 accumulator 返回），则会抛出错误（`Uncaught TypeError: Reduce of empty array with no initial value`）。

```html
<script>
    var arr = [1, 2, 3, 4];
    var result = arr.reduce(function (accumulator, currentValue, currentIndex, array) {
        console.log("accumulator----->", accumulator);
        console.log("currentValue----->", currentValue);
        console.log("currentIndex----->", currentIndex);
        console.log("array----->", array);
        return accumulator + currentValue;
    }, -3);
    console.warn("result----->", result);
</script>

```

## 手写 reduce

```html
<script>
    Array.prototype.kaimoReduce = function (callbackfn, initialValue) {
        let hasInitialValue = initialValue !== undefined;
        if (this.length === 0) {
            if (hasInitialValue) {
                return initialValue;
            } else {
                throw TypeError("Reduce of empty array with no initial value");
            }
        }
        let accumulator = hasInitialValue ? initialValue : this[0];
        let i = hasInitialValue ? 0 : 1;
        for (i; i < this.length; i++) {
            accumulator = callbackfn(accumulator, this[i], i, this);
        }
        return accumulator;
    };

    var result2 = arr.kaimoReduce(function (accumulator, currentValue, currentIndex, array) {
        console.log("accumulator---kaimoReduce-->", accumulator);
        console.log("currentValue---kaimoReduce-->", currentValue);
        console.log("currentIndex---kaimoReduce-->", currentIndex);
        console.log("array---kaimoReduce-->", array);
        return accumulator + currentValue;
    }, -3);

    console.warn("result2---kaimoReduce-->", result2);
</script>
```