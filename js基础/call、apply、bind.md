### js中call()、apply()、bind()的区别及用法

#### 1.区别

##### 1.1三者的相同点：都是用来改变this的指向

##### 1.2call()和apply()的区别：

> 相同点：都是调用一个对象的一个方法，用另一个对象替换当前对象(功能相同)
>
> 例如： B.call(A, args1, args2);即A对象调用B对象的方法
>
> F.apply(G, arguments);即G对象应用F对象的方法
>
> 不同点：参数书写方式不同
>
> call()的第一个参数是this要指向的对象，后面传入的是参数列表，参数可以是任意类型，当第一个参数为null, undefined的时候，默认指向window;
>
> apply()：第一个参数是this要指向的对象，第二个参数是数组
>
> 

##### 1.3call()和bind()的区别

> 相同点：都是用来改变this的指向
>
> 不同点：call()改过this的指向后，会再执行函数，bind()改过this后，不执行函数，会返回一个绑定新this的函数

```javascript
function f() {
  console.log("看我怎么被调用")
  console,log(this)  //指向this
}
var obj = {}
f.call(obj)  //直接调用函数
var g = f.bind(obj)   //bind()不能调用函数
g()  //此时才调用函数
```

#### 2.用法

##### 2.1call()的应用

###### 2.1.1利用call()判断函数类型

```javascript
//在判断数据类型时使用typeof，一般不是太准确，可以使用Object.prototype.toString.call()方法来判断一个数据的数据类型
console.log(Object.prototype.toString.call(12))    //[onject Number]
```

我们可以利用上面的输出的内容进行封装一个函数，以达到判断输入数据的基本类型

```javascript
function getType(a) {
  var obj = Object.prototype.toString.call(a)   //区分对象类型，确定当前类型的数据的类型
  var sub = obj.substr(8)      //console.log(sub)   String]
  //stringObject.substr(start, length)  start要抽取的字符串的起始下标
  //length截取的长度，如果不写则表示从start开始截取到最后，stringObject表示某一串字符串
  var len = sub.length
  var sub = sub.substr(0, len - 1)      // String
  var rs = sub.toLowerCase(sub)  //转换为小写
  return rs
}
console.log(getType("a"))    //string
```

###### 2.1.2利用call()翻转字符串

```javascript
//思路：将字符串转化为数组，借用数组中的reverse,将字符串翻转过来
var str = "abcdefg"
console.log(Array.prototype.reverse.call(str))  //此时会报错误，即引用类型错误，就是说只有数组才能使用reverse这个方法(错误写法)
//方法一：这种方法内有使用call()    Array.from()方法就是将一个类数组对象或者可遍历对象转换为一个真正的数组
var arr = Array.from(str).reverse().join("")  
console.log(arr) //gfedcba
console.log(typeof arr) //string
//方法2
var rs = Array.prototype.reverse.call(str.splice("")).join("")
//splice(start, length)方法用于把一个字符串分割成字符串数组，start表示从指定的地方分割字符串,length表示被分割的长，返回一个一个字符串数组，如果把空字符串("")用为参数那么字符串中的每个字符之间都会被分割
console.log(rs); //gfedcba
console.log(typeof arr) //string
```

##### 2.2apply()的应用

###### 2.2.1利用apply()求最大值

```javascript
var arr = [2,6,8,3,4,9,7,23,56,889]; 
console.log(Math.max.apply(arr, arr))  
//Math是一个对象，并不是构造器
//第一个arr表示让arr借用max这个方法，第二个arr表示传给max的数据
//apply()所执行的操作：1.执行Math.max(1,2,3,5,4)  2.把内部的this改成arr
```

