### 1 数组去重

```js
    // 思路1：定义一个新数组，并存放原数组的第一个元素，
    // 然后将元素组一一和新数组的元素对比，若不同则存放在新数组中。
    function unique(arr) {
      var res = [arr[0]];
      for (var i = 0;i < arr.length;i++) {
        var repeat = false;
        for (var j = 0;j<res.length;j++) {
          if (arr[i] === res[j]) {
            repeat = true;
            break;           
            alert(1);                        
          }
        }
        if (!repeat) {
          res.push(arr[i]);
        }
      }
      return res;
    }
    console.log(unique([1,2,1,2,3,4,3,1,3,4]));

```

### 2 使用正则表达式验证邮箱格式