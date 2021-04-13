# interview

# 数组去重
### 1.es6去重

```
// set结构中不会有重复的数据
function unique (arr) {
  return Array.from(new Set(arr))
}

```

### 2.利用两个for循环，splice

```
function unique (arr) {
  for( var i = 0 ; i < arr.length ; i++ ){
    for( var j = i + 1 ;j < arr.length ; j++ ){
      if( arr[i] === arr[j] ){
        arr.splice(j , 1)
        j--
      }
    }
  }
  return arr
}

```

### 3.利用indexOf

```
function unique(arr){
  let newArr = []
  for(var i = 0;i < arr.length; i++){
    if(newArr.indexOf(arr[i]) === -1){
       newArr.push(arr[i])
    }
  }
  return newArr
}
```

### 4.利用includes（检测数组是否有某值）

```
function unique(arr){
  let newArr = []
  for(var i = 0;i < arr.length; i++){
    if(!arr.includes(arr[i])){
       newArr.push(arr[i])
    }
  }
  return newArr
}
```

### 5.利用hasOwnProperty（ 判断是否存在对象属性 ）

```
function unique(arr){
   var obj = {};
    return arr.filter(function(item, index, arr){
        return obj.hasOwnProperty(typeof item + item) ? false : (obj[typeof item + item] = true)
    })
}
```

### 6.利用filter

```
function unique(arr){
   return arr.filter(function(item, index, arr) {
    //当前元素，在原始数组中的第一个索引==当前索引值，否则返回当前元素
    return arr.indexOf(item, 0) === index;
  });
}
```

### 7.利用Map数据结构去重

```
function arrayNonRepeatfy(arr) {
  let map = new Map();
  let array = new Array();  // 数组用于返回结果
  for (let i = 0; i < arr.length; i++) {
    if(map .has(arr[i])) {  // 如果有该key值
      map .set(arr[i], true); 
    } else { 
      map .set(arr[i], false);   // 如果没有该key值
      array .push(arr[i]);
    }
  } 
  return array ;
}
```



# 深拷贝函数 

```
 function isObject(obj) {
      return Object.prototype.toString.call(obj) === '[object Object]'
  }
  
  function deepCopy(source, hash = new WeakMap()) {
      // 判断如果参数不是一个对象，返回改参数
      if (!isObject(source)) return source;
      if (hash.has(source)) return hash.get(source); // 如何拷贝过该对象，则直接返回该对象
      // 判断参数是对象还是数组来初始化返回值
      let res = Array.isArray(source) ? [] : {};
      hash.set(source, res); // 哈希表添加新对象
      // 循环参数对象的key
      for (let key in source) {
          // 如果该key属于参数对象本身
          if (Object.prototype.hasOwnProperty.call(source, key)) {
              // 如果该key的value值是对象，递归调用深拷贝方法进行拷贝
              if (isObject(source[key])) {
                  res[key] = deepCopy(source[key], hash);
              } else if (Array.isArray(source[key])) {
                  // 如果是数组
                  res[key] = []
                  for (var i = 0, len = source[key].length; i < len; i++) {
                      res[key].push(deepCopy(source[key][i]));
                  }
              } else {
                  // 如果该key的value值不是对象，则把参数对象key的value值赋给返回值的key
                  res[key] = source[key];
              }
          }
      }
      // 返回返回值
      return res;
  };

 let obj1 = {
    name: 'obj.name',
    un: undefined,
    nu: null,
    sy: Symbol(123),
    say: function () {
        console.log(this.name);
    },
    reg: /\d{6}/g,
    date: new Date(),
    child: {
        name: 'child.name'
    },
    list: [1,2,3,4]
}
let obj2 = deepCopy(obj1);
console.log(obj1);
console.log(obj2);
// console.log(obj2 === obj1)
obj2.name = 'obj2.name';
obj2.say();//复制代码
obj1.say();//复制代码
obj2.list.push(7, 8, 9)
console.log(obj1)
console.log(obj2)

```

# js的事件循环eventloop

### 进程与线程

#### 进程  资源分配的最小单位

应用程序的执行实例，每一个进程都是由私有的虚拟地址空间、代码、数据和其他系统资源所组成。

#### 线程 程序执行的最小单位

线程是进程内的一个独立执行单元，在不同的线程之间是可以共享进程资源的。


###  宏任务和微任务

###### 宏任务包括：** script（整体代码），setTimeout，setInterval，requestAnimationFrame，I/O，setTmmediate **

###### 其中setImmediate只存在于Node中，requestAnimationFrame只存在于浏览器中。



###### 微任务包括：** Promise，Object.observe（已废弃），MutationObserver（html5新特性） **

###### 其中process.nextTick只存在于Node中，MutationObserver只存在于浏览器中。

##### 执行方式

执行一个宏任务，过程中遇到微任务时，将其放在微任务的事件队列里，当前宏任务执行完成后，会查看微任务的事件队列，以此执行里面的微任务。如果还有宏任务的话，在重新开启宏任务。。。

```
console.log('a');

setTimeout(function() {
    console.log('b');
    process.nextTick(function() {
        console.log('c');
    })
    new Promise(function(resolve) {
        console.log('d');
        resolve();
    }).then(function() {
        console.log('e')
    })
})
process.nextTick(function() {
    console.log('f');
})
new Promise(function(resolve) {
    console.log('g');
    resolve();
}).then(function() {
    console.log('h')
})

setTimeout(function() {
    console.log('i');
    process.nextTick(function() {
        console.log('j');
    })
    new Promise(function(resolve) {
        console.log('k');
        resolve();
    }).then(function() {
        console.log('l')
    })
})












// a,g,f,h,b,d,c,e,i,k,j,l

```


# VUE面试

### MVVM设计模式

MVVM是 ** Model-View-ViewModel ** 缩写，也就是吧MVC中的Controller演变成ViewModel。Model层代码数据模型，View代表UI组件，ViewModel是view和model层的桥梁，数据会绑定ViewModel层自动将数据渲染到页面中，视图变化时会通知ViewModel层更新数据


