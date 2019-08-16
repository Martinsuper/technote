# java容器

## collection 接口
> collection是一个根接口

<mermaid>
graph TD
a(Collection) --extends--> b1(List)
a --extends--> b2(Set)
a --extends--> b3(Queue)
a --extends--> b4[AbstractCollection]
b1 --implements--> c1(AbsrtactList)
b4 --extends--> c1
c1 --extends--> d1(ArrayList)
b1 --implements--> d1
c1 --extends--> d2(AbstractSequentialList)
d2 --extends--> e1(LinkedList)
b1 --implements--> e1
c1 --extends--> e2(Vector)
b1 --implements--> e2
e2 --extends--> e3(Stack)
b2 --extends--> c3(SortedSet)
b2 --implements--> c2(AbstractSet)
b4 --extends--> c2
c2 --extends--> d3(HashSet)
b2 --implements--> d3
c2 --extends--> d4(TreeSet)
c3 --> d4
d3 --extends--> e4(LinkedHashSet)
b2 --implements--> e4
</mermaid>
::: tip 抽象方法
* `abstract` 抽象方法，不能直接调用抽象方法，不能实例化。
* 不能被`private`修饰，因为抽象方法必须被子类实现，而private对于子类来说没有办法访问，所以会产生矛盾
* 不能被`static`修饰，如果用static修饰了，那么我们可以直接通过类名调用，而抽象方法压根就没有主体，没有任何业务逻辑，这样就毫无意义了。
* 抽象类不能使用final关键字修饰，因为final修饰的类是无法被继承，而对于抽象类来说就是需要通过继承去实现抽象方法，这又会产生矛盾。
* 抽象类与接口（interface）有很大的不同之处，接口中不能有实例方法去实现业务逻辑，而抽象类中可以有实例方法，并实现业务逻辑，比如我们可以在抽象类中创建和销毁一个线程池。
* 如果一个类继承了一个抽象类，那么它必须全部覆写抽象类中的抽象方法。
:::

### collection接口定义方法
`add()`:确保容器保持具有泛型类型T的参数，如果没有将此参数添加进容器，则返回false
`addAll(Collection<?> c)`：添加参数中所有元素
`clear()`：移除容器中所有元素

`contains(Object o)`：如果元素中包含o，则返回true

`containsAll(Collection<?> c)`：如果此Collection中包含c中所有元素，返回true

`equals(Object o)`：比较此Collection与指定对象是否相等

`hashCode()`：返回此collection的哈希码值

`isEmpty()`：如果此collection不包含元素，返回true

`iterator()`：返回此collection的元素上进行迭代的迭代器

`remove(Object o)`：从此collection中移除此元素的一个实例

`removeAll(Collection<?> c)`：移除参数中的元素

`retainAll(Collection<?> c)`：只保留参数中的元素，求交集

`size()`：返回容器中元素的数目

`toArray()`：返回包含此collection中的所有元素的数组

`toArray(T[] a)`：返回包含此collection中的所有元素的数组；返回数组的运行时类型与参数数组a的类型相同，不是单纯的Object

实例：

```java
public class LearnArray {
    public static void main(String[] args) {
        Collection<String> list = new ArrayList<>();
        list.add("hello");
        list.add("world");
        System.out.println("add()操作：");
        print(list);
        Collection<String> param = new ArrayList<>();
        param.add("a");
        param.add("b");
        System.out.println("addAll()操作：");
        list.addAll(param);
        print(list);
        System.out.println("移除前：");
        print(param);
        param.clear();
        System.out.println("移除后：");
        print(param);
        System.out.println(list.contains("a"));
    }
    private static void print(Collection<String> list){
        for (String str: list) {
            System.out.print(str+" ");
        }
        System.out.println();
    }
}
```

集合转数组：

```java
Collection<String> list = new ArrayList<>();
list.add("hello");
list.add("world");
Object[] array = list.toArray();
String[] str = list.toArray(new String[0]);
```

### List接口

> 继承Collection接口，包含Collection操作外，还提供如下操作：



`get(int index)`：获取指定位置元素

`indexOf(Object c)`：返回此列表中第一次出现的指定元素的索引；如果此列表不包含该元素，则返回-1

