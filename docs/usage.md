# Vue的使用

## 1. 安装

~~~shell
npm install vue
~~~

**npm**的使用请另外学习

国内环境使用国内镜像定制的npm版本**cnpm**

~~~shell
npm install -g cnpm --registry=https://registry.npm.taobao.org
~~~

**cnpm**安装命令

~~~shell
cnpm install vue
~~~

## 2. 语法

### 2.1 Hello world

Html

~~~html
<div id="app">
  {{ message }}
</div>
~~~

~~~javascript
Javascript

var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!'
  }
})
~~~

Full

~~~html
<html>

<head>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>

<body>
    <div id="app">
        {{message}}
    </div>
    <script type="text/javascript">
        var app = new Vue({
            el: "#app",
            data: {
                message: "hello vue!"
            }
        });
    </script>
</body>

</html>
~~~

### 2.2 页面与代码分离

hello.html

~~~html
<html>

<head>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>

<body>
    <div id="app">
        {{message}}
    </div>
    <script src="hello.js"></script>
</body>

</html>
~~~

hello.js

~~~javascript
var app = new Vue({
    el: "#app",
    data: {
        message: "hello vue!"
    }
});
~~~

### 2.3 v-bind  绑定属性

~~~html
<html>

<head>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>

<body>
    <span id="app" v-bind:title="message">
        Hello. I have a title
    </span>
    <script type="text/javascript">
        var app = new Vue({
            el: "#app",
            data: {
                message: "Hello," + new Date().toLocaleDateString()
            }
        });
    </script>
</body>

</html>
~~~

v-bind 缩写

~~~html
<!-- 完整语法 -->
<a v-bind:href="url">...</a>

<!-- 缩写 -->
<a :href="url">...</a>
~~~



### 2.3 v-if     条件

~~~html
<html>

<head>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>

<body>
    <div id="app">
        <p v-if="seen">You can see me now.</p>
    </div>
    <script type="text/javascript">
        var app = new Vue({
            el: "#app",
            data: {
                seen: true
            }
        });
    </script>
</body>

</html>
~~~

### 2.4 v-for    循环

~~~html
<html>

<head>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>

<body>
    <div id="app">
        <ul>
            <li v-for="todo in todos">{{todo.desc}}</li>
        </ul>
        <p>{{todos.length}}</p>
    </div>
    <script type="text/javascript">
        var app = new Vue({
            el: "#app",
            data: {
                todos: [
                    {desc:"学习"},
                    {desc:"运动"},
                    {desc:"看电影"}
                ]
            }
        });
    </script>
</body>

</html>
~~~

### 2.5 v-on   事件

~~~html
<html>

<head>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>

<body>
    <div id="app">
        <p>{{message}}</p>
        <button v-on:click="reverseMessage">Reverse</button>
    </div>
    <script type="text/javascript">
        var app = new Vue({
            el: "#app",
            data: {
                message: "Hello, vuejs!"
            },
            methods: {
                reverseMessage: function () {
                    this.message = this.message.split('').reverse().join('');
                }
            }
        });
    </script>
</body>

</html>
~~~

v-on缩写

~~~html
<!-- 完整语法 -->
<a v-on:click="doSomething">...</a>

<!-- 缩写 -->
<a @click="doSomething">...</a>
~~~



### 2.6 v-model  双向绑定

~~~html
<html>

<head>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>

<body>
    <div id="app">
        <p>{{message}}</p>
        <input v-model="message"/>
    </div>
    <script type="text/javascript">
        var app = new Vue({
            el: "#app",
            data: {
                message: "Hello, vue"
            } 
        });
    </script>
</body>

</html>
~~~

### 2.7 v-html  原始HTML   

P.S. <span style="color:red">生产环境中危险</span>

~~~html
<html>

<head>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>

<body>
    <div id="app">
        <p>Raw: {{raw}}</p>
        <p>Direct: <span v-html="raw"></p></p>
    </div>
    <script type="text/javascript">
        var app = new Vue({
            el: "#app",
            data: {
                raw: "<span style='color:red'>raw html</span>"
            }
        });
    </script>
</body>

</html>
~~~

### 2.8 v-bind:class 绑定样式类

#### 2.8.1 JSON对象

~~~html
<html>

<head>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <style type="text/css">
        .active{
            color: red;
        }

        .static{
            font-style:oblique;
        }
    </style>
</head>

<body>
    <div id="app" :class="{static:true,active:isActive}">Hello</div>
    <script type="text/javascript">
        var app = new Vue({
            el: "#app",
            data: {
                isActive: true
            }
        });
    </script>
</body>

</html>
~~~

#### 2.8.2 数据对象

也可以采用下面的方式赋值样式类

~~~html
<html>

<head>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <style type="text/css">
        .active {
            color: red;
        }

        .static {
            font-style: oblique;
        }
    </style>
</head>

<body>
    <div id="app" :class="classObj">Hello</div>
    <script type="text/javascript">
        var app = new Vue({
            el: "#app",
            data: {
                classObj: {
                    active: true,
                    static: true
                }
            }
        });
    </script>
</body>

