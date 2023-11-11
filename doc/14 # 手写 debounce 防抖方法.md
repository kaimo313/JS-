## 什么是防抖

防抖: n 秒后再去执行该事件，若在 n 秒内被重复触发，则重新计时，这个效果跟英雄联盟里的回城技能差不多。

本质上是优化高频率执行代码的一种手段，目的就是降低回调执行频率、节省计算资源。

应用场景：

- 搜索框搜索输入，手机号、邮箱等验证输入检测，只需用户最后一次输入完，再发送请求
- 窗口大小 resize，只需窗口调整完成后，计算窗口大小，防止重复渲染。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>防抖</title>
        <script src="https://cdn.bootcdn.net/ajax/libs/underscore.js/1.13.6/underscore-min.js"></script>
    </head>
    <body>
        <div>
            普通输入框：
            <input class="input1" />
        </div>
        <div>
            防抖输入框：
            <input class="input2" />
        </div>
        <script>
            // 普通
            const inputEl1 = document.querySelector(".input1");
            let counter1 = 1;
            inputEl1.oninput = function () {
                console.log(`发送网络请求${counter1++}`, this.value);
            };
            // 防抖处理过的
            const inputEl2 = document.querySelector(".input2");
            let counter2 = 1;
            inputEl2.oninput = _.debounce(function () {
                console.log(`防抖处理：发送网络请求${counter2++}`, this.value);
            }, 1000);
        </script>
    </body>
</html>
```

## 手写 debounce

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>手写防抖</title>
    <script>
        function kaimoDebounce(fn, delay) {
            let timer = null;
            let _debounce = function (...args) {
                // 清除上一次定时器
                clearTimeout(timer);
                // 开启新的一个定时器
                timer = setTimeout(() => {
                    // this 和参数绑定
                    fn.apply(this, args);
                    // 函数执行完之后，将timer置为null
                    timer = null;
                }, delay);
            };
            return _debounce;
        }
    </script>
</head>

<body>
    <div>
        防抖输入框：
        <input class="input" />
    </div>
    <script>
        const inputEl = document.querySelector(".input");
        let counter = 1;
        inputEl.oninput = kaimoDebounce(function (e) {
            console.log(`手写防抖：发送网络请求${counter++}`, this, this.value);
            console.log(e);
        }, 1000);
    </script>
</body>

</html>
```
