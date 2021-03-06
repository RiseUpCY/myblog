# 模拟bind实现

> 在基础知识的学习中要注重深入，模拟一些常用函数的学习便是很好的办法,一下皆是本人学习记录，无关对错

## 模拟bind

```text
Function.prototype.newBind = function (target, ...args){
    target = target || window
    let self = this
    let temp = function (){}

    let F = function (...args2) {
        return self.apply(this instanceof temp ? this : target, args.concat(args2))
    }
    // 由于返回的F函数与show不同原型
    temp.prototype = this.prototype
    F.prototype = new temp()
    return F
}
```

## 模拟数组的方法

> push
>
> ```text
> Array.prototype.push = function (){
>     for(let val of arguments){
>         this[this.length] = val
>     }
>     this.length++
>     return this.length
> }
> ```
>
> pop
>
> ```text
>  Array.prototype.pop = function () {
>     let last = this[this.length - 1]
>     this.length--
>     return last
> }
> ```
>
> shift

```text
Array.prototype.shift = function () {
    for(let [index, val] of this.entries()){
        this[index] = this[index + 1]
    }
    this.length --
}
```

> unshift
>
> ```text
> Array.prototype.unshift = function () {
>     let newArr = []
>     newArr.length = arguments.length + this.length
>     for(let [index, val] of newArr.entries()){
>         index < arguments.length ?
>         newArr[index] = arguments[index] : 
>         newArr[index] = this[index - arguments.length]
>     }
>     return newArr
> }
> ```
>
> 去重
>
> ```text
> Array.prototype.unique = function () {
>     // 方法一 return [...new Set(this)]
>     let temp = {}, arr = []
>     for(let val of this){
>         if(!temp[val]){
>             temp[val] = 'yes'
>             arr.push(val)
>         }
>     }
>     return arr
> }
> ```