</html>
~~~

#### 2.8.3 计算属性

也可以采用计算属性赋值样式类

~~~html
<html>

<head>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <style type="text/css">
        .danger {
            color: red;
        }

        .active {
            font-style: oblique;
        }
    </style>
</head>

<body>
    <div id="app" :class="classObj">Hello</div>
    <script type="text/javascript">
        var app = new Vue({
            el: "#app",
            data: {
                isActive: true,
                error: null
            },
            computed: {
                classObj: function () {
                    return {
                        active: this.isActive && !this.error,
                        danger: this.error && this.error.type === 'fatal'
                    }
                }
            },
        });
    </script>
</body>

</html>
~~~



#### 2.8.4 数组

~~~html
<html>

<head>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <style type="text/css">
        .danger {
            color: red;
        }

        .active {
            font-style: oblique;
        }
    </style>
</head>

<body>
    <div id="app" :class="[active,'danger']">Hello</div>
    <script type="text/javascript">
        var app = new Vue({
            el: "#app",
            data: {
                active: "active"
            }
        });
    </script>
</body>

</html>
~~~

### 2.9 v-bind:style  绑定样式

~~~html
<html>

<head>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>

<body>
    <div id="app" :style="{color:activeColor,'font-size':fontSize+'px'}">Hello</div>
    <script type="text/javascript">
        var app = new Vue({
            el: "#app",
            data: {
                activeColor: "red",
                fontSize: 50
            }
        });
    </script>
</body>

</html>
~~~

`v-bind:style` 的对象语法十分直观——看着非常像 CSS，但其实是一个 JavaScript 对象。CSS 属性名可以用驼峰式 (camelCase) 或短横线分隔 (kebab-case，记得用单引号括起来) 来命名：

~~~html
<div v-bind:style="styleObject"></div>
~~~

~~~javascript
data: {
  styleObject: {
    color: 'red',
    fontSize: '13px'
  }
}
~~~

#### 2.9.1 多重值

从 2.3.0 起你可以为 `style` 绑定中的属性提供一个包含多个值的数组，常用于提供多个带前缀的值，例如：

```
<div :style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>
```

这样写只会渲染数组中最后一个被浏览器支持的值。在本例中，如果浏览器支持不带浏览器前缀的 flexbox，那么就只会渲染 `display: flex`

### v-if-else

~~~html
<html>

<head>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>

<body>
    <div id="app">
        <p v-if="seen">Seen.</p>
        <p v-else="seen">Not seen.</p>
    </div>
    <script type="text/javascript">
        var app = new Vue({
            el: "#app",
            data: {
                seen: true
            }
        });
    </script>
</body>

</html>
~~~



------

## 3. 数据与生命周期

### 3.1 数据与方法

当一个 Vue 实例被创建时，它向 Vue 的**响应式系统**中加入了其 `data` 对象中能找到的所有的属性。当这些属性的值发生改变时，视图将会产生“响应”，即匹配更新为新的值。

~~~javascript
// 我们的数据对象
var data = { a: 1 }

// 该对象被加入到一个 Vue 实例中
var vm = new Vue({
  data: data
})

// 获得这个实例上的属性
// 返回源数据中对应的字段
vm.a == data.a // => true

// 设置属性也会影响到原始数据
vm.a = 2
data.a // => 2

// ……反之亦然
data.a = 3
vm.a // => 3
~~~

当这些数据改变时，视图会进行重渲染。值得注意的是只有当实例被创建时 `data` 中存在的属性才是**响应式**的。也就是说如果你添加一个新的属性，比如：

~~~javascript
vm.b = 'hi'
~~~

那么对 `b` 的改动将不会触发任何视图的更新。如果你知道你会在晚些时候需要一个属性，但是一开始它为空或不存在，那么你仅需要设置一些初始值。比如：

~~~javascript
data: {
  newTodoText: '',
  visitCount: 0,
  hideCompletedTodos: false,
  todos: [],
  error: null
}
~~~

这里唯一的例外是使用 `Object.freeze()`，这会阻止修改现有的属性，也意味着响应系统无法再*追踪*变化。

~~~javascript
var obj = {
  foo: 'bar'
}

Object.freeze(obj)

new Vue({
  el: '#app',
  data: obj
})
~~~

~~~html
<div id="app">
  <p>{{ foo }}</p>
  <!-- 这里的 `foo` 不会更新！ -->
  <button v-on:click="foo = 'baz'">Change it</button>
</div>
~~~

除了数据属性，Vue 实例还暴露了一些有用的实例属性与方法。它们都有前缀 `$`，以便与用户定义的属性区分开来。例如：

~~~javascript
var data = { a: 1 }
var vm = new Vue({
  el: '#example',
  data: data
})

vm.$data === data // => true
vm.$el === document.getElementById('example') // => true

// $watch 是一个实例方法
vm.$watch('a', function (newValue, oldValue) {
  // 这个回调将在 `vm.a` 改变后调用
})
~~~



