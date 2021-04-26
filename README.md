# ES6+VUE基础入门

## 1. ES6入门

### 视频教程

http://e-learning.51cto.com/video/590613

### 概念

#### **干什么的**

5.1版本JS语言的下一个标准，2015年发布，企业级开发语言

#### **有什么用**

框架vue react 基础；

大部分公司使用es6；

#### **新的特性**

![image-20210403101419302](C:\Users\liesmars\AppData\Roaming\Typora\typora-user-images\image-20210403101419302.png)

#### **浏览器兼容性**

![image-20210403101501600](C:\Users\liesmars\AppData\Roaming\Typora\typora-user-images\image-20210403101501600.png)

**babel编译器：**将es6转换为es5代码，让浏览器获得支持	教程 https://es6.ruanyifeng.com/#docs/intro

[Babel](https://babeljs.io/) 是一个广泛使用的 ES6 转码器，可以将 ES6 代码转为 ES5 代码，从而在老版本的浏览器执行。这意味着，你可以用 ES6 的方式编写程序，又不用担心现有环境是否支持。下面是一个例子。

```javascript
// 转码前
input.map(item => item + 1);

// 转码后
input.map(function (item) {
  return item + 1;
});
```

上面的原始代码用了箭头函数，Babel 将其转为普通函数，就能在不支持箭头函数的 JavaScript 环境执行了。

```html
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
<script type="text/babel">
// Your ES6 code
</script>
```

#### 参考文献

es6阮一峰教程	https://es6.ruanyifeng.com/

MDN教程	https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript

### 语法特性

#### 1. let和const

- 声明变量，没有变量提升(不能提到最上面声明)

- 块级作用域
- 不能重复声明

**作用：**

- for循环

- 不污染全局变量

```html
    <script>
        //var
        // console.log(a);
        // var a = 2;

        //1.let声明变量，没有变量提升
        // console.log(a);
        // let a = 10;

        //2. let是一个块级作用域
        // if (true) {
        //     let b = 10;
        // }
        // console.log(b);

        //3. let不能重复声明
        // let a = 10;
        // let a = 20;
        // console.log(a);

        // const 和 let 一样；但是声明常量，做插件用

        //作用1 for循环
        // var arr = [];
        // for(let i = 0;i < 10;i++){
        //     arr[i] = function(){
        //         return i;
        //     }
        // }
        // console.log(arr[5]());// var 10  let 5 

        // 作用2：不会污染全局变量
        let RegExp = 10;
        console.log(RegExp);
        console.log(window.RegExp);

        //建议：一般使用const 需要修改变量值的时候使用let
    </script>
```

#### 2. 模板字符串

**模板字符串使用反应号`，插入变量时，使用${变量名}**

就不需要字符串拼接了

```html
<script>
    //模板字符串使用反应号`，插入变量时，使用${变量名}
    const oBox = document.querySelector(".box");
    let id = 1;
    let name = "峥宝"

    let htmlStr = `<ul>
        <li>
            <p id=${id}>${name}</p>
        </li>
    </ul>`;
    // oBox.innerHTML = "<ul><li><p id=" + id + ">" + name + "</p></li></ul>"
    oBox.innerHTML = htmlStr;
</script>
```

#### 3. 强大的函数

- 带参数默认值的函数	function add(a, b = 10) {}
- 默认的表达式也可以是一个函数   function add(a, b = getVal(5)) {}
- es6 剩余参数：三个点...和一个紧跟着的具名参数指定...keys    
- es6扩展运算符  Math.max(...arr)

#####  箭头函数   

- 使用=>来定义function(){} 等价于 ()=>{}

- 没有this绑定，箭头函数没有作用域链，一旦使用箭头函数，没有作用域链，就找上层对象
- 使用箭头函数，内部没有arguments
- 不能使用new关键字,没有constructor属性

```html
    <script>
        // 1.带参数默认值的函数

        // es5
        // function add(a, b) {
        //     a = a || 10;
        //     b = b || 10;
        //     return a + b;
        // }
        // console.log(add(60));

        // es6
        // function add(a, b = 10) {
        //     return a + b;
        // }
        // console.log(add(20));

        // 2. 默认的表达式也可以是一个函数
        // function add(a, b = getVal(5)) {
        //     return a + b;
        // }
        // function getVal(val){
        //     return val + 5;
        // }
        // console.log(add(10));

        //es5 剩余参数方法
        // function pick(obj){
        //     let result = Object.create(null);
        //     for(let i = 1;i<arguments.length;i++){
        //         result[arguments[i]] = obj[arguments[i]];
        //     }
        //     return result;
        // }
        // let book = {
        //     title : "es6",
        //     author: "峥宝",
        //     year : 2021
        // }
        // let bookData = pick(book,'title','author','year');
        // console.log(bookData);

        // 3. es6 剩余参数：三个点...和一个紧跟着的具名参数指定...keys

        /*         function pick(obj, ...keys) {
                    let result = Object.create(null);
                    // console.log(keys);
                    //解决了剩余参数 arguments复杂不方便的问题
                    for (let i = 0; i < keys.length; i++) {
                        result[keys[i]] = obj[keys[i]];
                    }
                    return result;
                }
                let book = {
                    title: "es6",
                    author: "峥宝",
                    year: 2021
                }
                let bookData = pick(book, 'title', 'author', 'year');
                console.log(bookData); 
        */


        //4. es6扩展运算符
        //剩余运算符：把多个独立的合并到一个数组中
        //扩展运算符：把一个数组分割，并将各个项作为分离的参数传给函数
        // const arr = [1, 20, 50, 64, 15, 89, 95, 100];
        // console.log(Math.max.apply(null,arr));        //es5
        // console.log(Math.max(...arr));        //es6

        //5.箭头函数
        // 使用=>来定义function(){} 等价于 ()=>{}
        /*         let add = (a, b) => a + b;
                let add2 = (a, b = 10) => a + b;
                let getJson = () =>({
                    name:"wz",
                    id: 1 
                });
                let fn = (()=>{
                    var name = "hellof";//局部变量
                    return ()=> name;
                })();
        
                console.log(getJson());
                console.log(fn());//可以闭包输出局部变量
                console.log(name);//无法输出局部变量 */

        //没有this绑定
        //es5中的this指向：取决于调用该函数的上下文对象
/*         let PageHandle = {
            id: 123,
            init: function () {
                //this.doSomething is not a function
                //箭头函数没有作用域链，一旦使用箭头函数，没有作用域链，就找上层对象
                document.addEventListener('click', () => {
                    this.doSomething(event.type);
                }, false);
            },
            doSomething: function (type) {
                console.log(`当前id:${this.id}`);
            }
        }
        PageHandle.init(); */

        //箭头函数注意事项
        //1.使用箭头函数，内部没有arguments,没有作用域链，指向document对象
/*         let getVal = (a, b) => {
            //arguments is not defined
            console.log(arguments);
        }
        console.log(getVal(5, 10)); */

        //2. 箭头函数不能使用new关键字,没有constructor属性
        // let Person = ()=>{console.log(1);};
        let Person = function(){console.log(1);};
        let p = new Person();//Person is not a constructor
        console.log(p);
        </script>

```

#### 4. 解构赋值

- 解构赋值是对赋值运算符的一种扩展

- 它针对数组和对象进行操作

- 优点：代码书写上简洁易读

  

```html
    <script>
        // 解构赋值是对赋值运算符的一种扩展
        // 它针对数组和对象进行操作
        // 优点：代码书写上简洁易读

        let code = {
            type: "hh",
            name: "foo"
        }

        //es5
        // let type = code.type;
        // let name = code.name;
        //es6
        let { type, name } = code;//完全解构

        let obj = {
            a: 1,
            b: [],
            c: 'hello'
        }
        let { a, ...res } = obj;//不完全解构
        console.log(res);

        //数组解构
        let arr = [1, 2, 3];
        let [x, y] = arr;
        console.log(x, y);

        //可嵌套
        let arr = [1, [2], 3];
        let [x, [y]] = arr;
    </script>
```

#### 5. 扩展的对象功能

- es6 方法对象简写

- is() === 

- assig()

```html
    <script>
        //es6 方法对象简写
        const name = 'wz',age = 23;
        const person = {
            isShow:true,
            [name + 'abc']:123,
            name,//等价于name:name
            age,
            logName(){
                console.log(this.age);
            },
            assets:2000,
            setAsset(newAsset){
                this.assets = newAsset;
            },
            getAsset(){
                return this.assets;
            }
        }
        person.logName();
        person.setAsset(5000);
        console.log(person.getAsset());
        console.log(person);
        
        //is() === 
        //比较两个对象是否严格相等
        // console.log(NaN === NaN);
        console.log(Object.is(NaN,NaN));

        //assig()
        //对象的合并
        console.log(Object.assign({},{a:220},{b:20}));
    </script>
```

#### 6. Map and Set

- set集合数据类型，表示无重复值的有序列表
  - add
  - delete
  - has
- map类型是键值对的有序列表，键和值是任意对象
  - set
  - delete
  - clear

```html
    <script>
        //set集合数据类型，表示无重复值的有序列表
        let set = new Set();
        console.log(set);
        //添加元素
        set.add(2);
        set.add('aaa');
        set.add([2,3,4]);
        //delete
        set.delete('aaa');
        //判断has是否存在
        console.log(set.has('aaa'));
        //遍历
        //将其转换为数组
        let set2 = new Set([1,2,4,5,6,3,6]);
        console.log(set2);
        //扩展运算符-把一个数组分割，并将各个项作为分离的参数传给函数
        let arr = [...set2];
        console.log(arr);
        
        //1. set中对象的引用无法被释放
        let set3 = new Set();
        obj = {};
        set3.add(obj);
        obj = null;//释放当前对象
        console.log(set3);


        //map类型是键值对的有序列表，键和值是任意对象
        let map = new Map();
        //添加元素
        map.set('name','wz');
        map.set('age',23);
        //删除元素
        map.delete('name');
        //has
        map.has('age');//ture
        //全部删除
        map.clear();
        console.log(map);
    </script>

```

#### 7. 数组

Array的方法

<img src="E:\OneDrive - whu.edu.cn\Typora\网课\ES6+VUE基础入门.assets\image-20210412190825398.png" alt="image-20210412190825398" style="zoom: 67%;" />

- from()将伪数组转换为数组	let arr = Array.from(arguments);
- from 1伪数组 2对伪数组进行处理     Array.from(lis, ele => ele.textContent)
- of 将任意数据类型，转换的到数组中
- find 找出第一个符合条件的数组成员
- 遍历器  entries() keys() values() 返回一个键，值，键值对遍历器，可以用for of 循环进行遍历
- includes()判断数组是否包含给定值

```html
    <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
    </ul>
    <script>
        //数组的方法 from() of()
        //from()将伪数组转换为数组
        function add(a, b) {
            console.log(arguments);
            //es5转换
            // let arr = [].slice.call(arguments);
            //es6转换
            //from转换
            let arr = Array.from(arguments);
            console.log(arr);
            //1. 扩展运算符转换伪数组
            console.log([...arguments]);
        }
        add(1, 2);
        //2. from 1伪数组 2对伪数组进行处理
        let lis = document.getElementsByTagName('li');
        console.log(Array.from(lis, ele => ele.textContent));

        //3. of 将任意数据类型，转换的到数组中
        let arr2 = Array.of(2, 3, 4, 5, [1, 3, 4], { id: 2 });
        console.log(arr2);

        //4. find 找出第一个符合条件的数组成员
        console.log(arr2.find(n => n > 3));
        console.log(arr2.findIndex(n => n > 3));

        //5. 遍历器
        // entries() keys() values() 返回一个键，值，键值对遍历器，可以用for of 循环进行遍历
        for(let index of ['a','b'].keys()){
            console.log((index));
        }
        for(let value of ['a','b'].values()){
            console.log((value));
        }
        for(let [index,value] of ['a','b'].entries()){
            console.log((index));
        }
        for(let [index,value] of ['a','b'].entries()){
            console.log((value));
        }

        //6. includes()判断数组是否包含给定值
        console.log([1,3,4].includes(5));//false
    </script>

```

#### 8. 迭代器

-  Iterator
-  一种新的遍历机制  遍历=迭代
   - 迭代器是一个接口，能快捷访问数据，通过symbol.iterator来创建迭代器，next访问数据
   - 迭代器是用于遍历数据结构的指针

```html
    <script>
        //Iterator
        //一种新的遍历机制  遍历=迭代
        //1. 迭代器是一个接口，能快捷访问数据，通过symbol.iterator来创建迭代器，next访问数据
        //2. 迭代器是用于遍历数据结构的指针

        //使用迭代
        const items = ['a', 'b', 'c'];
        console.log(items);
        //创建新的迭代器
        const ite = items[Symbol.iterator]();
        console.log(ite.next());
        console.log(ite.next());
        console.log(ite.next());
        console.log(ite.next());
    </script>
```

#### 9. 生成器

- generator函数 function* 可以通过yield关键字，将函数挂起。可以使用next
- generator函数是分段执行的，yield是暂停执行，next是继续执行
- x真的不是yield ‘2’的返回值，它是next()调用 恢复当前yield()执行的传值
- 使用场景：为不具备迭代器Interator接口的对象体提供了遍历操作

```html
    <script>
        //generator函数 function* 可以通过yield关键字，将函数挂起。可以使用next

        function* func() {
            console.log("1");
            yield 2;
            console.log("2");
            yield 3;

        }
        //返回一个遍历器对象 可以调用next
        let fn = func();
        // console.log(o);
        console.log(fn.next());
        console.log(fn.next());
        console.log(fn.next());

        //总结：generator函数是分段执行的，yield是暂停执行，next是继续执行

        function* add() {
            console.log("s");
            //x真的不是yield ‘2’的返回值，它是next()调用 恢复当前yield()执行的传值
            let x = yield '2';
            console.log('one' + x);
            let y = yield '3';
            console.log('two' + y);
            return x + y;
        }
        const fn2 = add();
        console.log(fn2.next());
        console.log(fn2.next(20));
        console.log(fn2.next(30));

        //使用场景：为不具备迭代器Interator接口的对象体提供了遍历操作
        const obj = {
            name: 'wz',
            age: 23
        }
        function* ObjectEntries(obj) {
            //获取对象的所有key保存到数组[name,age]
            const propKeys = Object.keys(obj);
            for (const propKey of propKeys) {
                yield [propKey, obj[propKey]];
            }
        }
        obj[Symbol.iterator] = ObjectEntries;
        console.log(obj);

        for (let [key, value] of ObjectEntries(obj)) {
            console.log(`${key}：${value}`);
        }

    </script>

```

#### 10. 生成器应用

- 避免回调地狱
- 数据加载 异步变同步

```html
    <script>
        //避免回调地狱
        
         function* main(){
             let res = yield request('http://route.showapi.com/238-2?showapi_appid%3Dmyappid%26lng%3D116.32298703399%26lat%3D39.983424051248%26from%3D5%26showapi_sign%3Dmysecret');
             console.log(res);
             //进行下一步操作
             console.log("数据1请求完成");
             let res2 = yield request('http://route.showapi.com/238-2?showapi_appid%3Dmyappid%26lng%3D123.32298703399%26lat%3D39.983424051248%26from%3D5%26showapi_sign%3Dmysecret');
             console.log(res2);
             console.log("数据2请求完成");
         }
         const ite = main();
         ite.next();
 
         function request(url){
             $.ajax({
                 url,
                 method:'get',
                 success(res){
                     ite.next(res);
                 }
             })
         }
         

        //数据加载 异步变同步
        function loadUI() {
            console.log("开始loading");
        }
        function loadData() {
            setTimeout(() => {
                console.log("数据加载完成");
                fn.next();
            }, 1000);

        }
        function loadSuccess() {
            console.log("隐藏loading");
        }

        function* main() {
            loadUI();
            yield loadData();
            loadSuccess();
        }
        const fn = main();
        fn.next();
    </script>
```

#### 11. Promise

- promise 承诺 相当于一个容器，保存着未来还未结束的事件（异步操作）
- 对象的状态不受外界影响  异步操作三个状态  pending(进行) resolved(成功) rejected(失败)
- 一旦状态改变，就不会逆转，任何时候都可以得到这个结果
- resolve可以将任何对象转换为promise对象
- Promise.all() 异步并行 应用于游戏加载资源，前端的静态文件
- 想要某个函数拥有promise功能，只需让其返回一个promise即可。****

```html
    <script>
        //promise 承诺
        //相当于一个容器，保存着未来还未结束的事件（异步操作）
        //各种异步操作都可以用同样的方法进行处理
        //特点
        //1. 对象的状态不受外界影响  异步操作三个状态  pending(进行) resolved(成功) rejected(失败)
        //2. 一旦状态改变，就不会逆转，任何时候都可以得到这个结果
        
        function timeOut(ms) {
            return new Promise((resolved, rejected) => {
                setTimeout(() => {
                    resolved("hello promise success");
                }, ms);
            })
        }
        timeOut(2000).then((val) => {
            console.log(val);
        })

        //具体应用
        function getJSON(url,callback) {
            return new Promise((resolved, rejected) => {
                $.ajax({
                    url,
                    method: 'get',
                    success(res) {
                        resolved(res.showapi_res_id);
                        callback(res.showapi_res_id);
                    }
                })
            })

        }
        getJSON('http://route.showapi.com/238-2?showapi_appid%3Dmyappid%26lng%3D123.32298703399%26lat%3D39.983424051248%26from%3D5%26showapi_sign%3Dmysecret')
            .then((data) => {
                console.log(data);
                
            }, (error) => {
                console.log(error);
            });

        //resolve() reject() all() race() done() finally()

        //resolve可以将任何对象转换为promise对象
        //    let p =  Promise.resolve('foo');
        /*
        let p = new Promise(resolved => resolved('foo'));//等价
        console.log(p);
        p.then((data) => {
            console.log(data);
        })
        */

        //Promise.all() 异步并行 应用于游戏加载资源，前端的静态文件
        /*
        let p1 = new Promise(resolved => resolved('foo'));
        let p2 = new Promise(resolved => resolved('ddd'));
        let p3 = new Promise(resolved => resolved('sss'));
        let p4 = Promise.all([p1,p2,p3]);
        p4.then((data) => {
            console.log(data);
        }).catch(err => {
            console.log('ee');

        })
        */

        //race()请求超时操作
        /*
        function loadImg(imgSrc) {
            return new Promise((resolve, reject) => {
                const img = new Image();
                img.src = imgSrc;
                img.onload = function () {
                    resolve(img);
                }
            })
        }
        function timeout() {
            return new Promise((resolve, reject) => {
                setTimeout(() => {
                    reject(new Error('图片请求超时'));
                }, 3000);
            })
        }
        Promise.race([loadImg('https://tse4-mm.cn.bing.net/th/id/OIP.ZTmNathhKflijArYDaQEDAHaEo?w=249&h=180&c=7&o=5&dpr=2&pid=1.7'), timeout()]).then(data => {
            console.log(data);
            document.body.appendChild(data);
        })
        */
    </script>

```

#### 12 async

```html
    <script>
        //async 是异步操作更加方便
        //await 等待异步操作完成后才执行下面操作
        //基本操作，async可以返回一个promise对象
        //async 是generator的一个语法糖 await async 必须一起使用
        //await后面的东西是一个promise对象 只要一个await是reject就不会往下执行 解决办法：try catch
        //generetor promise async 1. 解决回调地狱 2. 方便异步调用
        async function f() {
            let a = await 'hello async';
            return a + "1111";
        }
        let b;
        f().then(v => { b = v; }).catch(e => { console.log(e); });
        setTimeout(() => {
            console.log(b);
        }, 0);

        function getJSON(url) {
            return new Promise((resolved, rejected) => {
                $.ajax({
                    url,
                    method: 'get',
                    success(res) {
                        resolved(res);
                    }
                })
            })
        }
        async function getMyData(url) {
            let res = await getJSON(url);
            console.log(res);
            let arr = await res.showapi_res_id;
            return arr;

        }
        getMyData('http://route.showapi.com/238-2?showapi_appid%3Dmyappid%26lng%3D123.32298703399%26lat%3D39.983424051248%26from%3D5%26showapi_sign%3Dmysecret')
            .then(data => console.log(data));

    </script>
```

#### 13 class

- 类的继承 和java差不多
- 通过Object.assign()方法来一次性向类中添加多个方法

```html
    <script>
        //es5造类
        /*
        function Person(name, age) {
            this.name = name;
            this.age = age;
        }
        Person.prototype.sayName = function () {
            return this.name;
        }
        let p1 = new Person('wz', 23);
        console.log(p1.sayName());
        */
        //es6造类
        class Person {
            constructor(name, age) {
                this.name = name;
                this.age = age;
            }
            // sayName(){
            //     return this.name;
            // }
            // sayAge(){
            //     return this.age;
            // }
        }
        //通过Object.assign()方法来一次性向类中添加多个方法
        Object.assign(Person.prototype, {
            sayName() {
                return this.name;
            },
            sayAge() {
                return this.age;
            }
        });
        let p1 = new Person('wz', 23);
        console.log(p1);

        //类的继承 和java差不多
        class Animal {
            constructor(name, age) {
                this.name = name;
                this.age = age;
            }
            sayName() {
                return this.name;
            }
            sayAge() {
                return this.age;
            }
        }

        //子类
        class Dog extends Animal {
            constructor(name, age, color) {
                super(name, age);//animal.call(this,name,age)
                this.color = color;
            }
            sayColor() {
                return this.color;
            }
        }
        let d = new Dog('ww', 2, "blue");
        console.log(d);
    </script>

```

#### 14 模块化

- es6模块 有 export和import
- export 抛出 import导入
- 一个模块就是一个独立的文件
- **`export default` 与普通的 `export`不要同时使用**

```javascript
export const name = 'wz';
export const age = 15;
export function sss(){
    console.log("sss");
}

const obj = {
    foo:"foo"
}
const ddd = 'ddd';
export {
    ddd
}
export default obj;
```



```html
    <script type="module">
        //es6模块 有 export和import
        //export 抛出 import导入
        // 一个模块就是一个独立的文件
        // import * as f  from './modules/index.js'
        import obj,{name,age}  from './modules/index.js'
        console.log(name);
        console.log(age);
        console.log(obj);
    </script>
```

### 进阶

#### ES6编程风格

https://www.w3cschool.cn/escript6/escript6-mjlf37fk.html
