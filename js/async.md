# 异步

## 疑问

JS是单线程的,异步不应该是多线程的吗?

异步不一定是多线程的,但一定是非堵塞的.多线程只是异步的一种实现方式.

为什么需要异步编程?

防止异步内容堵塞同步的内容.

比如,你使用ajax向服务器请求数据,极端假设服务器需要10min才能返回给你数据.假设不使用异步,那么这将是堵塞的.

JS如何实现异步的?

JS会把异步放入`消息队列(优先级相同的情况下,先进先出)`,当同步执行完成之后,会取消息队列的内容.

所以执行顺序可以理解为:同步优先、异步靠边、回调垫底

JS的异步有哪些?

setTimeout()异步函数

Promise对象类型的函数,比如async/await,fetch()等

## Promise

### 意义

支持异步编程

### 状态

Promise(期约)共有三个状态:

- pending(待定))
- fulfilled(兑现)
- reject(拒绝)

Promise初始状态为pending,当变为fulfilled或者reject时,状态将会被冻结,即无法改变.可以看作一次性用品.

### 方法

- then(callback)
- catch(callback)

*callback表示回调函数*

then()与catch()返回的仍为Promise

该返回的Promise会封装then()和catch()回调函数的返回值(如果无返值则封装undefined)

```js
let promise = new Promise(
    (resolve, reject) => {
        resolve('promise');
    }
)

let pt = promise.then((data) => {console.log(data);});

// 考虑到异步的执行顺序,这里使用setTimeout,保证then()异步先完成
setTimeout(() => console.log(pt), 0)
// output: Promise { undefined }
```

因此你可以`promiseObj.then(callback).then(callback).catch(callback).then(callback).catch(callback)...`then()与catch()方法交叉使用,这种链式调用被称作**复合(composition)**.

在then()与catch()组成的方法链中,当前方法的回调方法的参数为当前方法的Promise对象所封装的内容,所以就可以避免了臭名昭著的回调地狱.


## 方法与状态的关系

then()对应fulfilled,catch()对应reject.

当上一个promise的状态为fulfilled时,将执行下一个then().

当上一个promise的状态为reject时,将执行下一个catch().

### Promise的fulfilled与reject规则

Promise对象可以在executor中设置

```js
let promise = new Promise(
    (resolve, reject) => {
        // You can set resolve or reject
        // Once you set one of them, it will not change again
        resolve('fulfilled');
    }
)
```

then()或者catch()返回的Promise状态:

[摘录MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)

- 返回了一个值，那么 then 返回的 Promise 将会成为接受状态，并且将返回的值作为接受状态的回调函数的参数值。
- 没有返回任何值，那么 then 返回的 Promise 将会成为接受状态，并且该接受状态的回调函数的参数值为 undefined。
- 抛出一个错误，那么 then 返回的 Promise 将会成为拒绝状态，并且将抛出的错误作为拒绝状态的回调函数的参数值。
- 返回一个已经是接受状态的 Promise，那么 then 返回的 Promise 也会成为接受状态，并且将那个 Promise 的接受状态的回调函数的参数值作为该被返回的Promise的接受状态回调函数的参数值。
- 返回一个已经是拒绝状态的 Promise，那么 then 返回的 Promise 也会成为拒绝状态，并且将那个 Promise 的拒绝状态的回调函数的参数值作为该被返回的Promise的拒绝状态回调函数的参数值。
- 返回一个未定状态（pending）的 Promise，那么 then 返回 Promise 的状态也是未定的，并且它的终态与那个 Promise 的终态相同；同时，它变为终态时调用的回调函数参数与那个 Promise 变为终态时的回调函数的参数是相同的。


## async/await

async修饰的函数如果不存在await,那他将是同步的.

同样,async修饰的函数返回值会被封装为Promise对象.

举例:

```js
async function test(){
    return "I am returned";
}
console.log(test()) // Promise { 'I am returned' }
```

await一般用来修饰异步(可以修饰同步,但没什么用)

当await修饰异步之后,那么await后面的操作将作为异步放到await修饰的异步的队列之后.

await修饰的异步返回值不再是Promise对象,而是Promise对象所包含的内容.

举个例子
```js
let p = new Promise(
    (resolve,reject) => {
        resolve('fulfilled');
    }
)

async function test() {
    const a = await p;
    console.log(a);
}

test();

// fulfilled
```

## setTimeout

这个异步有点特殊,他依靠时钟,不返回promise,依旧在消息队列,但优先级低于promise.


## 例子
```js
let promise = new Promise(
    (resolve, reject) => {
        // You can set resolve or reject
        // Once you set one of them, it will not change again
        resolve('Yeah, First promise is resolved! So, I can execute then() of the promise method!');
    }
)

console.log(promise);

const promiseGoOn = promise
    .then(() => {console.log(Oops);} )
    .catch(() => {console.log("Ohhh! I catch it! Last then() occurred error! It is so bad!");})
    .then(() => {
        console.log("last promise of then() or catch() is fulfilled, so I can execute.");
        return "the asynchronous method is over";
    });
    
setTimeout( () => console.log(promiseGoOn), 0)

/*
output:
Promise {
  'Yeah, First promise is resolved! So, I can execute then() of the promise method!'
}
Ohhh! I catch it! Last then() occurred error! It is so bad!
last promise of then() or catch() is fulfilled, so I can execute.
Promise { 'the asynchronous method is over' }
*/
```

