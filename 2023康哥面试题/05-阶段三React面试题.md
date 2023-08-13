# ■ 符号说明

💘 课题   

🐝 企业级面试题

⭐️ 重要知识点

🌛 需要有影响

❄️ 超纲 



# 💘 typescript

# 🐝🐝🐝 any、unknown类型区别

```
1️⃣ any 可以完全不受类型系统的约束，你可以很自由的去使用它，而不用去担心 TS 的类型检测。甚至可以把这个变量赋值给一个明确声明为 boolean  的变量。
2️⃣ any 可以让你完成跳过 TS 的类型系统的检测，你可以在一些紧急的情况使用它来处理一些讨厌的类型错误问题
3️⃣ unknown 则比 any 安全一点，你同样的可以把任意的东西赋值给 unknown，但你却不可以不安全的使用它。怎么理解呢？例如调用 trim() 方法时，你需要通过 typeof 来判断变量，确保是字符串类型时才可以调用。同样的你也需要确定变量是布尔值，才可以赋值给一个声明为 boolean 的变量
⭕️ 相同点：any 和 unknown 在 TS 中像是超级/顶级类型的存在，任意类型的变量都可以赋值给它们，这也是 any 和 unknown 唯一相同的地方
❌ 不同点：unknown 需要先进行类型判断，才可以执行相应的类型操作。所以 unknown 可以被看成是更安全的 any


相同点：
const a: any = 任意类型数据
const a: unknown = 任意类型数据

不同点：
- 说法1：unknown 需要先进行类型判断，才可以执行相应的类型操作。所以 unknown 可以被看成是更安全的 any
- 说法2：在执行大多数操作之前，会进行某种形式的检查。。所以 unknown 可以被看成是更安全的 any

let foo: any = 123;
console.log(foo.msg); // 符合TS的语法
let a_value1: unknown = foo;   // OK
let a_value2: any = foo;      // OK
let a_value3: string = foo;   // OK


let bar: unknown = 222; // OK 
console.log(bar.msg); // Error
let k_value1: unknown = bar;   // OK
let K_value2: any = bar;      // OK
let K_value3: string = bar;   // Error
```

# 🐝🐝🐝 any、void、never区别

```
any（任意类型）
void（无类型   与 any 类型相反，它表示没有任何类型。当一个【函数】没有返回值，通常使用它表示）   
never（永不存在的值的类型 。通常是抛出异常或者永远不会有返回值的类型） 
```



# 🐝🐝🐝 ts新增了哪些数据类型

````
| js 原有类型 | ts 新增数据类型                                              |
| ----------- | ------------------------------------------------------------ |
| null        | ✨✨✨string |number （联合类型）                                 |
| undefined   | ✨✨✨any（任意类型）                                              |
| boolean     | unknown（不详的/未知类型）                                   |
| number      | ✨✨✨type 类型别名（ 自定义类型）                                 |
| string      | tuple（元组   表示一个已知元素数量和类型的数组，各元素的类型不必相同） |
| symbol      | ✨enum（枚举  使用枚举类型可以为**一组数值**赋予**友好的名字**）  ORDER_PAY 0   ORDER_NO_PAY 1 |
| bigint      | ✨✨✨ void（无类型   与 any 类型相反，它表示没有任何类型。当一个函数没有返回值，通常使用它表示） |
| object      | never（永不存在的值的类型 。通常是抛出异常或者永远不会有返回值的类型） |
|             | 字面量类型                                                   |
|             | 等                                                           |
````





# 🐝🐝🐝ts会不会用? 

会



# 🐝🐝🐝interface、type区别 

> 面试题：区别
>
> ```
> type 可以表示原始类型，interface 不能
> type 可以声明联合类型和交叉类型，interface 不能，但是interface extends
> type 重名报错，interface交叉
> ...
> ```
>
> 项目用：如何选择
>
> ```
> 项目开发优先 interface 也比较正统，当无法满足需求的情况下用 type。
> - 备注1： 因为 联合类型 和 交叉类型 是很常用的，所以避免不了大量使用 type 的场景，一些复杂类型也需要通过组装后形成类型别名来使用。
> - 备注2： 想保持代码统一，还是可选择使用 type （不推荐）
> - 备注3： 编写三方库时使用interface，其更加灵活自动的类型合并可应对未知的复杂使用场景。
> ```





type语法：类型别名不仅可以用来表示基本类型，还可以用来表示对象类型、联合类型、元组和交叉类型

````
type Type1 = string; 							  // 基本类型

type Type2 = { a:numer, b: number}  // 对象类型
type Type21 = any[]
type Type22 = (data1:string)=>any

type Type3 = string | number  			  // 联合类型
type Type4 = [number, string]         // 元组
type Type5 = {a:number} & {b:number}  // 交叉（类似于继承）
type Type6<T> = { value: T } 	  	  	// 泛型


// 实现
type Animal = {
	eat(food: string): void
}
class Dog implements Animal {
	eat(food: string): void {
		console.log('eat：', food)
	}
}
````

