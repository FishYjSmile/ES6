## ES6新特性

 

let

　　块级作用域 ：只在{ // 只在此块级作用域内有效，如果有嵌套会向外继续查找 }
　　不影响作用域链的效果 ： { // 会逐层向上查找 }
　　用var执行循环并给予事件回调时，此时实践的回调值会根据循环体结束的最终值作为回调的取值
　　　　　　例如：此时的事件回调函数会向外进行查找i，找window.i ，window.i此时等于3 ，

　　　　　　类似于    {  var i = 0  } {  var i = 1  } {  var i = 2  } {  var i = 3  }  因为var没有块级作用域概念，所以此时的var i = 3 覆盖了前面的i值

　　　　　　由此通过将var 改为 let 即可解决这个问题， {  let i = 0  } {  let i = 1  } {  let i = 2  } {  let i = 3  }  ，块级作用域互不影响

　　　　　

 

 

 

 const

　　一定要赋初值
　　一般常量使用大写
　　  常量的值不可修改
         块级作用域
　　对于数组和对象的元素修改，不算是对常量的修改，不报错（常量所指向的地址没有发生变化）例如
　　　　　　

 

 解构解析

　　允许按照一定模式从数组和对象中提取值，可对变量进行赋值  例如：
对数组的解构此时可以对变量进行赋值
　　　　　　

 

 

 对对象的解构　　
　　　　　　

 

 

 

 

模板字符串

　　反引号 ` `  也可用于声明字符串
　　可以直接出现换行符回车等（在单引号和双引号中需要用+进行拼接）
　　变量的拼接例如：let a = '123'    let out  =  `${a}2222222`   可以更加简便的拼接

 

 

 

简化对象的写法

 

　　ES6允许在大括号里直接写入变量和函数，作为对象的属性和方法


 　　简写方法，直接在对象中定义方法不用在improve:function(){}
　　　　　　

 

 

 

 箭头函数

 

　　this 是静态的   this  始终3指向函数声明时所在的作用域下的this的值
　　此时通过call方法改变this的指向，第一个输出为ATGUIGU   ,第二个输出为尚硅谷，
　　采用箭头函数不改变this的指向，（函数在声明时所在作用域下this的值）此时仍是window.name的值
 

 

 

 　　不可作为构造函数实例化对象
　　此时将Person箭头函数作为构造器程序会报错


 

 

 　　不可使用arguments 变量 （保存实参对象，输出为实参属性和length属性等）
 

 

　　此时程序报错undefined


 

 

 适合运用的场景
　　与this无关的回调   定时器   数组的方法回调（arr.filter（function（）{}））回调返回为真的值，返回给arr数组
 不适合的场景
　　与this有关的回调    事件回调    对象的方法
 

 函数参数默认值

 

形参初始化（给形参赋一个初始值）
　

与解构赋值结合


 

 

 

 

 rest参数（放在形参内）

用于保存实参，意义与ES5中的arguments类似，（rest参数返回是数组，arguments返回的是对象）


 

 

 

rest参数必须放到参数最后
 

 

 

拓展运算符（放在函数调用的实参内）

【...】拓展运算符可将数组转换为逗号分隔的参数序列，最终输出的arguments存在数组中的每个项


 

 

运用
　　数组的合并


 

　　数组的克隆（如果有运用数据类型的话是浅拷贝）


 

　　将伪数组转为真正的数组（伪数组无法直接调用数组中的那些方法）
 

 

 

Symbol（表示独一无二的值，是一种新的原始数据类型）

值是唯一的，用于解决命名冲突的问题
值不能与其他数据类型进行运算（四则运算等）
定义的对象属性不能使用for...in 循环遍历，可以使用Reflct.ownKeys 来获取对象的所有键名
创建Symbol
　　Symbol()    ，此时的Symbol中的字符串为标识值，在测试是否相等时s2 === s3  结果为false


 

 

　　 Symbol.for()     ，此时的Symbol中的字符串为标识值，在测试是否相等时s4 === s5  结果为true


 

 

 

数据类型   USONB
　　　　U： undefined

　　　　S： string    symbol

　　　　O： object

　　　　N： number    null

　　　　B： boolean

 

作用
　　给对象添加方法，此时不确定game中是否有up 和down方法，由此利用symbol给对象添加方法（具有唯一性）
　　

 

 

 

 此时在对象中添加方法，且键唯一可以利用Symbol()   ，因为symbol()是一个动态的值，所以这里加上中括号就可以利用symbol的唯一性

 

Symbol内置值  （11个内置，改变对象在特定场景下的表现，拓展对象概功能）
　Symbol.hasInstance  　　       其他对象使用instanceof 运算符，判断是否为该对象的实例时 会调用这个方法

 

 

　Symbol.isConcatSreadable 使用concat函数时 用于控制结果是否可以展开 ，此时为false不可展开



 

   Symbol.unscopables          使用with关键字时，哪些属性会被with环境排除
   Symbol.match                    使用match方法时调用
   Symbol.replace                  使用replace方法时调用
   Symbol.search                   使用search方法时调用
   Symbol.split                       使用split方法时调用
   Symbol.iterator                  对象进行for...of循环时，调用
   Symbol.toPrimitive
   Symbol.toStringTag           使用tostring方法时，返回该方法的返回值
   Symbol.species                  创建衍生对象时，使用该属性
迭代器 

for...of循环   通过消费Iterator接口来使用本循环，具有Iterator接口的如下：
　　Array
　　Arguments
　　Set
　　Map
　　String
　　TypedArray
　　NodeList
Iterator接口对应的是符合条件的数组或者其他存在Symbol(Symbol.iterator)这个属性
　　

 

 

 工作原理：
　　创建一个指针对象，指向当前数据结构的起始位置

 

 

　　第一次调用对象的next方法，此时指针自动指向数据结构的第一个成员
　
 

 

 

 

 

不断调用next方法，指针一直后移，直到指向最后一个成员
　　
每调用next方法 返回一个包含 value和 done属性的对象
　
 

 

for...in 循环和for...of 循环的区别  for...in 保留的是键名   for ... of  保留的是键值
　　

 

 

 



 

 

 

 需要自定义编译数据的时候，可以使用迭代器
　　例如在对象中声明了一个数组，选中想要遍历这个数组作为for...of的返回结果的话，此时需要编写Symbol.iterator
       此时的对象中并没有Symbol(Symbol.unscopables)属性

 

需要创建Symbol(Symbol.unscopables)属性

复制代码
t2[Symbol.iterator] = function(){
    let index = 0
    let _this = this
    return {
        next:function(){
            if(index < _this.arr.length){
                const result = { value:_this.arr[index],done:false}
                index ++
                return result
            }else{
                return {value:undefined,done:true}
            }
        }
    }
}       
复制代码
for(let i of t2){
    console.log(i)  //qwe   ert   dfs
}




　　　　

生成器函数

　　作用于异步编程
　　此时 需要使用   *  
　　在执行此生成器函数时，实际上是迭代器对象，里面有一个next方法   ，实际的运行可以借助于next方法


      可以使用yield来作为分隔符，再借由next方法来执行，例如：
　　

 

 

 　可以借由for...of方法来遍历yield里的值，因为此时迭代器里next方法返回的对象的value值是yield里面的值　　　　　
　　　　　　

 

 

 

生成器函数参数
　可以对生成器函数传入形参，此时调用生成器函数想要输出形参传入值，一定要先执行next方法才行，对于next方法也可以传入参数，将作为上一个yield的返回结果返回


 

 

 

 

 

 

 

 

  可以解决回调地狱的问题，此时创建三个异步执行函数，通过创建生成器函数，并设置代码块yield，最后执行该生成器函数，执行生成器函数的next方法
　

 

 

 

模拟实际场景，先执行one返回结果再执行two、three，结合使用next方法传入实参作为上一个yield的返回结果的特性
 

复制代码
function getone(){
    setTimeout(()=>{
        let data = 'one'
        iterator.next(data)
    },1000)
}

function gettwo(){
    setTimeout(()=>{
        let data = 'two'
        iterator.next(data)
    },1000)
}

function getthree(){
    setTimeout(()=>{
        let data = 'three'
        iterator.next(data)
    },1000)
}
function * gen(){
    let one = yield getone()
    console.log(one)

    let two = yield gettwo()
    console.log(two)

    let three = yield getthree()
    console.log(three)}   

let iterator = gen()
iterator.next()           //第一个next

// one
// two
// three 
复制代码
 

 

Promise 对象

 异步请求到的数据成功则执行resolve方法并将参数传递，失败则执行reject方法并将失败参数传递，其中有.then方法，里面有2个参数，第一个是成功的function，第二个是失败的function

 

 

 

 

 

 

 

ajax请求


 

 

 

 

Promise封装ajax请求


 

 

　　Promise可以使用  .then 方法来进行链式调用


 

 

      回调地狱的解决，此时先通过new一个Promise读取第一个文件的内容resolve(data)将Promise置为resolve成功，此时通过then获取的value是第一个文件内容，再通过第一个then方法执行回调函数返回一个Promise对象，并且该Promise对象读取第二个文件的内容，并且resolve（将第一个文件内容和第二个文件内容结合），作为第二个Promise的成功的返回结果，此时第二个Promise的返回为真，此时第二个then方法执行，此时的value为第一个文件和第二个文件内容的结合


 

 

Set（集合）

Set会自动去重


 

 

 

查看集合长度通过size


 

 

 

 添加集合使用add方法


 

 

 

 删除集合元素delete方法


 

 

 

检测集合中是否含有某元素has方法


 

 

 

清空集合clear方法


 

 

 

集合实现了Symbol(Symbol.iterator)由此可以使用for...of方法遍历


 

 

 

 

set的实际
　　数组去重（通过set集合的去重特性，以及使用拓展运算符[]）


 

 

 

　　求交集（通过先将第一个数组去重变为集合，再将此集合利用fliter方法，该方法如果返回为true就保留，否则就移除，再通过将arr2转为集合并去重，再利用has来进行判断该元素是否在集合里）

简化写法

 

 

 

　　求并集（先将两个数组进行合并操作，在将合并后的结果转为集合即可,并将该集转换为数组即可）

 

 

 

 

   

　　求差集
 
 

 

Map（键值对集合）

声明Map

添加元素set方法（第一个参数是键，第二个是值）键和值可以是函数、对象、数组、字符串都可以


删除delete方法


 

 

获取get方法


 

 

清空clear方法
 

Map中含有Symbol(Symbol.iterator) 由此可以使用for...of方法遍历
　　　　每一个返回结果是一个数组，数组中存放的是键、值的形式

 

Class

可以创建构造函数和实例化对象
　　ES5写法：



 

 　ES6 利用Class的写法：

（通过此时要使用constructor来创建构造函数，当执行实例化对象时  此时会执行constructor，方法的定义直接在class里面声明方法即可）



 

函数对象的属性与实例对象不相通    （对于用static静态属性标注的属性和方法是属于类，不属于实例化对象）例如：

复制代码
class test{
    static name = '123'
    static change(){
        console.log('555')
    }
}

let t1 = new test()
t1.name
// undefined
t1.change()
// error
test.name
// "123"
test.change()
// 555
复制代码
 

对象继承

ES5类的继承
复制代码
function Phone(brand,price){ 
    this.brand = brand
    this.price = price
}
Phone.prototype.call = function(){  // 传入原型方法
    console.log('111111')
}

function SmartPhone(brand,price,color,size){ 
    Phone.call(this,brand,price)   // 利用call方法改变此时的this指向的是SmarPhone
    this.size = size
    this.color = color 
}

SmartPhone.prototype = new Phone() // 创建实例化对象，并继承于
SmartPhone.prototype.constructor = SmartPhone  // 构造器

SmartPhone.prototype.photo = function(){  // 创建方法
    console.log('22222')
}

let t2 = new SmartPhone(1,2,3,4)  // 创建实例化对象
console.log(t2)

可以发现实例化属性继承完成，并且原型链中有继承父类的call方法
SmartPhone {brand: 1, price: 2, size: 4, color: 3}
brand: 1
color: 3
price: 2
size: 4
[[Prototype]]: Phone
brand: undefined
constructor: ƒ SmartPhone(brand,price,color,size)
photo: ƒ ()
price: undefined
[[Prototype]]: Object
call: ƒ ()
constructor: ƒ Phone(brand,price)
[[Prototype]]: Object
复制代码


 

 

 

ES6类的继承
复制代码
class Phone{
    constructor(brand,price){ 
    this.brand = brand;
    this.price = price
    } 
    call(){      // 实例化方法在constructor方法外创建
        console.log('1111')
    }
}

class SmartPhone extends Phone {
    constructor(brand,price,color,size){
        super(brand,price)   // 这里调用父类的构造方法 ，相当于调用Phone.call(this,brand,price)
        this.color = color 
        this.size = size 
    }
    phone(){      // 实例化方法在constructor方法外创建
        console.log('22222')
    }
}

const t3 = new SmartPhone('123',56,78,123)
console.log(t3)

SmartPhone {brand: "123", price: 56, color: 78, size: 123}
brand: "123"
color: 78
price: 56
size: 123
[[Prototype]]: Phone
constructor: class SmartPhone
phone: ƒ phone()
[[Prototype]]: Object
call: ƒ call()
constructor: class Phone
[[Prototype]]: Object
复制代码


 

 

 

子类重写父类的方法

声明和父类同名的方法，以上例为例，在SmartPhone中声明一个和父类同名的call方法

 

class中的get  和 set 方法

get
复制代码
class Phone{
    get price(){
        console.log(123)
        return '5567'  // 此时的返回值作为函数调用的返回值，不设置为undefined
    } 
}

let s = new Phone()

console.log(s.price)
// 123
// 5567  
复制代码
 

set
复制代码
class Phone{
    set price(val){           // 要传入一个参数，此时的参数作为返回值
        console.log(7789)
    }
}

let s = new Phone()
console.log(s.price = '123')
// 7789
// 123
复制代码
 

数值拓展（Number.EPSILON 最小精度2.220446049250313e-16）



 

 

 　　第一个输出为 false

　　 第二个输出为 true

 

ES6关于数值拓展的方法

Number.isNaN（用于检测数值是否为NaN）
Number.parseInt  NumberparseFloat（用于将字符串转换为数值，开头必须是数字，只取从有数值时开始，到没有数值时结束）
Number.isInteger（用于检测数值是否为整数）
Math.trunc（将数字的小数部分抹去）
Math.sign（用于检测数值是正式、负数、还是零  返回值分别为 1 -1 0）
 

对象方法拓展

Object.is（用于判断两个值是否完全相等    类似于  === ）
 

　　但是有一点区别，例如：NaN === NaN  => false     Object.is(NaN,NaN)  =>  true
 

 

Object.assign（用于对象的合并，传入2个参数，后面的将前面已有的属性覆盖）
 

Object.setPrototypeOf  Object.getPrototypeOf  （设置原型对象）
 

模块化

export  暴露   import    引入

 

分别暴露


 

 统一暴露（对象的方式，将待暴露变量或方法写入）


 

 

默认暴露（调用时返回的是default对象，需要引用其方法）


 

 

解构赋值形式引入（当出现同名时可以使用别名 as）
 

 

 

 

简便形式（只针对默认暴露形式）


 

 

 幂运算

ES7中引入的新方法是   ** 

console.log(2**10)
// 1024

console.log(Math.pow(2,10))
// 1024
 

ES8中最要的新特性 async  和  await

async 函数

1.返回结果是Promise对象   

2.Promise对象的结果由async函数执行的返回值决定

 

声明为async的函数，返回一个 Promise对象 可以调用.then方法 



 

 

 

await 表达式

1.await 要放在 async 函数中

2.await 右侧的表达式一般为Promise对象

3.await 返回的是Promise成功的值

4.await 的Promise失败了，就会抛出异常，需要通过 try ... catch 捕获

复制代码
const p = new Promise((resolve,reject)=>{resolve("123456")})
undefined
async function main(){
    let result = await p    // await 右边是一个Promise对象，返回结果是Promise对象成功的值
    console.log(result)
}
undefined
main()

// 123456
复制代码
 



 

 

 

结合async 和 await 发送ajax请求

先对promise   then 封装 ajax请求，再由async 和 await（右边为Promise对象）



 


 



 
