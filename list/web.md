Notes / Web
===

## atob不能解码Unicode的base64

```JavaScript
atob( btoa('报错') )
// => Uncaught DOMException: Failed to execute 'btoa' on 'Window': 
# //    The string to be encoded contains characters outside of the Latin1 range.
```

##### 起因：取[jwt](https://jwt.io/)的payload

##### 解决：

1. payload在JSON中随token返回
2. 第三方base64库，`base64 -> bytes -> string`。参见[base64-js](https://github.com/beatgammit/base64-js)、[stackoverflow](http://stackoverflow.com/questions/17191945/conversion-between-utf-8-arraybuffer-and-string)


## flex

注意内部元素搭`flex-shrink`，否则小屏幕下会内部元素被压缩（显示不全）