interface语法：接口 是命名数据结构（例如对象）的另一种方式；与type 不同，interface仅限于描述对象类型。

```
interface Type2 { a:number,b:number }			// 对象类型
interface Type22 { [index:number]:any }
interface Type23 { (data1:string)=>any }

interface Type5 extends 父类型
interface Type6<T> { a:T,b:number }

// 实现
interface Animal {
	eat(food: string): void
}
class Dog implements Animal {
	eat(food: string): void {
		console.log('eat：', food)
	}
}
```



# 🐝🐝🐝 ts的泛型应用场景？

vue  ref

vue reacive

vue  useAxios  Promise<T> 后端返回数据

vue  API.Result<T> {}



react useState<类型>()

react Component<Props, State>

react FC<Props>



# 🌛 修饰符public/protected/private/readonly

public 默认修饰符，TypeScript中类中的成员默认为public

private 类的成员不能在类的外部访问，子类也不可以

protected 类的成员不能在类的外部访问，但是子类中可以访问。如果一个类的构造函数，修饰符为protected，那么此类只能被继承，无法实例化。

readonly 关键字`readonly`可以将实例的属性，设置为只读

```
					
	public  	 自身	子类	外部
	protected   自身	子类 
	private     自身


class Animal
{
    public a = 1
    protected b = 2
    private c = 3
}

class Dog extends Animal {

    readonly d = 4

    constructor() {
        super()
        console.log(1, this.a)
    }
}

const dog1 = new Dog
console.log(2, dog1.a)
console.log(3, dog1.d)
// dog1.d = 44
```





# ts了解过吗，和js区别

# typeScript用的怎么样？好用么？一般用到什么？你觉得是否要用呢？也就是好处是啥呢？怎么写的？

# 你对TS的了解以及泛型





# 💘 day1

# 🐝🐝🐝vue和react区别、vue2和vue3区别

思考：如果你是面试官你问 v2和v3区别   vue和react区别 你想听到什么或者可以从几个维度去回答

回答：

- 第一种：拿出语法区别挨个说   例如  v3相对v2不支持过滤器、混入；....
- 第二种：框架层面思想上设计上、语法层面、底层原理



测试：v2、v3

> 框架层面思想设计上
>
> ```
> - v2不贴近原生很多封装好了 理解起来抽象   不方便二阶段学完很好吸收；v3  定义变量就是模型数据视图可以显示，但是没有响应式  ref、reactive  再比如方法 不需要写个抽象的methods  直接写方法 
> - 还有去掉了抽象的过滤器、混入   而是通过hooks  其实就是函数 
> - composition api、 hooks
> - ts
> - webapck  改成  vite 
> - vuex 改成 pinia   切记细品pinia发展史  先去掉mutations  后来直接里面写composition api
>   等等
> ```
>
> 语法层面：双向绑定、侦听器watch/watchEffect、组件实例需要暴露属性才可以外部使用public/private、生命周期、样式:deep/:global、增加teleport、emits、Fragments、Composition API、sfc script setup等等
>
> 底层原理：Object.defineProperty、Proxy；  diff算法区别

测试：vue、react区别 

> 组件化：Vue的组件化更加直接，因为组件包含了模板、逻辑和样式；而React的组件化更加灵活，它只关注逻辑，样式可以使用外部的CSS文件或库。
>
> ```
> - 相同点 
> react和vue都推崇组件化，通过将页面拆分成一个一个小的可复用单元来提高代码的复用率和开发效率。 在开发时react和vue有相同的套路，比如都有父子组件传参，都有数据状态管理，都有前端路由等。
> 
> - 不同点：.vue template、script、style      .js/jsx/tsx     返回function、class  
> React推荐的做法是JSX + inline style, 也就是把 HTML 和 CSS 全都写进 JavaScript 中,即 all in js;
> Vue 推荐的做法是 template 的单文件组件格式(简单易懂，从传统前端转过来易于理解),即 html,css,JS 写在同一个文件(vue也支持JSX写法)
> ```
>
> 模板语法：Vue使用基于HTML的模板语法，而React使用JSX语法，它将HTML嵌入到JavaScript代码中。
>
> 状态管理：Vue使用名为Vuex、PInia的状态管理库，而React则使用一个名为Redux的库、和基于Redux封装的Dva模块
>
> 生态系统：React的生态系统更加庞大，拥有更多的第三方库和工具。Vue生态系统也很强大，但是相对来说较小。大厂加持
>
> 学习曲线：由于Vue的模板语法和直观的API，学习Vue相对来说比较容易。而React的JSX语法和函数式编程风格，需要一定的JavaScript知识和函数式编程理念。
>
> 移动开发：weex开发app   uniapp、     rn/react native 开发app
>
> 开发团队：尤雨溪团队、Facebook
>
> 数据响应：Vue 的数据响应采用的是双向绑定方式，可以直接修改数据和视图；React 的数据响应采用的是单向数据流方式，需要手动更新数据和视图。
>
> 最终：vue 官方化； react 社区化   





