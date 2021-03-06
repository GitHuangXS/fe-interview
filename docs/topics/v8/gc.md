## 垃圾回收器

### 概念

### 组成

### 垃圾回收的方式

#### 手动

```js
const gc = {};
gc.a = null;
gc.b = null;
// or 
gc = null;
```
#### 自动(V8内置算法)

##### 触发时机

周期性，具体的执行时机在不同的V8版本中是不太一样的。

> IE版本的浏览器内置的垃圾回收触发时机不是周期性的，而是满足一定条件才执行，
比如内存对象个数达到多少或者内存总数达到多少百分比。

### 回收算法

#### 标记清除

- 从root开始(浏览器中是window)遍历所有可访问的对象。
- 回收不可访问的对象。

> 在之前的V8版本中GC和JS主线程是阻塞执行的，这样实现和管理起来
比较简单。但是在某些极端情况会有性能问题，之后V8对这一块
有了很大的改动，现在这样的问题已经非常不明显了。

#### 引用计数(基本废弃)

其最大的缺点就是不能处理循环引用问题

```js
function fn() {
  var a = {};
  var b = {};
  a.pointer = b;
  b.pointer = a;
}
fn();
```
