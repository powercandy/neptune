

## 收藏JS方法

### URL参数获取（getQuery）

```js

function getQuery(key) {
  if (location.href.indexOf('?') == -1) {
    return '';
  }
  var search = location.href.split('?')[1];
  var arr = search.split('&');
  var res = '';
  for (var i = 0; i < arr.length; i++) {
    var valArr = arr[i].split('=');
    if (valArr[0] == key) {
      res = valArr[1];
      break;
    }
  }
  return decodeURIComponent(res);
}

```

### 参数拼接（queryConcatString）

```js
function queryConcatString(obj) {
  var str = '';
  if (JSON.stringify(obj) == '{}') return str;
  for (var key in obj) {
    str += (key + '=' + obj[key] + '&')
  }
  str = str.slice(0, str.length - 1)
  return str;
}

```

### 深度克隆（deepClone）

> 下文方法只针对多层对象结构，递归处理

```js
function deepClone(obj) {
  var newObj = {};
  for (var key in obj) {
    if (Object.prototype.toString.call(obj[key]) === '[object Object]') {
      newObj[key] = deepClone(obj[key])
    } else {
      newObj[key] = obj[key]
    }
  }
  return newObj;
}

```

### 防抖函数（debounce）

> 触发高频事件后n秒内函数只会执行一次，如果n秒内高频事件再次被触发，则重新计算时间

```重点在清零clearTimeout(timer)```

使用场景：

- 登录、发短信等按钮避免用户点击太快，以致于发送了多次请求，需要防抖
- 调整浏览器窗口大小时，resize 次数过于频繁，造成计算过多，此时需要一次到位，就用到了防抖
- 文本编辑器实时保存，当无任何更改操作一秒后进行保存

```js

function debounce(fn, wait) {
    var timer;
    return function() {
        var _this = this;
        if (timer) {
            clearTimeout(timer)
        }
        timer = setTimeout(function() {
            fn.apply(_this, arguments)
        }, wait)
    }
}

window.onscroll = debounce(function() {
    console.log('scroll event);
}, 500)


```

### 节流函数（throttle）

> 高频事件触发，但在n秒内只会执行一次，所以节流会稀释函数的执行频率

```重点在开锁和关锁```

```js

function throttle(fn, wait) {
    var timer;
    return function() {
        var _this = this;
        if (timer) return;
        setTimeout(function() {
            fn.apply(_this, arguments)
            timer = null;
        }, wait)
    }
}

```

### 函数只执行一次（once）

<details open>
<summary>实现方法</summary>

```js
function once (fn) {
    let called = false
    return function () {
        if (!called) {
            called = true
            fn.apply(this, arguments)
        }
    }
}

function test() {
    console.log(1);
}
function test2() {
    console.log(2);
}

var a = once(test);
var c = once(test2);

a(); // 1
a(); // 无输出
c(); // 2
c(); // 无输出  

```
</details>

### 删除数组中某一项（removeArrayItem）

<details open>
<summary>实现方法</summary>

```js
function removeArrayItem(array, item) {
    if (array.length > 0) {
        var index = array.indexOf(item);
        if (index > -1) {
            return array.splice(index, 1)
        }
    }
}
```
</details>

### 重复某个字符串N次（repeatStr）

> 时间复杂度O(logN)

<details open>
<summary>实现方法</summary>

```js
function repeat (str, n) {
  let result = ''
  if (n > 0) {
    while (true) { // eslint-disable-line
      if (n & 1) result += str
      n >>>= 1
      if (n <= 0) break
      str += str
    }
  }
  return result
}

```
</details>