# 🐝 jsx的优点

1、JSX 更加灵活，JSX 执行更快，因为它在编译为 JavaScript 代码后进行了优化

2、Template 更多约束、类型安全的，在编译过程中就能发现错误

等等



> JSX 是一种 JavaScript 语法扩展，是 React 中定义 UI 的一种方式。相对于传统的模板语言，JSX 具有以下优点：
>
> 1. 更加直观
>
> JSX 可以将 HTML 和 JavaScript 代码混合在一起编写，使得代码更加直观和易于理解。开发者可以在组件中轻松地编写 HTML 标记和逻辑代码，不需要在模板和代码之间来回切换。
>
> 1. 更加灵活
>
> JSX 可以在 JavaScript 中使用表达式和变量，可以根据逻辑动态生成组件和元素，使得开发更加灵活。JSX 可以使用 JavaScript 的所有特性，如循环、条件语句、函数调用等。
>
> 1. 更加强大
>
> JSX 可以使用自定义组件、事件处理器、样式、属性等功能，可以创建复杂的 UI 界面。使用 JSX 可以更好地组织代码，使得代码更加易于维护和扩展。
>
> 1. 更加高效
>
> JSX 可以在编译时进行优化，可以生成更加高效的 JavaScript 代码，提高应用程序的性能。JSX 编译器可以将 JSX 转换为常规的 JavaScript 函数调用，这些函数调用会创建 React 元素对象，从而提高了渲染效率。
>
> 总的来说，JSX 具有更加直观、灵活、强大和高效等优点，使得 React 开发更加便捷和高效。但是，对于一些开发者来说，可能需要一些时间来适应 JSX 的语法和编写方式。



# 🌛 babel原理

Babel 是一个 JavaScript 编译器，它可以将最新版的 ECMAScript 代码转换为向后兼容的代码，以便在旧版浏览器或其他 JavaScript 环境中运行。Babel 的核心功能是将 ECMAScript 代码转换为 JavaScript AST（抽象语法树），然后根据一组规则（称为插件）对 AST 进行变换，最后将变换后的 AST 转换为 JavaScript 代码。

下面是 Babel 的编译过程：

1. 解析：将 ECMAScript 代码解析成抽象语法树（AST）。
2. 转换：对 AST 进行转换，可以添加、修改、删除节点等操作，例如将 ES6 的箭头函数转换为 ES5 的函数表达式。
3. 生成：根据变换后的 AST 生成新的 ECMAScript 代码。

Babel 的插件系统是 Babel 的核心，它允许开发者根据需要添加、删除和修改 AST 节点，以达到所需的转换效果。Babel 内置了很多插件，同时还有很多社区维护的插件供使用。

Babel 还有一个很重要的概念：预设（preset）。预设是一组插件的集合，可以直接用于对代码的编译。Babel 官方提供了很多预设，例如 babel-preset-env、babel-preset-react 等。预设通常是针对某种场景或应用开发的，可以减少开发者配置插件的时间和精力。

Babel 在编译时还有一些重要的概念，例如 polyfill、source map 等。polyfill 是在编译时自动添加到代码中的补丁，用于实现一些在当前 JavaScript 运行环境中不支持的特性。source map 是一种映射关系，它将编译后的代码映射回原始代码，方便开发者在调试时快速定位问题。

总之，Babel 的原理是将 ECMAScript 代码转换为抽象语法树（AST），然后根据一组规则对 AST 进行变换，最后将变换后的 AST 转换为 JavaScript 代码。Babel 的插件系统和预设是 Babel 的核心，它们可以帮助开发者实现所需的转换效果。





# 🌛 类组件继承能继承哪些东西

在 React 中，类组件可以通过继承 React.Component 类来创建。继承 React.Component 类后，类组件可以获得以下功能：

1. State 状态：类组件可以定义 state 状态，用于存储组件内部的数据。可以通过 this.state 访问 state 状态，并且可以使用 this.setState 方法更新 state 状态。
2. 生命周期：React 提供了一组生命周期函数，可以在组件的不同阶段执行特定的代码逻辑。类组件可以通过重写这些生命周期函数来自定义组件的行为。
3. Props 属性：类组件可以通过 this.props 访问传递给组件的属性。这些属性是只读的，不能在组件内部修改。
4. Refs 引用：类组件可以通过 Refs 引用来访问组件内部的 DOM 元素或子组件实例。
5. 事件处理函数：类组件可以定义事件处理函数，用于响应用户的交互行为，例如点击、滚动等。
6. Context 上下文：类组件可以通过 Context 来实现跨组件的数据共享。

除了继承 React.Component 类之外，类组件还可以继承其他类或类组件。这种方式可以实现代码的复用和继承，但是需要注意避免出现深层次的继承关系，以避免代码的复杂性和可维护性问题。

