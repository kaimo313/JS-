## new 做了什么?

1. 在构造器内部创建一个新的对象
2. 这个对象内部的隐式原型指向该构造函数的显式原型
3. 让构造器中的 this 指向这个对象
4. 执行构造器中的代码
5. 如果构造器中没有返回对象，则返回上面的创建出来的对象

## 手写 new 的过程

new 是一个运算符，只能通过函数的方式去模拟

```html
<script>
    function Person(name, age) {
        this.name = name;
        this.age = age;
    }
    // 使用 kaimoPerson 函数去模拟 new 运算符
    function kaimoPerson(fn, ...args) {
        // 1) 创建一个对象
        let obj = {};
        // 2) 让对象的隐式原型指向 fn 的显式原型
        obj.__proto__ = fn.prototype;
        // 3) 改变 this 指向；4) 执行 fn
        fn.apply(obj, args);
        // 5) 返回对象
        return obj;
    }

    let p1 = new Person("kaimo", 313);
    console.log("p1---->", p1);
    let p2 = kaimoPerson(Person, "kaimo", 313);
    console.log("p2---->", p2);
</script>
```