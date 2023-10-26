## instanceof 干什么的？

instanceof 运算符用于检测构造函数的 prototype 属性是否出现在某个实例对象的原型链上。

instanceof 可以判断一个对象是否属于某个类

```html
<script>
    function Person(name, age) {
        this.name = name;
        this.age = age;
    }

    Person.prototype.sayHello = function () {
        console.log("hello kaimo");
    };

    // 寄生组合继承
    function Student(name, age, className) {
        // 继承 Person 私有属性
        Person.call(this, name, age);
        this.className = className;
    }

    // 继承 Person 公有属性：使用 `Object.create()` 来解决多次调用父类构造函数问题
    Student.prototype = Object.create(Person.prototype);
    // 由于修改了构造器 `Student.prototype`，`Student.prototype.constructor` 已经不是 Student
    // 为了避免误解，手动重设 `Student.prototype.constructor` 属性
    // 这样通过 new Student 创建的实例的 constructor 又可以正确取到 Student
    Student.prototype.constructor = Student;
    console.log(Student.prototype.constructor);

    let p1 = new Person("kaimo", 313);
    console.log("p1---->", p1 instanceof Person);
    let s = new Student("kaimo-s", 18, "手写课堂");
    console.log(s);
    s.sayHello();
    console.log("s--Student-->", s instanceof Student);
    console.log("s--Person-->", s instanceof Person);
</script>
```

## 手写 instanceof

```html
<script>
    function Person(name, age) {
        this.name = name;
        this.age = age;
    }

    Person.prototype.sayHello = function () {
        console.log("hello kaimo");
    };

    function Student(name, age, className) {
        Person.call(this, name, age);
        this.className = className;
    }

    Student.prototype = Object.create(Person.prototype);
    Student.prototype.constructor = Student;

    // 使用 kaimoInstanceof 模拟 instanceof 运算符
    function kaimoInstanceof(className, obj) {
        let fp = className.prototype; // className 的原型对象
        let cp = obj.__proto__; // obj 是 className 实例的原型对象
        // cp 为 null 结束循环，Object.prototype.__proto__ = null
        while (cp) {
            if (fp === cp) {
                return true;
            }
            // 往原型链上继续找
            cp = cp.__proto__;
        }
        return false;
    }

    let p1 = new Person("kaimo", 313);
    console.log("p1---->", kaimoInstanceof(Person, p1));
    let s = new Student("kaimo-s", 18, "手写课堂");
    console.log(s);
    s.sayHello();
    console.log("s--Student-->", kaimoInstanceof(Student, s));
    console.log("s--Person-->", kaimoInstanceof(Person, s));
</script>
```