## 1、浅拷贝
有时候我们只是想备份数组，但是只是简单让它赋给一个变量，改变其中一个，另外一个就紧跟着改变，但很多时候这不是我们想要的。

```
var obj = {
    name:'wsscat',
    age:0
}
var obj2 = obj;
obj2['c'] = 5;
console.log(obj);//Object {name: "wsscat", age: 0, c: 5}
console.log(obj2);//Object {name: "wsscat", age: 0, c: 5}
```


## 2、深拷贝
解决上面的办法有4种：
### （1）slice


```
var arr = ['wsscat', 'autumns', 'winds'];
var arrCopy = arr.slice(0);
arrCopy[0] = 'tacssw'
console.log(arr)//['wsscat', 'autumns', 'winds']
console.log(arrCopy)//['tacssw', 'autumns', 'winds']
```


### （2）concat


```
var arr = ['wsscat', 'autumns', 'winds'];
var arrCopy = arr.concat();
arrCopy[0] = 'tacssw'
console.log(arr)//['wsscat', 'autumns', 'winds']
console.log(arrCopy)//['tacssw', 'autumns', 'winds']
```


### （3）对象

```
var obj = {
    name:'wsscat',
    age:0
}

var obj2 = new Object();
obj2.name = obj.name;
obj2.age = obj.age

obj.name = 'autumns';
console.log(obj);//Object {name: "autumns", age: 0}
console.log(obj2);//Object {name: "wsscat", age: 0}
```



### （4）封装好一个方法来处理对象的深拷贝

```
var obj = {
    name: 'wsscat',
    age: 0
}
var deepCopy = function(source) {
    var result = {};
    for(var key in source) {
       if(typeof source[key] === 'object') {
           result[key] = deepCopy(source[key])
       } else {
           result[key] = source[key]
       }
     }
    return result;
}
var obj3 = deepCopy(obj)
obj.name = 'autumns';
console.log(obj);//Object {name: "autumns", age: 0}
console.log(obj3);//Object {name: "wsscat", age: 0}
```