需要注意的是，从 React 16.8 开始，React 推出了 Hooks，可以让函数组件也具有类似于类组件的能力，例如状态管理、生命周期函数等。因此，使用 Hooks 可以避免类组件继承的一些问题和限制，建议在新的项目中使用 Hooks。





# 🌛 除jsx外，react还可以使用那些方式编写UI

1. React.createElement()
2. 直接使用 React APIs

除了使用 JSX 和 React.createElement()，React 还提供了一些其他的 API，可以直接操作 React 组件和 DOM 元素。例如，可以使用 React.createRef() 来创建一个 Ref 引用，使用 ReactDOM.render() 来将组件渲染到 DOM 中，使用 ReactDOM.findDOMNode() 来获取组件的 DOM 节点等。

需要注意的是，虽然 React 提供了多种方式编写 UI，但是在实际开发中，JSX 是最常用的方式，因为它可以更方便地编写和阅读复杂的 UI 结构，并且可以使用 Babel 等工具将 JSX 转换为普通的 JavaScript 代码。



# 🐝🐝🐝 diff算法区别

Vue 和 React 在 Virtual DOM Diff 算法的实现上有一些区别。

1. 策略不同

Vue 的 Diff 策略是双端比较，即从两端向中间比较。Vue 会先对新旧节点列表的头尾进行比较，然后移动比较指针，再次比较新旧节点列表的头尾，以此类推。这种策略比较适合处理常见的场景，例如列表末尾插入、删除等操作。

React 的 Diff 策略是遍历算法，即遍历整个 Virtual DOM 树进行比较。React 会使用 Fiber 数据结构，将 Virtual DOM 树分解成多个小的 Fiber 节点，并通过优先级调度和协调算法来决定节点的更新顺序。这种策略比较适合处理复杂的场景，例如节点移动、组件内部状态变化等操作。

1. Key 的处理方式不同

Vue 和 React 在处理 Key 的方式上有一些差异。

Vue 在进行 Diff 算法时，如果没有设置 Key，会采用节点的索引值作为 Key 进行比较。当列表数据变化时，如果新节点和旧节点的顺序没有变化，而只是数据发生了变化，则 Vue 会复用旧节点，从而提高渲染性能。但是，如果新旧节点的顺序发生了变化，则会造成不必要的 DOM 操作，影响性能。

React 强制要求设置 Key，用来标识列表中的每个节点。当列表数据变化时，React 会根据新旧节点的 Key 进行比较，而不是节点的顺序。这种方式可以避免不必要的 DOM 操作，提高渲染性能。

1. Diff 算法复杂度不同

Vue 的 Diff 算法的时间复杂度是 O(n)，即线性复杂度。因为 Vue 的 Diff 算法采用的是双端比较策略，所以在常见的列表末尾插入、删除等操作时，性能表现比较优秀。

React 的 Diff 算法的时间复杂度是 O(n log n)，即对数复杂度。因为 React 的 Diff 算法采用的是遍历算法，所以在复杂的场景下，例如节点移动、组件内部状态变化等操作，性能表现比较优秀。

总的来说，Vue 和 React 的 Diff 算法有一些差异。Vue 的 Diff 算法采用的是双端比较策略，性能表现比较优秀，但在复杂场景下可能会存在性能问题。React 的 Diff 算法采用的是遍历算法，并使用 Fiber 数据结构，能够更好地处理复杂场



# 💘 day2

# 🐝🐝 setState语法是同步的还是异步的，什么时候会合并操作

react16：react控制异步/合并、非react控制同步/不合并
react18：都是异步、归类合并



# 🌛 setState底层原理 

> 在 React 类组件中，`setState()` 方法用于更新组件的状态。当调用 `setState()` 方法时，React 会将新的状态合并到当前的状态中，然后重新渲染组件。
>
> `setState()` 方法的底层实现可以分为以下几个步骤：
>
> 1. 将新的状态对象与当前状态对象合并  神龙教主
>
> 当调用 `setState()` 方法时，React 会将传入的新的状态对象与当前的状态对象进行浅合并。这意味着只有新状态对象中包含的属性会被更新，而当前状态对象中的其他属性将保持不变。
>
> 1. 将合并后的状态对象存储到组件实例中
>
> 合并后的状态对象将被存储到组件实例的一个内部属性中。这个内部属性称为`_pendingState`，表示待处理的状态。
>
> 1. 判断是否处于批量更新模式
>
> 在 React 中，可以通过 `batchedUpdates()` 方法将多个状态更新操作合并为一个批量更新操作，从而提高性能。当调用 `setState()` 方法时，React 会判断当前是否处于批量更新模式。
>
> 如果处于批量更新模式，React 会将组件实例添加到更新队列中，等到下一次批量更新时再进行更新。
>
> 如果不处于批量更新模式，React 会立即进行更新。
>
> 1. 触发组件更新
>
> 当合并后的状态对象被存储到组件实例中后，React 会触发组件的更新流程。在更新流程中，React 会先调用组件的 `shouldComponentUpdate()` 方法，判断是否需要更新组件。
>
> 如果需要更新组件，React 会重新调用组件的 `render()` 方法，生成新的虚拟 DOM 对象。然后，React 会通过 Diff 算法比较新的虚拟 DOM 和旧的虚拟 DOM，计算出需要更新的部分，并生成更新操作。
>
> 最后，React 会将更新操作应用到真实的 DOM 上，完成组件的更新。
>
> 总的来说，`setState()` 方法的底层原理是将新的状态对象合并到当前状态对象中，存储到组件实例中，并触发组件的更新流程。通过这个流程，React 可以保证组件的状态和 UI 同步更新。





