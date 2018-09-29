# lazy
lazyload&amp;tell you when element scroll into viewport

主要功能就是实现懒加载。

## usage

### 最简单的用法,一次添加所有图片 ###

后面示例的 会省略import 语句 

```js
import Lazy from './lazy.js'

const lazy=new Lazy()
lazy.add(document.querySelectorAll('img[data-src]'))
```
需要懒加载的图片都会data-src 属性。把图片 add 到lazy对象，需要显示的时候会自动显示图片

add方法可以多次调用,比如增加 data-srcset属性的图片

```js
const lazy=new Lazy()
lazy.add(document.querySelectorAll('img[data-src]'))
lazy.add(document.querySelectorAll('img[data-srcset]'))
```
### 空元素点位，lazy加载数据 ###

比如在页面底部有一个区块 叫做 猜你喜欢。
因为在页面底部，如果一开始就加载，但用户又看不到，有点浪费

为了提高性能，开始的时候猜你喜欢是一个空的div,等到元素快显现的时候再加载数据。因为加载数据再显示需要一点时间，所以在距离比较远的时候，就需要触发加载

```js
const lazy=new Lazy({
ammend:100,//设大一些，给加载数据留出时间
	cb:elem=>{
		//异步加载数据，显示
	}
})
lazy.add(document.getElementById('like'))
```
### tab切换 ###

有两个tab，默认显示tab1,当点击tab的时候显示tab2。
默认是靠scroll,resize事件来触发，因为tag2的显示是手动click触发，并没有触发scroll，resize事件，所以显示tab2的图片也应该手动触发。

```js
let lazy=new Lazy()
//添加所有图片
lazy.add(tab.getElementsByTagName('img'))
//当切换tab的时候，需要手动触发加载
tab.onclick=lazy.load
```

### body子元素内的图片懒加载 ###

指定 root可选参数即可

```js
const div=document.getElementById('d1')
let lazy=new Lazy(
  root:div
)
```