<!--
 * @Author: xiaowan.chen
 * @Date: 2022-02-07 13:31:05
 * @Description: Do not edit
-->

### Event Loop 事件循环

#### 堆得概念

- 堆是线性数据结构，相当于一维数组，有唯一后继。

#### 栈的概念

- 栈在计算机科学中是限定仅在表尾进行插入或删除操作的线性表
- 后进先出

#### 队列

- 先进先出

#### Event Loop

##### MacroTask（宏任务）

- script 全部代码、setTimeout

##### MicroTask（微任务）

- Promise

### 浏览器中的 Event Loop

- Javascript 有一个 main thread 主线程和 call-stack 调用栈(执行栈)，所有的任务都会被放到调用栈等待主线程执行

#### JS 调用栈

- 后进先出的规则

#### 同步任务和异步任务

- Javascript 单线程任务被分为同步任务和异步任务，同步任务会在调用栈中按照顺序等待主线程依次执行，异步任务会在异步任务有了结果后，将注册的回调函数放入任务队列中等待主线程空闲的时候（调用栈被清空），被读取到栈内等待主线程的执行。

```
console.log('script start')

async function async1() {
  await async2()
  console.log('async1 end')
}
async function async2() {
  console.log('async2 end')
}
async1()

setTimeout(function() {
  console.log('setTimeout')
}, 0)

new Promise(resolve => {
  console.log('Promise')
  resolve()
})
  .then(function() {
    console.log('promise1')
  })
  .then(function() {
    console.log('promise2')
  })

console.log('script end')


// 输出的结果是
script start
async2 end
Promise
script end
async1 end
promise1
promise2
setTimeout
```