# 🐝🐝🐝 函数组件和类组件区别

函数组件：无状态也就是模型数据，无生命周期   hooks
    类组件：有状态，有生命周期



# 🐝🐝🐝 函数组件如何状态管理

可以通过redux、或 hook是新技术





# 🐝🐝🐝 状态state、和属性props区别；如何选

语法角度

```
state可以更新
props因为单向数据流不可以更改
```

功能角度

```
state主要是组件内部状态管理，例如收集表单数据、dialog状态管理等等
props主要子组件传递属性，例如普通的button按钮、table表格、page分页等等都有大量使用
```





# 🐝 谈谈你对合成事件的理解、优势、原理、和原生事件区别

是什么：React模拟原生 DOM 事件开发的一套事件系统

> ```
> //  原生事件
> <button onclick="处理函数">+1</button>
> 或
> document.qs().onclick = function() {}
> 或
> document.qs().addEventListener('click', function(){})
> 
> 
> // 合成事件：这个onClick就是
> <button onClick={xxx}>+1</button>
> ```

啥好处

> 如果把所有的事件处理函数都绑定在DOM上，那么在页面响应的时候就会收到影响，导致页面很慢。react为了避免这类DOM事件的滥用，同时屏蔽底层之间不同浏览器事件的系统差异，实现了一个中间层- syntheticEvent合成事件
>
> ```
> 更好的兼容性和跨平台
> 避免频繁绑定和解绑事件，也方便事件统一管理
> 减少内存消耗，挂载到documnet，React17事件委托的变更 React 树的根 DOM 容器中
> 等等
> ```

啥原理：

> React 上注册的事件最终会绑定在document这个 DOM 上，而不是 React 组件对应的 DOM(减少内存开销就是因为所有的事件都绑定在 document 上，其他节点没有绑定事件，React17事件委托的变更 React 树的根 DOM 容器中)
>
> https://img-blog.csdnimg.cn/img_convert/945dd88ba1f47ecac1b9f27c15d8b312.png 
>
> 为啥升级
>
> ```
> const Search = function() 
> {
> 	const handleClick = (e) => {
>   e.stopPropagation();
> 	}, 
> 	return <input onClick={this.handleClick} /> 
> 
> 	document.addEventListener('click', function() {
>   里面通过表示判断是当前input点击才会触发
> }, false);
> }
> 
> document.addEventListener('click', function() {
> console.log('propagation')
> }, false);
> ```

和原生区别

> 1、事件名称命名方式不同
>
> ```
> 原生事件命名为纯小写（onclick, onblur），而 React 事件命名采用小驼峰式（camelCase），如 onClick 等
> // 原生事件绑定方式
> <button onclick="handleClick()">+1</button>
> // React 合成事件绑定方式
> const button = <button onClick={handleClick}>+1</button>
> ```
>
> 2、事件处理函数写法不同
>
> ```
> 原生事件中事件处理函数为字符串，在 React JSX 语法中，传入一个函数作为事件处理函数。
> // 原生事件 事件处理函数写法
> <button onclick="handleClick()">+1</button>
> // React 合成事件 事件处理函数写法
> const button = <button onClick={handleClick}>+1</button>
> ```
>
>   3. 阻止默认行为方式不同
>
> ```
> 在原生事件中，可以通过返回 false 方式来阻止默认行为，但是在 React 中，需要显式使用 preventDefault() 方法来阻止
> // 原生事件阻止默认行为方式 神龙教主
> <a href="http://www.mobiletrain.org/"
> onclick="console.log('阻止原生事件'); return false"
> >
> 阻止原生事件
> </a>
> 
> // React 事件阻止默认行为方式
> const handleClick = e => {
> e.preventDefault();
> console.log('阻止原生事件~');
> }
> const clickElement = <a href="http://www.mobiletrain.org/" onClick={handleClick}>
> 阻止原生事件
> </a>
> ```





# 💘 day3

# 🐝🐝🐝react中如何解决样式污染问题

方案1：Inline styling    行内样式

方案2：CSS Modules	      默认（不可能的）

方案3：SASS/LESS Modules		  UMI推荐

方法4：Styled Components CRA推荐 实战相对少





# 🐝🐝🐝数组常用方法、数组去重至少写3种方案 

二阶段面试题一堆



# 🐝🐝🐝为什么循环的时候要写key