以后你可以在 [API 参考](https://cn.vuejs.org/v2/api/#%E5%AE%9E%E4%BE%8B%E5%B1%9E%E6%80%A7)中查阅到完整的实例属性和方法的列表。

### 3.2 计算属性

~~~html
<html>

<head>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>

<body>
    <div id="app">
        <p>{{message}}</p>
        <p>{{reverseMessage}}</p>
    </div>
    <script type="text/javascript">
        var app = new Vue({
            el: "#app",
            data: {
                message: "Hello, vuejs!"
            },
            computed: {
                reverseMessage: function () {
                    return this.message.split('').reverse().join('');
                }
            }
        });
    </script>
</body>

</html>
~~~

#### 3.2.1 getter 与 setter

~~~html
<html>

<head>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>

<body>
    <div id="app">
        <p>{{firstName}}</p>
        <p>{{lastName}}</p>
        <p>{{fullName}}</p>
    </div>
    <script type="text/javascript">
        var app = new Vue({
            el: "#app",
            data: {
                firstName: "Foo",
                lastName: "Bar"
            },
            computed: {
                fullName: {
                    get: function () {
                        return this.firstName + " " + this.lastName;
                    },
                    set: function (newValue) {
                        var names = newValue.split(' ')
                        this.firstName = names[0]
                        this.lastName = names[names.length - 1]
                    }
                }
            }
        });
    </script>
</body>

</html>
~~~



### 3.3 侦听属性

#### 3.3.1 简单示例

~~~html
<html>

<head>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>

<body>
    <div id="app">
        {{fullName}}
    </div>
    <script type="text/javascript">
        var app = new Vue({
            el: '#app',
            data: {
                firstName: 'Foo',
                lastName: 'Bar',
                fullName: 'Foo Bar'
            },
            watch: {
                firstName: function (val) {
                    this.fullName = val + ' ' + this.lastName
                },
                lastName: function (val) {
                    this.fullName = this.firstName + ' ' + val
                }
            }
        })
    </script>
</body>

</html>
~~~

#### 3.3.3.2 复杂示例

~~~html
<html>

<head>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/axios@0.12.0/dist/axios.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/lodash@4.13.1/lodash.min.js"></script>
</head>

<body>
    <div id="app">
        <p>
            Ask a yes/no question:
            <input v-model="question">
        </p>
        <p>{{ answer }}</p>
    </div>
    <script type="text/javascript">
        var app = new Vue({
            el: '#app',
            data: {
                question: '',
                answer: 'I cannot give you an answer until you ask a question!'
            },
            watch: {
                // 如果 `question` 发生改变，这个函数就会运行
                question: function (newQuestion, oldQuestion) {
                    this.answer = 'Waiting for you to stop typing...'
                    this.debouncedGetAnswer()
                }
            },
            created: function () {
                // `_.debounce` 是一个通过 Lodash 限制操作频率的函数。
                // 在这个例子中，我们希望限制访问 yesno.wtf/api 的频率
                // AJAX 请求直到用户输入完毕才会发出。想要了解更多关于
                // `_.debounce` 函数 (及其近亲 `_.throttle`) 的知识，
                // 请参考：https://lodash.com/docs#debounce
                this.debouncedGetAnswer = _.debounce(this.getAnswer, 500)
            },
            methods: {
                getAnswer: function () {
                    if (this.question.indexOf('?') === -1) {
                        this.answer = 'Questions usually contain a question mark. ;-)'
                        return
                    }
                    this.answer = 'Thinking...'
                    var vm = this
                    axios.get('https://yesno.wtf/api')
                        .then(function (response) {
                            vm.answer = _.capitalize(response.data.answer)
                        })
                        .catch(function (error) {
                            vm.answer = 'Error! Could not reach the API. ' + error
                        })
                }
            }
        })
    </script>
</body>

</html>
~~~



### 3.4 生命周期钩子

![生命周期](https://cn.vuejs.org/images/lifecycle.png)

#### 3.2.1 Create  被创建

~~~html
<html>

<head>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>

<body>
    <div id="app">
        hello
    </div>
    <script>
        var app = new Vue({
            el: "#app",
            created() {
                console.log("i am created");
            },
        });
    </script>
</body>

</html>
~~~

P.S.

~~~ps
不要在选项属性或回调上使用箭头函数，比如 created: () => console.log(this.a) 或 vm.$watch('a', newValue => this.myMethod())。因为箭头函数是和父级上下文绑定在一起的，this 不会是如你所预期的 Vue 实例，经常导致 Uncaught TypeError: Cannot read property of undefined 或 Uncaught TypeError: this.myMethod is not a function 之类的错误。
~~~



<hr>

## 4. 组件化应用



### 4.1 最简单的组件

~~~html
<html>

<head>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>

<body>
    <div id="app">
        <ul>
            <todo-item></todo-item>
            <todo-item></todo-item>
        </ul>
    </div>
    <script type="text/javascript">
        Vue.component("todo-item", {
            template: "<li>I am a to-do item</li>"
        });

        var app = new Vue({
            el: "#app"
        });
    </script>
</body>

</html>
~~~



### 4.2  组件包含数据











## 5. 调试

## 6. 编译发布

## 7. 前后端分离

