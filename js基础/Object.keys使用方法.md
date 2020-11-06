Object.keys(obj) 参数：要返回其枚举自身属性的对象  返回值：一个表示给定对象的所有可枚举属性的字符串数组

- 处理对象，返回可枚举的属性数组

  ```javascript
  let person = { name:"张三", age:26, address:"广州", getPhone:function(){} }
  Object.keys(person) //["name", "age", "address", "getPhone"]
  ```

- 处理数组，返回索引值数组

  ```javascript
  let arr = [1,2,3,4,5,6]
  Object.keys(arr)   //["0", "1", "2", "3", "4", "5"]
  ```

- 处理字符串，返回索引值数组

  ```javascript
  let str = "wasdr字符串"
  Object.keys(str) //["0", "1", "2", "3", "4", "5", "6", "7"]
  ```

  ##### 常用技巧

  ```javascript
  let person = { name:"张三", age: 26, address: "广州", getPhone: function(){} }
  Object.keys(person).map((key) => {
    person[key]   //获取到属性对应的值，做一些处理
  })
  ```

  #### PS：Object.values()和Object.keys()是相反的操作，把一个对象的值转换为数组

  