1-提升性能

2-避免出现不可控bug



在 React 中，当我们使用循环渲染列表时，需要给每个列表项添加一个唯一的 `key` 属性，这是因为 React 在进行渲染时会利用 `key` 属性来判断哪些元素是新增的、哪些元素是删除的，从而进行最小化的 DOM 操作，提高性能。

具体来说，当列表项的顺序发生变化时，如果没有指定 `key` 属性，React 可能会将一个旧的列表项误认为是新的列表项，从而导致 DOM 操作不必要的重复。此外，如果列表项的顺序不变，但是有一些项被删除或添加，如果没有指定 `key` 属性，React 可能会将一个旧的列表项误认为是新的列表项，从而导致 DOM 操作不必要的重复。

因此，为了保证 React 渲染列表时的正确性和性能，需要给每个列表项添加一个唯一的 `key` 属性，通常使用列表项的 ID 或索引作为 `key` 属性的值，从而让 React 能够准确地识别每个列表项，进行最小化的 DOM 操作。神龙教主





# 🐝🐝🐝谈谈你对受控组件、和非受控组件的理解

受控组件：通过react控制表单的输入输出

非受控组件：通过DOM操作表单数据



# 🐝🐝🐝如何实现组件通信

父传子：props

父传子：children

子传父：调用父的方法

兄弟：状态提升

组件实例：ref    =》 属于ref转发、ref引用实现组件通信

children属性 =》也是父传子 超文本

context

状态管理工具：redux、redux-toolkit(RTK)、mobx等

等等





# 🐝🐝🐝项目跨域是如何解决的？

> 在vue中

a 在根目录创建vue.config.js （不用安装

```
module.exports = {
    devServer: {
        proxy: {  //配置跨域
          '/api': {
            target: 'http://kg.zhaodashen.cn/v2/', 
            changOrigin: true,  //允许跨域
            pathRewrite: {
              '^/api': '' 
            }
          },
        }
    },
}
```

b 修改api baseURL   /api前缀



> 在react中

a 安装模块

```
yarn add http-proxy-middleware@0.19.1 -D
或
cnpm i http-proxy-middleware@0.19.1 -D
```



b 在src目录创建src/setupProxy.js

```
const proxy = require("http-proxy-middleware");

module.exports = function (app) {
  app.use(
    proxy("/api", {
      target: "http://kg.zhaodashen.cn/mt/admin/", // 目标服务器网址
      changeOrigin: true, // 是否允许跨域
      secure: false, // 关闭SSL证书验证HTTPS接口需要神龙教主
      pathRewrite: {
        // 重写路径请求
        "^/api": "",
      },
    })
  );

  // ...
};

```

c  修改api baseURL   /api前缀







# 💘 day4

# 🐝🐝🐝react生命周期有哪些&应用场景

```
单词															触发机制 			    应用场景

挂载
constructor						  				 首次					  	初始化ref、state等属性
static getDerivedStateFromProps  首次&状态/属性	    较少，监控props更新state
componentWillMount				   		 首次			      		弃1
render							  				  	首次&状态/属性    渲染页面
componentDidMount				   		   首次				 		   异步请求、操作DOM 如echarts、swiper

更新属性/状态

static getDerivedStateFromProps   首次&状态/属性		较少，监控props更新state
componentWillReceiveProps		   		仅属性				  	弃2
shouldComponentUpdate   		   		属性/状态					子组件减少渲染次数  性能优化
componentWillUpdate				   			属性/状态					弃3
render							  						首次&状态/属性		 渲染页面
getSnapshotBeforeUpdate			   		属性/状态	     DOM更新前收集DOM信息交给componentDidUpdate
componentDidUpdate				   			属性/状态			监控更新进一步操作DOM、聊天、echarts

卸载
componentWillUnmount			    		组件卸载			清除非react资源 例如登陆定时器

错误
componentDidCatch				   				后代组件发错异常错误
```





问1：react生命周期有哪些

答1：挺多的挂载、更新、卸载等等，然后我常用的就是componentDidMount

问2：具体呢

答2

```
componentWillMount
render
componentDidMount

componentWillUpdate
render
componentDidUpdate

componentWillUnmount
...
```





# 🐝🐝🐝react16.3新增了哪些、弃用了哪些

## 

新增

```
单词						      						触发机制  	    场景
static getDerivedStateFromProps   首次&属性/状态    案例较少，主要监控props变化更新state用    
getSnapshotBeforeUpdate			 		  属性/状态        案例更少，在更新DOM之前收集DOM信息
```

弃用

```
componentWillMount				   	  首次			   		 弃1
componentWillReceiveProps		   	仅属性				  	弃2
componentWillUpdate				   		属性/状态					弃3
```



# 🐝🐝🐝react用来优化性能的是哪一个生命周期，说一下实战如何优化使用

shouldComponentUpdate

避免父组件更新状态或者属性后避免子组件不必要渲染



# 🐝🐝🐝父组件更新状态或者属性如何避免子组件不必要渲染

