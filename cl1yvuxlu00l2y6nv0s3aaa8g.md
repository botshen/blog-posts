# Handwriting function throttling and debounced

## Function throttling

Function throttling There is a requirement that the game's skills need to be CD'd for 3 seconds and cannot be released again within three seconds.

First, write a function

We need to record the CD time, when I want to release the skill to see whether it is in the CD, if not in the CD, then set the CD to true and then release the skill

```js
function fn() {
}

var cd = false
button.onclick = function () {
    if (cd) {
        //如果正在cd就什么都不做
    } else {
        //cd完了就可以释放技能了
        fn()
        //释放完了置为冷却中
        cd = true
        //3秒之后就不在冷却中了
        var timeId = setTimeout(() => {
            cd = false
        }, 3000)
    }
}
```

## 函数防抖

就是带着一起做

假设你是外卖骑手，只要有外卖就去送，但是你发现取了单没到1分钟就来了新单，很亏

所以可以这样，每次有了外卖就在等五分钟，如果没有外卖就去送，如果有外卖就去拿一下再等五分钟

直到5分钟没有外卖就全部送掉。

```js
//创建一个送外卖的想法
var timeId = null
button.onclick = function () {
    //第一次不会执行
    if (timeId) {
        window.clearTimeout(timeId)
    }
    //用户点了按钮就5秒钟之后送
    timeId = setTimeout(() => {
        fn()
        timeId = null
    }, 5000)
}
```

## 总结

```js
 // 节流（一段时间执行一次之后，就不执行第二次）
function throttle(fn, delay) {
    let canUse = true
    return function () {
        if (canUse) {
            fn.apply(this, arguments)
            canUse = false
            setTimeout(() => canUse = true, delay)
        }
    }
}

const throttled = throttle(() => console.log('hi'))
throttled()
throttled()
```

```js
 // 防抖（一段时间会等，然后带着一起做了）
function debounce(fn, delay) {
    let timerId = null
    return function () {
        const context = this
        if (timerId) {
            window.clearTimeout(timerId)
        }
        timerId = setTimeout(() => {
            fn.apply(context, arguments)
            timerId = null
        }, delay)
    }
}

const debounced = debounce(() => console.log('hi'))
debounced()
debounced()
```