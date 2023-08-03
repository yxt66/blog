---
title: 异步编程Promise、async、await
date: 2022-11-26
tag:
- 异步
categories:
- Js

---

{% note success:: 异步编程Promise、async、await%}

 

<!-- more -->

### 1.Promise三种状态

- `pending`
- `fulfilled`
- `rejected`

### 2.如何改变promise<pending>的状态

- 可以调用`resolve()`、`reject()`方法和抛出异常。状态一旦生成，不会改变。

### 3.特点

（1）不执行resolve或者reject 就一直是pending状态，pending不会触发then和catch

（2）`Promise.resolve（）`返回的状态取决于括号中的状态；`Promise.reject（）`返回的是rejected状态的Promise

### 4.一个 promise 指定多个成功/失败回调函数, 都会调用吗?

- 当promise改变为对应状态时会调用。

### 5.改变 promise 状态和指定回调函数谁先谁后?

1. 都有可能，正常情况是先执行回调再改变状态，但也可以先改状态再指定回调。

2. 如果先改状态再指定回调

  - 延长时间调用then（）

  - 在执行器中之间调用resolve()/reject()

### 6.什么时候才能得到数据

1. 如果先指定的回调, 那当状态发生改变时, 回调函数就会调用, 得到数据。

2. 如果先改变的状态, 那当指定回调时, 回调函数就会调用, 得到数据

### 8.promise.then()返回的新 promise 的结果状态由什么决定?

(1) 简单表达: 由 then()指定的回调函数执行的结果`v => {}`或`e=>{}`决定 ,默认为pending状态。

注意：`Promise.resolve()`和`async`默认状态为`fulfilled`

(2) 详细表达: 

​	① 如果抛出异常, 新 promise 变为 rejected, reason 为抛出的异常 

​	② 如果返回的是非 promise 的任意值, 新 promise 变为 resolved, value 为返回的值 

​	③ 如果返回的是另一个新 promise, 此 promise 的结果就会成为新 promise 的结果

### 9.promise 异常传透? 

(1) 当使用 promise 的 then 链式调用时, 可以在最后指定失败的回调。

(2) 前面任何操作出了异常, 都会传到最后失败的回调中处理

### 10.中断 promise 链? 

办法: 在回调函数中返回一个 pendding 状态的 promise 对象

```js
//1. 打印结果：1  p(fulfilled)
	let p = Promise.reject().catch(e => {
    })
    p.then(()=>{
        console.log(1)
    })
    p.catch(()=> {
        console.log(2)
    })
    setTimeout(()=>{
        console.log(p);
    })

//2.打印结果： 1 2 3 
    Promise.resolve().then(()=>{
            console.log(1)
            throw new Error('err')
        }).catch(()=>{
            console.log(2)
        }).then(()=>{
            console.log(3)
        })
```

### 11.Promise源码实现（Es5)



```js
function Promise(exector) {
    //1.基础模板

    //2.当同步调用resolve,reject,throw影响Promise状态控制执行then返回结果的状态。
    //eg: 同步执行let p = new Promise((resolve,reject) => { resolve('ok')});
    //      const res = p.then() 控制res的状态

    //3.当异步影响Promise的改变，回调执行then中的函数
    //eg: let p = new Promise((resolve,reject) => { setTimeout(...resolve('ok'))});

    //4.v=>{}(onResolve) or e => {}(onReject)未定义 抛绣球实现异常穿透和值传递

    //5.异步执行 
    this.PromiseStatus = 'pending'
    this.PromiseValue = undefined
    this.callbacks = []
    const _this = this

    function resolve(data) {
        if (_this.PromiseStatus !== 'pending') return
        _this.PromiseStatus = 'fulfilled'
        _this.PromiseValue = data

        //当状态改变调用then中的函数
        setTimeout(() => {
            _this.callbacks.forEach(item => {
                item.onResolve()
            })
        })

    }

    function reject(data) {
        if (_this.PromiseStatus !== 'pending') return
        _this.PromiseStatus = 'rejected'
        _this.PromiseValue = data
        //5.
        setTimeout(() => {
            _this.callbacks.forEach(item => {
                item.onReject()
            })
        })
    }
    try {
        exector(resolve, reject)
    } catch (e) {
        reject(e)
    }

}
//then方法
Promise.prototype.then = function (onResolve, onReject) {
    const _this = this
    return new Promise((resolve, reject) => {
        //4.抛绣球
        //值传递
        if (typeof onResolve !== 'function') {
            onResolve = value => value
        }
        //异常穿透
        if (typeof onReject !== 'function') {
            onReject = e => { throw e }
        }
        //2.
        //封装函数，避免冗余
        function callback(type) {
            try {
                let result = type(_this.PromiseValue)
                if (result instanceof Promise) {
                    result.then(v => {
                        resolve(v)
                    }, e => {
                        reject(e)
                    })
                } else {
                    resolve(result)
                }
            } catch (e) {
                reject(e)
            }
        }
        if (this.PromiseStatus === 'fulfilled') {

            //5.
            setTimeout(() => {
                callback(onResolve)
            })
        }
        if (this.PromiseStatus === 'rejected') {
            setTimeout(() => {
                callback(onReject)
            })
        }
        //3.
        if (this.PromiseStatus === 'pending') {
            //保存then中的函数
            this.callbacks.push({
                //细节地方：then式调用
                onResolve() {
                    callback(onResolve)
                },
                // onResolve ,onReject 这种写法不会改变res的状态一直是pending就无法链式调用
                onReject() {
                    callback(onReject)
                }
            })
        }
    })

}

//catch方法
Promise.prototype.catch = function (onReject) {
    return this.then(undefined, onReject)
}

//Promise.resolve()
Promise.resolve = function (value) {
    return new Promise((resolve, reject) => {
        if (value instanceof Promise) {
            value.then(v => {
                resolve(v)
            }, e => {
                reject(e)
            })
        } else {
            resolve(value)
        }
    })
}

//Promise.reject()返回状态永远是rejected状态
Promise.reject = function (err) {
    return new Promise((resolve, reject) => {
        reject(err)
    })
}
//Promise.all() 参数可以全是promise对象

Promise.all = function (promises) {
    //1.计数器 空数组
    //2.遍历每个Promise.then,不能用push
    let count = 0
    let length = promises.length
    let resultArr = new Array(length)
    return new Promise((resolve, reject) => {
        for (let i = 0; i < length; i++) {
            promises[i].then(v => {
                count++
                resultArr[i] = v
                if (count === length) resolve(resultArr)
            }, e => {
                reject(e)
            })
        }
    })
}

//Promise.race() 参数可以全是promise对象

Promise.race = function (promises) {
    return new Promise((resolve, reject) => {
        for (let i = 0; i < promises.length; i++) {
            // if(!promises[i] instanceof Promise) {
            //     转为Promise对象
            // }
            promises[i].then(v => {
                resolve(v)
            }, e => {
                reject(e)
            })

        }
    })
}
```