通过shouldComponentUpdate

或者直接继承PureComponent



# 🐝🐝🐝说出新增的生命周期各自应用场景

```
单词						      						触发机制  	    场景
static getDerivedStateFromProps   首次&属性/状态    案例较少，主要监控props变化更新state用    
getSnapshotBeforeUpdate			 		  属性/状态        案例更少，在更新DOM之前收集DOM信息
```





# 🐝🐝父子组件mount生命周期执行顺序  
# 🐝🐝父子组件update生命周期执行顺序

```
父子嵌套生命周期（一般个1~2个概率）
	mount 首次刷新或者组件销毁后重新创建**
		f will mount
		f render
			s will mount
			s render
			s did mount
		f did mount
	update 
		f will update
		f render
			s will receive props
			s will update
			s render
			s did update
		f did update
		
生命周期形参了解：仅给你传递意识 
```



 

# 💘 day5 Hooks

# 🌛 谈谈你对hooks理解

React Hooks 是 React 16.8 版本中引入的一项新特性，它可以让我们在函数组件中使用 React 的状态和生命周期等功能，从而减少类组件的使用，使代码更加简洁和易于维护。神龙教主

具体来说，Hooks 提供了一些特殊的函数，如 `useState`、`useEffect`、`useContext` 等，这些函数可以让我们在函数组件中使用状态、副作用和上下文等功能。使用 Hooks，我们可以：

1. 状态管理：通过 `useState` 函数，可以在函数组件中管理状态，而不需要使用类组件的 `this.state`。`useState` 接受一个初始状态值，返回一个数组，其中第一个元素是当前状态值，第二个元素是用于更新状态的函数。可以使用解构赋值来获取这两个值。
2. 副作用处理：通过 `useEffect` 函数，可以在函数组件中处理副作用，如访问 API、更新 DOM 等。`useEffect` 接受两个参数，第一个参数是一个函数，用于执行副作用，第二个参数是一个数组，用于指定依赖项。当指定的依赖项发生变化时，`useEffect` 中的函数将被重新执行。
3. 上下文传递：通过 `useContext` 函数，可以在函数组件中获取上下文信息，而不需要使用类组件的 `static contextType`。`useContext` 接受一个上下文对象，返回上下文中的值。

Hooks 还提供了一些其他函数，如 `useReducer`、`useCallback`、`useMemo`、`useRef` 等，这些函数可以让我们在函数组件中实现更复杂的逻辑和功能。

使用 Hooks 的优点是它能够使代码更加简洁和易于维护，避免了类组件中的一些繁琐的操作，如生命周期函数、this 绑定等。同时，Hooks 也能够提高代码的可读性和可测试性，使代码更加模块化和可复用。

不过，在使用 Hooks 时需要注意，它有一些规则和限制，如只能在函数组件的最顶层使用 Hooks，不能在循环和条件语句中使用 Hooks 等。另外，Hooks 也需要考虑到性能问题，避免过多地进行不必要的副作用和状态更新。



# 🌛 用hooks 意义

使用 Hooks 的主要意义在于它可以让我们在函数组件中使用 React 的状态、生命周期和其他功能，从而减少类组件的使用，使代码更加简洁和易于维护。

在之前的 React 版本中，我们只能通过类组件来管理状态和处理生命周期等功能。而使用类组件有一些缺点，如需要继承 React.Component、需要在构造函数中绑定 this、需要在生命周期函数中处理副作用等。这些操作使代码变得繁琐和难以理解，同时也容易出现错误。

而使用 Hooks，我们可以直接在函数组件中管理状态和处理副作用等功能，避免了类组件的一些繁琐操作。同时，Hooks 也能够提高代码的可读性和可测试性，使代码更加模块化和可复用。

除此之外，使用 Hooks 还有以下一些优点：

1. Hooks 可以使代码更加简洁和易于维护。
2. Hooks 可以提高代码的可读性和可测试性。
3. Hooks 可以避免一些常见的错误，如忘记绑定 this、在副作用函数中忘记清理等。
4. Hooks 可以使代码更加模块化和可复用，减少了代码的耦合度。

总之，使用 Hooks 可以使我们的代码更加简洁、易于维护、可读性和可测试性更好，同时也可以避免一些常见的错误，提高代码的质量和可靠性。



# 🐝🐝🐝 hook种类

1. useState：用于在函数组件中添加状态管理功能。
2. useEffect：用于在函数组件中处理副作用，如数据请求、事件监听等。
3. useContext：用于在函数组件中访问上下文数据。
4. useReducer：用于在函数组件中实现复杂的状态管理，类似于 Redux。
5. useCallback：用于在函数组件中缓存回调函数，避免无用的重新渲染。
6. useMemo：用于在函数组件中缓存计算结果，避免重复计算。
7. useRef：用于在函数组件中访问 DOM 元素或保存其他数据。
8. useLayoutEffect：类似于 useEffect，但会在 DOM 更新之前同步调用回调函数。
9. useImperativeHandle：用于在父组件中访问子组件的实例方法。
10. useDebugValue：用于在开发阶段输出调试信息。

