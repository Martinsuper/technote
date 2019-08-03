# Guava

- [ ] 熟悉Guava，知道，了解Guava每个方法是用来干什么的，可以用来干什么
- [ ] 熟练使用Guava
- [ ] 明白Guava实现原理
- [ ] 能够自己实现Guava方法

[Guava中文教程](https://github.com/guobinhit/guava-guide)



## 基础工具 `Basic utilities`

### 使用和避免 `null` `Optional`

`Optional` 使用和避免空指针问题

> 并不明白到底用来干什么的



### 前置条件 `Preconditions` 

`Preconditions` 前置条件检查

![preconditions](http://image.martind.cn:8080/BackEnd/java/Guava/Preconditions.png)



### 通用 `object` 方法

简化 `Object` 方法的实现

![通用Object方法](http://image.martind.cn:8080/BackEnd/java/Guava/Object.png)





### `Ordering` 排序

用于排序



### `Throwable` 异常抛出



简化异常和错误的检查及传播机制





## 集合 `Collections`

### 不可变集合 `Immutable Collections`

不可变集合优点：

- 当被不可信库调用时，不可变形式是安全的；
- 不可变对象被多个线程调用时，不存在竞态问题
- 不可变集合不需要考虑变化，因此可以节省时间和空间。所有比可变的集合都比它们的可变形式有更好的内存利用率。
- 不可变对象因为固定不变，可以作为常量来安全使用。

#### `Multiset`

- 元素可以重复出现
- 不保证顺序

#### `Multimap`

- 实现一对多问题，一个`key`值可以对应多个`value`值

#### `BiMap`

- 保证 `key` 和 `value` 都是唯一的情况下，可以实现根据`value`找到`key`，实现键值对的双向映射，不用单独维护两个`map`

#### `Table`

- 类似一张二维表格，存储行、列、值

#### `RangeSet`

- 描述了一组不相连的、非空的区间。当把一个区间添加到可变的`RangeSet`时，所有相连的区间会被合并，空区间会被忽略。

#### `RangeMap`

- 描述了”不相交的、非空的区间”到特定值的映射。和`RangeSet`不同，`RangeMap`不会合并相邻的映射，即便相邻的区间映射到相同的值

### 集合工具类





### 扩展工具类





## 图 `Graphs`









## 缓存 `Caches`



## 函数风格 `Functional idioms`







## 并发 `Concurrency`







## 字符串 `String`











## 原生类型 `Primitives`







## 区间 `Ranges`





## 输入输出流 `I/O`





## 散列 `Hashing`







## 事件总线 `EventBus`



## 数学运算 `Math`





## 反射 `Reflection`


















