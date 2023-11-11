## 什么是节流

节流是限制事件触发的频率，当持续触发事件时，在一定时间内只执行一次事件，这个效果跟英雄联盟里的闪现技能释放差不多。

函数防抖关注一定时间连续触发的事件只在最后执行一次，而函数节流侧重于一段时间内只执行一次。

间隔一段时间执行一次回调的场景有：

- 滚动加载，加载更多或滚到底部监听
- 谷歌搜索框，搜索联想功能
- 高频点击提交，表单重复提交

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>节流</title>
    <script src="https://cdn.bootcdn.net/ajax/libs/underscore.js/1.13.6/underscore-min.js"></script>
</head>

<body>
    <div>
        普通输入框：
        <input class="input1" />
    </div>
    <div>
        节流输入框：
        <input class="input2" />
    </div>
    <script>
        // 普通
        const inputEl1 = document.querySelector(".input1");
        let counter1 = 1;
        inputEl1.oninput = function () {
            console.log(`发送网络请求${counter1++}`, this.value);
        };
        // 节流处理过的
        const inputEl2 = document.querySelector(".input2");
        let counter2 = 1;
        inputEl2.oninput = _.throttle(function () {
            console.log(`节流处理：发送网络请求${counter2++}`, this.value);
        }, 1000);
    </script>
</body>

</html>
```

## 手写 throttle

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>手写节流</title>
    <script>
        // 时间戳实现节流
        function kaimoThrottle(fn, delay) {
            let startTime = 0;
            let _throttle = function (...args) {
                let now = new Date().getTime();
                let waitTime = delay - (now - startTime);
                if (waitTime <= 0) {
                    fn.apply(this, args);
                    startTime = now;
                }
            }
            return _throttle;
        }
        // setTimeout 实现节流
        function kaimoThrottle2(fn, delay) {
            let timer = null;
            let _throttle = function (...args) {
                // 如果 timer 不为 null，说明上一个定时器还未执行，则直接返回
                if (timer) {
                    return;
                }
                // 开启新的一个定时器
                timer = setTimeout(() => {
                    // this 和参数绑定
                    fn.apply(this, args);
                    // 函数执行完之后，将timer置为null
                    timer = null;
                }, delay);
            };
            return _throttle;
        }
    </script>
</head>

<body>
    <div>
        节流输入框：
        <input class="input" />
    </div>
    <script>
        const inputEl = document.querySelector(".input");
        let counter = 1;
        inputEl.oninput = kaimoThrottle2(function (e) {
            console.log(`手写节流：发送网络请求${counter++}`, this, this.value);
            console.log(e);
        }, 1000);
    </script>
</body>

</html>
```