这些 Hooks 种类可以使函数组件具有类似于类组件的功能，使得函数组件在处理状态、生命周期、副作用等方面更加灵活和强大。同时，Hooks 也可以帮助我们避免一些常见的错误和降低代码的耦合度，从而提高代码的可维护性和可读性。





除了常用的 Hooks 种类，还有一些其他的 Hooks 可以用于特定的场景：

1. useReducerWithMiddleware：用于在 useReducer 中实现中间件，类似于 Redux。
2. useEventCallback：用于在函数组件中缓存事件回调函数，避免因为闭包引用导致的性能问题。
3. useInterval：用于在函数组件中实现定时器功能。
4. useDebounce：用于在函数组件中实现防抖功能。
5. useThrottle：用于在函数组件中实现节流功能。
6. useAsync：用于在函数组件中实现异步请求的状态管理。
7. useIntersectionObserver：用于在函数组件中观察元素的可见性状态。
8. usePrevious：用于在函数组件中缓存上一次的状态值。神龙教主

这些 Hooks 可以帮助我们更加方便地处理特定的场景，提高代码的复用性和可读性，同时也可以使得函数组件具有更加强大和灵活的功能。除了以上列举的 Hooks，还有很多其他的自定义 Hooks 可以根据实际需求来编写，从而使得函数组件的编写更加方便和高效。





以下是一些较为高级的 React Hooks：

1. useLayout：用于获取组件的布局信息，包括宽度、高度、位置等。
2. useVirtualList：用于优化长列表的性能，只渲染可见区域的部分数据。
3. useMedia：用于根据媒体查询动态调整组件的样式或行为。
4. useDrag：用于实现拖拽功能，可以获取拖拽的状态、位置等信息。
5. useDrop：用于实现拖放功能，可以获取拖放目标的状态、位置等信息。
6. useTransition：用于实现平滑的动画效果，可以控制组件在进入、退出、更新时的动画效果。
7. useImmer：用于在函数组件中实现不可变数据的更新，类似于 Immer 库。
8. useSpeechRecognition：用于实现语音识别功能，可以获取用户的语音输入并进行相应的处理。
9. useBattery：用于获取设备的电池信息，包括电量、充电状态等。神龙教主

这些高级的 React Hooks 可以帮助我们实现更加复杂和灵活的功能，同时也能够避免一些常见的错误和提高代码的可维护性和可读性。但是需要注意的是，使用这些高级 Hooks 需要具有一定的 React 和 JavaScript 基础知识，并且需要根据具体场景来选择和使用合适的 Hooks。



# 🐝🐝🐝 自己封装过哪些hook

1. useLocalStorage：将数据存储到本地存储中，包括设置、获取和删除数据。 神龙教主

```
import { useState, useEffect } from 'react';

function useLocalStorage(key, initialValue) {
  const [value, setValue] = useState(() => {
    const storedValue = window.localStorage.getItem(key);
    return storedValue ? JSON.parse(storedValue) : initialValue;
  });

  useEffect(() => {
    window.localStorage.setItem(key, JSON.stringify(value));
  }, [key, value]);

  const removeValue = () => {
    window.localStorage.removeItem(key);
  };

  return [value, setValue, removeValue];
}

export default useLocalStorage;

```

2. useDebounce：防抖动 Hook，用于在用户输入停止后延迟一段时间再执行函数。

```
import { useState, useEffect } from 'react';

function useDebounce(value, delay) {
  const [debouncedValue, setDebouncedValue] = useState(value);

  useEffect(() => {
    const timeout = setTimeout(() => {
      setDebouncedValue(value);
    }, delay);

    return () => {
      clearTimeout(timeout);
    };
  }, [value, delay]);

  return debouncedValue;
}

export default useDebounce;

```

3. useFetch：用于获取数据的 Hook，包括加载中、错误和数据三种状态。

  ```
  import { useState, useEffect } from 'react';
  
  function useFetch(url) {
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState(null);
    const [data, setData] = useState(null);
  
    useEffect(() => {
      async function fetchData() {
        try {
          const response = await fetch(url);
          const json = await response.json();
          setData(json);
          setLoading(false);
        } catch (error) {
          setError(error);
          setLoading(false);
        }
      }
      fetchData();
    }, [url]);
  
    return [data, loading, error];
  }
  
  export default useFetch;
  
  ```

4. useForm：用于处理表单数据的 Hook，包括设置、获取和重置表单数据。

```
import { useState } from 'react';

function useForm(initialValues) {
  const [values, setValues] = useState(initialValues);

  const handleChange = (event) => {
    const { name, value } = event.target;
    setValues((prevValues) => ({ ...prevValues, [name]: value }));
  };

  const resetForm = () => {
    setValues(initialValues);
  };

  return [values, handleChange, resetForm];
}

export default useForm;

```