`lastIndexOf(Object o)`：返回此列表中最后出现的指定元素的索引；如果列表不包含此元素，则返回 -1

`listIterator()`：返回此列表元素的列表迭代器（按适当顺序）

`listIterator(int index)`：返回列表中元素的列表迭代器（按适当顺序），从列表的指定位置开始

`remove(int index)`：移除指定元素

`remove(Object o)`：移除第一次出现的指定元素

`removeAll(Collection<?> c)`：移除所有包含在c中的元素

`retainAll(Collection<?> c)`：仅保留c中包含的元素

`set(int index, E element)`：用指定元素替换列表中指定位置的元素

`subList(int fromIndex, int toIndex)`：返回列表中指定的 `fromIndex`（包括 ）和 `toIndex`（不包括）之间的部分视图





### Set接口

> set是不包含重复元素的collection，提供操作和collection完全相同，set是无序的



```mermaid
graph TD

a(set) --> b1(HashSet)
a --> b2(TreeSet)
a --> b3(LinkedHashSet)

```

#### HashSet

> 为快速查找设计的Set，存入HashCode的元素必须定义hashCode()

`add(E e)`：如果set中不包含指定元素，则添加指定元素

`clear()`：从set中移除所有元素

`clone()`：返回此HashSet实例的浅表副本：并没有复制这些元素本身

`contains(Object o)`：如果set包含指定元素，返回true

`isEmpty()`：如果此set不包含任何元素，则返回true

#### TreeSet

> 保持次序的Set，底层为树结构。使用它可以从Set中提取有序的序列。元素必须实现Comparable接口



`ceiling(E e)`：返回此set中大于等于给定元素的最小元素；如果不存在这样的对象，则返回null

`clone()`：返回`TreeSet`实例的浅表副本

`descendingIterator()`：返回此set元素上按降序进行迭代的迭代器

`descendingSet()`：返回此set中包含元素的逆序视图

`first()`：返回此set中当前第一个（最低）元素

`floor(E e)`：返回此set中小于等于给定元素的最大元素；如果不存在这样的元素，则返回null；

`headSet(E toElement)`：返回此set的部分视图，其元素严格小于toElement


`headSet(E toElement, boolean inclusive)`：返回此 set 的部分视图，其元素小于（或等于，如果 inclusive 为 true）toElement。

`higher(E e)`：返回此 set 中严格大于给定元素的最小元素；如果不存在这样的元素，则返回 null。

`last() `：返回此 set 中当前最后一个（最高）元素。

`lower(E e)` ：返回此 set 中严格小于给定元素的最大元素；如果不存在这样的元素，则返回 null。
`pollFirst()` ：获取并移除第一个（最低）元素；如果此 set 为空，则返回 null。
`pollLast()` ：获取并移除最后一个（最高）元素；如果此 set 为空，则返回 null。
`subSet(E fromElement, boolean fromInclusive, E toElement, boolean toInclusive)` ：返回此 set 的部分视图，其元素范围从 fromElement 到 toElement。
`subSet(E fromElement, E toElement)` ：返回此 set 的部分视图，其元素从 fromElement（包括）到 toElement（不包括）

`tailSet(E fromElement)` ：返回此 set 的部分视图，其元素大于等于 fromElement。
`tailSet(E fromElement, boolean inclusive)` ：返回此 set 的部分视图，其元素大于（或等于，如果 inclusive 为 true）fromElement。

#### LinkedHashSet

> 具有`HashSet`的查询速度，且内部使用链表维护元素的顺序。于是在使用迭代器遍历Set时，结果会按元素插入的次序显示。元素也必须定义`hashCode()`方法

### Queue接口

> 除了包含基本的Collection操作外，还提供一下操作：

`add(E e)`：将指定元素插入队列

`element()`：获取，但不移除此队列的头

`offer(E e)`：将指定元素插入队列，当使用有容量限制的队列时，此方法要优于`add()`，后者可能无法插入元素，而只是抛出一个异常

`peek()`，获取但不移除此队列的头；如果此队列为空，则返回null

`poll()`，获取并移除此队列的头；如果此队列为空，则返回null

### AbstractCollection接口

> 提供Collection接口的骨干实现，最大限度地减少实现此接口的工作量


