> js垃圾回收有两种实现方式，分别是`标记清除`和`引用计数`

### 标记清除

当变量进入执行环境时标记为“进入环境”，当变量离开执行环境时则标记为“离开环境”，被标记为“进入环境”的变量是不能被回收的，因为它们正在被使用，而标记为“离开环境”的变量则可以被回收

```javascript
function func3 () {
      const a = 1
      const b = 2
      // 函数执行时，a b 分别被标记 进入环境
}

func3() // 函数执行结束，a b 被标记 离开环境，被回收
```
### 引用计数

统计引用类型变量声明后被引用的次数，当次数为 0 时，该变量将被回收。（早期浏览器，现基本已被淘汰）

```javascript
function func4 () {
      const c = {} // 引用类型变量 c的引用计数为 0
      let d = c // c 被 d 引用 c的引用计数为 1
      let e = c // c 被 e 引用 c的引用计数为 2
      d = {} // d 不再引用c c的引用计数减为 1
      e = null // e 不再引用 c c的引用计数减为 0 将被回收
}
```

缺点：
循环引用会永远不会被清除，必须手动进行清除



https://juejin.im/post/5ad8507cf265da50472fc93c