### 12.Promise源码实现（Es6)

```js
// const PromiseStatus = 'pending'
class Promise {
    constructor(exector) {
        this.PromiseStatus = 'pending'
        this.PromiseValue = undefined
        this.callbacks = []

        //resolve
        const resolve = data => {
            if (this.PromiseStatus !== 'pending') return
            this.PromiseStatus = 'fulfilled'
            this.PromiseValue = data

            //当状态改变调用then中的函数
            setTimeout(() => {
                this.callbacks.forEach(item => {
                    item.onResolve()
                })
            })
        }

        //reject
        const reject = data => {
            if (this.PromiseStatus !== 'pending') return
            this.PromiseStatus = 'rejected'
            this.PromiseValue = data

            setTimeout(() => {
                this.callbacks.forEach(item => {
                    item.onReject()
                })
            })
        }

        try {
            exector(resolve, reject)
        } catch (e) {
            reject(e)
        }
    }
    then(onResolve, onReject) {
        return new Promise((resolve, reject) => {

            //值传递
            if (typeof onResolve !== 'function') {
                onResolve = value => value
            }
            //异常穿透
            if (typeof onReject !== 'function') {
                onReject = e => { throw e }
            }

            //封装函数，避免冗余
            const callback = type => {
                try {
                    let result = type(this.PromiseValue)
                    if (result instanceof Promise) {
                        result.then(v => {
                            resolve(v)
                        }, e => {
                            reject(e)
                        })
                    } else {
                        resolve(result)
                    }
                } catch (e) {
                    reject(e)
                }
            }

            if (this.PromiseStatus === 'fulfilled') {

                setTimeout(() => {
                    callback(onResolve)
                })
            }

            if (this.PromiseStatus === 'rejected') {
                setTimeout(() => {
                    callback(onReject)
                })
            }

            if (this.PromiseStatus === 'pending') {
                this.callbacks.push({
                    onResolve() {
                        callback(onResolve)
                    },
                    onReject() {
                        callback(onReject)
                    }
                })
            }
        })
    }
    catch(onReject) {
        return this.then(undefined, onReject)
    }
    //静态成员
    static resolve(value) {
        return new Promise((resolve, reject) => {
            if (value instanceof Promise) {
                value.then(v => {
                    resolve(v)
                }, e => {
                    reject(e)
                })
            } else {
                resolve(value)
            }
        })
    }
    static reject(err) {
        return new Promise((resolve, reject) => {
            reject(err)
        })
    }
    static all(promises) {
        let count = 0
        let length = promises.length
        let resultArr = new Array(length)
        return new Promise((resolve, reject) => {
            for (let i = 0; i < length; i++) {
                promises[i].then(v => {
                    count++
                    resultArr[i] = v
                    if (count === length) resolve(resultArr)
                }, e => {
                    reject(e)
                })
            }
        })
    }
    static race(promises) {
        return new Promise((resolve, reject) => {
            for (let i = 0; i < promises.length; i++) {
                // if(!promises[i] instanceof Promise) {
                //     转为Promise对象
                // }
                promises[i].then(v => {
                    resolve(v)
                }, e => {
                    reject(e)
                })

            }
        })
    }
}
```

### 13.async、await

1. async 函数

   - 只能修饰异步函数，函数的返回值为 promise 对象
   -  promise 对象的结果由 async 函数执行的返回值决定（同`promise.resolve()`）

2. await

   -  await 右侧的表达式一般为 promise 对象, 但也可以是其它的值
   - 如果表达式是 promise 对象, await 返回的是 promise 成功的值
   - 如果表达式是其它值, 直接将此值作为 await 的返回值

   - await 必须写在 async 函数中, 但 async 函数中可以没有 await
   - 如果 await 的 promise 失败了, 就会抛出异常, 需要通过 try...catch 捕获处理，`后面的代码将不会执行`

### 14.综合习题

<img src="https://raw.githubusercontent.com/yxt66/img/main/img/image-20221126203829514.png" alt="image-20221126203829514" style="zoom:70%;" />

<img src="https://raw.githubusercontent.com/yxt66/img/main/img/image-20221126203901625.png" alt="image-20221126203901625" style="zoom:70%;" />

<img src="https://raw.githubusercontent.com/yxt66/img/main/img/image-20221126204212217.png" alt="image-20221126204212217" style="zoom: 70%;" />