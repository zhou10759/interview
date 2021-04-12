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
