# 5.1 Volatile变量

#### 定义：

对于此变量的操作不会发生重排序，并且不会被缓存在寄存器或者对其他处理器不可见的地方。因此读取volatile类型的变量时，总会返回最新写入的值。**确保可见性**

#### 类似：

volatile变量类似于如下同步类（但是下面的同步类可见性比volatile变量更强）

```java
public class SynchronizedInteger{
    private int value;

    public synchronized int get(){
        return value;
    }

    public synchronized void set(int value){
        this.value=value;
    }
}
```

#### 使用情况：

当且仅当满足如下条件的时候，才应该使用

* 对变量的写入操作不依赖当前变量的值

> 例如一个volatile变量count，count++则不是一个原子操作。

* 该变量不会与其他状态变量一起纳入不变性条件中
* 在访问变量时不需要加锁



