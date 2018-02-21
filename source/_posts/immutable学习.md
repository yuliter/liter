---
title: immutable学习
date: 2018-02-21 11:38:54
tags:
---
## immutable宏观理解
Immutable：不可改变
***
Immutable data 就是一旦创建，就不能再被更改的数据。对Immutable对象的任何修改或添加删除操作都会返回一个新的Immutable对象。Immutable实现的原理是Persistent Data Structure（持久化数据结构），也就是使用旧数据创建新数据时，要保证旧数据同时可用且不变。同时为了避免deepCopy把所有节点都复制一遍带来的性能损耗，Immutable使用Structural Sharing（结构共享），即如果对象树中的一个节点发生变化，只修改这个节点和受它影响的父节点，而其他节点则进行共享。
***
当我们发生一个set操作的时候，immutable.js会只clone它的父级别以上的部分，其他保持不变，这样大家可以共享同样的部分，可以大大提高性能。
***
Immutable.js是一个完全独立的库，无论基于什么框架都可以用它.它的意义在于它弥补了js没有不可变数据结构的问题。
## immutable继续学习
Immutable.js提供了七种不可变的数据类型：List、Map、Stack、OrderMap、Set、OrderedSet、Record。对Immutable对象的操作均会返回新的对象。
***
当我们对一个Immutable对象进行操作的时候，ImmutableJS基于哈希映射树和vector map tries ，只clone该节点以及它的祖先节点，其他保持不变，这样可以共享相同的部分，大大提高性能。
#### fromJS方法
（从js数据生成不可变对象）（接收两个参数，json数据和reviver函数，在不传递reviver函数的情况下，默认将原生js的Array转为List，Object转为Map，其他原生类型原封不动返回。）
***
例子1：
var obj = {count: 1};
var map = Immutable.fromJS(obj);
var map2 = map.set('count', 2);
console.log(map.get('count')); //
console.log(map2.get('count')); // 2
***
例子2：
var obj = {
  count: 1,
  list: [1, 2, 3, 4, 5]
}
var map1 = Immutable.fromJS(obj);
var map2 = map1.set('count', 2);
console.log(map1.list === map2.list); // true
#### toJS方法
从不可变数据生成js对象  调用方式：immutableDate.toJS()
#### is方法 
判断数据结构是否相等
***
两个immutable对象可以使用‘===’来比较，这样是直接来比较内存地址，性能最好但是两个对象的值是一样的，也会返回‘false’。为了直接比较对象的值immutable.js提供了Immutable.js来做值比较。
Immutable.is(immutableA,immutableB)
Immutable.is比较的是两个对象的hashcode或valueof（对于js对象）。由于immutable内部使用了Trie数据结构来存储，只要两个对象的hashcode相等，值就是一样的，这样的算法避免了深度遍历比较，性能非常好。使用Immutable.is来减少react重复渲染，提高性能。