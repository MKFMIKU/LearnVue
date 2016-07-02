这里是数据绑定实验。也是 Vue 的第一步尝试。

[实验地址](../init／lab.html)

一步步调试观察中。

```js
var self=document.getElementById('test')
```

![](http://7xs9gn.com1.z0.glb.clouddn.com/16-7-2/75981400.jpg)

这里获取对象

```js
var bindingMark = 'data-element-binding'
function markToken (match, variable) {
    console.log(match);
    console.log(variable);
    return '<span ' + bindingMark + '="' + variable +'"></span>';
}
content  = self.innerHTML.replace(/\{\{(.*)\}\}/g, markToken)
```

查找对象标记
替换

```js
self.innerHTML = content
```

![](http://7xs9gn.com1.z0.glb.clouddn.com/16-7-2/59207622.jpg)

![](http://7xs9gn.com1.z0.glb.clouddn.com/16-7-3/40431798.jpg)

这里运用了正则去替换

然后是查找这个被标记的dom节点

```js
el = self.querySelectorAll('[' + bindingMark + '="' + 'msg' + '"]')
```
![](http://7xs9gn.com1.z0.glb.clouddn.com/16-7-3/2913747.jpg)

移除标记。

![](http://7xs9gn.com1.z0.glb.clouddn.com/16-7-3/85684137.jpg)

成功替换

![](http://7xs9gn.com1.z0.glb.clouddn.com/16-7-3/11459730.jpg)

***

然后注意大神在 Vue 里的写法

```js
Object.defineProperty(data, variable, {
    set: function (newVal) {
	    [].forEach.call(bindings[variable].els, function (e) {
		    bindings[variable].value = e.textContent = newVal
		})
	},
	get: function () {
	    return bindings[variable].value
	}
});
```