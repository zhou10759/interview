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

``

### 3.利用indexOf

```
function unique(arr){
  let newArr = []
  for(var i = 0;i < arr.length; i++){
    if(arr.indexOf(arr[i]) === -1){
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




