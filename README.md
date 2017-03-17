移动端页面功能扩展-----长按事件
============================

有事在做移动端页面开发的过程中遇到这种需求：“模拟指纹识别”。
实际上我们只能通过长按页面中的元素来模拟这个功能。
在jQuery和Zepto中都没有包含长按事件，所以需要我们来来扩展一下。

```javascript

	$.fn.longTap = function(fn) {
		var timeout = undefined;
		var $this = this;
		for(var i = 0;i < $this.length; i += 1){
			$this[i].addEventListener('touchstart', function(event) {
				timeout = setTimeout(fn, 800); //长按时间超过800ms，则执行传入方法
			}， false);
			$this[i].addEventListener('touchend', function(event) {
				clearTimeout(timeout); //长按事件少于800ms，不会执行传入的方法
			}, fasle);
		}
	};


```

首先要添加这段代码，然后调用：

```javascript

	$('.object').longTap(function(){
		// do something...
	});

```
