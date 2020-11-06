```javascript
function deepCopy(obj, cache = new WeakMap()) {
  if (!obj instanceof Object) return obj
  //防止循环利用
  if (cache.get(obj)) return cache.get(obj)
  //支持函数
  if (obj instanceof Function) {
    return function () {
      obj.apply(this, arguments)
    }
  }
  //支持日期
  if (obj instanceof Date) return new Date(obj)
  //支持正则对象
  if (obj instanceof RegExp) return new RegExp(obj.source, obj.flags)
  //数组是key为数字索引的特殊对象
  const res = Array.isArray(obj) ? [] : {}
  //缓存copy的对象，用于处理循环引用的情况
  cache.set(obj, res)
  Object.keys(obj).forEach((key) => {
    if (obj[key] instanceof Object) {
      res[key] = deepCopy(obj[key], cache)
    } else {
      res[key] = obj[key]
    }
  })
  return res
}
//测试
const source = {
  name: 'Jack',
  meta: {
    age: 12,
    birth: new Date('1997-10-10'),
    ary: [1,2,{ a: 1 }],
    say() {
      console.log('Hello')
    }
  }
}
source.source = source
const newObj = deepCopy(source)
console.log(newObj.meta.ary[2] === source.meta.ary[2])
```

