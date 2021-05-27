fucking-java-concurrency
==========================

:point_right: Demonstrate the concurrency problem in `Java` through Demo.

:apple: Reasons to organize Demo
----------------------------------

-Observable actual phenomena :see_no_evil: more intuitive and credible than the principle of concurrency :speak_no_evil:.
-The `Java` language standard library supports threads, and the language itself (such as `GC`) and applications (server side `The Server side`) will heavily use multithreading.
-Concurrency degree design In the analysis and implementation, the complexity is greatly increased.
    If you do not systematically understand and fully analyze the concurrency logic and write code at will, it is not an exaggeration to describe such a program as ** "happens" ** that it can run with correct results.

The Demos here do not give explanations and discussions, and they are all entry-level :neckbeard:, for more information, please refer to [Some Concurrent Issues Discussions and Materials](#Some Concurrent Issues Discussions and Materials).

You are welcome to provide ([Submit Issue](https://github.com/oldratlee/fucking-java-concurrency/issues)) and share ([Submit code after Fork](https ://github.com/oldratlee/fucking-java-concurrency/fork))! :kissing_heart:

-------------------------------------------------- ------------------------------

<img src="dining-philosophers-problem.jpg" width="30%" align="right" />

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


-[:beer: Modifications without synchronization will not be read in another thread](#beer-%E6%97%A0%E5%90%8C%E6%AD%A5%E7%9A%84%E4% BF%AE%E6%94%B9%E5%9C%A8%E5%8F%A6%E4%B8%80%E4%B8%AA%E7%BA%BF%E7%A8%8B%E4%B8% AD%E4%BC%9A%E8%AF%BB%E4%B8%8D%E5%88%B0)
  -[Demo Description](#demo%E8%AF%B4%E6%98%8E)
  -[Question Description] (#%E9%97%AE%E9%A2%98%E8%AF%B4%E6%98%8E)
  -[Quick Run](#%E5%BF%AB%E9%80%9F%E8%BF%90%E8%A1%8C)
-[:beer: Infinite loop of `HashMap`](#beer-hashmap%E7%9A%84%E6%AD%BB%E5%BE%AA%E7%8E%AF)
  -[Demo description](#demo%E8%AF%B4%E6%98%8E-1)
  -[Question Description] (#%E9%97%AE%E9%A2%98%E8%AF%B4%E6%98%8E-1)
  -[Quick Run](#%E5%BF%AB%E9%80%9F%E8%BF%90%E8%A1%8C-1)
-[:beer: Combination status read invalid combination](#beer-%E7%BB%84%E5%90%88%E7%8A%B6%E6%80%81%E8%AF%BB%E5%88 %B0%E6%97%A0%E6%95%88%E7%BB%84%E5%90%88)
  -[Demo description](#demo%E8%AF%B4%E6%98%8E-2)
  -[Question Description] (#%E9%97%AE%E9%A2%98%E8%AF%B4%E6%98%8E-2)
  -[Quick Run](#%E5%BF%AB%E9%80%9F%E8%BF%90%E8%A1%8C-2)
-[:beer: `long` variable read invalid value](#beer-long%E5%8F%98%E9%87%8F%E8%AF%BB%E5%88%B0%E6%97%A0% E6%95%88%E5%80%BC)
  -[Demo description](#demo%E8%AF%B4%E6%98%8E-3)
  -[Question Description] (#%E9%97%AE%E9%A2%98%E8%AF%B4%E6%98%8E-3)
  -[Quick Run](#%E5%BF%AB%E9%80%9F%E8%BF%90%E8%A1%8C-3)
-[:beer: Concurrency count without synchronization is wrong](#beer-%E6%97%A0%E5%90%8C%E6%AD%A5%E7%9A%84%E5%B9%B6%E5% 8F%91%E8%AE%A1%E6%95%B0%E7%BB%93%E6%9E%9C%E4%B8%8D%E5%AF%B9)
  -[Demo description](#demo%E8%AF%B4%E6%98%8E-4)
  -[Question Description] (#%E9%97%AE%E9%A2%98%E8%AF%B4%E6%98%8E-4)
  -[Quick Run](#%E5%BF%AB%E9%80%9F%E8%BF%90%E8%A1%8C-4)
-[:beer: synchronization on a variable domain](#beer-%E5%9C%A8%E6%98%93%E5%8F%98%E5%9F%9F%E4%B8%8A%E7% 9A%84%E5%90%8C%E6%AD%A5)
  -[Demo description](#demo%E8%AF%B4%E6%98%8E-5)
  -[Question Description] (#%E9%97%AE%E9%A2%98%E8%AF%B4%E6%98%8E-5)
  -[Quick Run](#%E5%BF%AB%E9%80%9F%E8%BF%90%E8%A1%8C-5)
-[:beer: Symmetrical lock deadlock](#beer-%E5%AF%B9%E7%A7%B0%E9%94%81%E6%AD%BB%E9%94%81)
  -[Demo description](#demo%E8%AF%B4%E6%98%8E-6)
  -[Question Description] (#%E9%97%AE%E9%A2%98%E8%AF%B4%E6%98%8E-6)
  -[Quick Run](#%E5%BF%AB%E9%80%9F%E8%BF%90%E8%A1%8C-6)
-[Some concurrent question discussion and information](#%E4%B8%80%E4%BA%9B%E5%B9%B6%E5%8F%91%E7%9A%84%E9%97%AE%E9 %A2%98%E8%AE%A8%E8%AE%BA%E5%92%8C%E8%B5%84%E6%96%99)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

-------------------------------------------------- ------------------------------

:beer: Unsynchronized changes will not be read in another thread
----------------------------------

Demo class [`com.oldratlee.fucking.concurrency.NoPublishDemo`](src/main/java/com/oldratlee/fucking/concurrency/NoPublishDemo.java).

### Demo description

Set the attribute `stop` to `true` in the main thread to control the exit of the task thread started in `main`.

### Problem description

After the main thread attribute `stop` is `true`, but the task thread continues to run, that is, no new value has been read in the task thread.

### Quick run

```bash
mvn compile exec:java -Dexec.mainClass=com.oldratlee.fucking.concurrency.NoPublishDemo
```

:beer: The infinite loop of `HashMap`
----------------------------------

This problem is explained in many places such as [Vaccine: The Infinite Loop of Java HashMap](http://coolshell.cn/articles/9606.html).
Demo class [`com.oldratlee.fucking.concurrency.HashMapHangDemo`](src/main/java/com/oldratlee/fucking/concurrency/HashMapHangDemo.java) can reproduce this problem.

### Demo description

Two task threads are opened in the main thread to execute the `put` operation of `HashMap`. The main thread does the `get` operation.

### Problem description

The main thread `Block` is determined by the lack of continuous output, that is, the occurrence of an infinite loop of `HashMap`.

### Quick run

```bash
mvn compile exec:java -Dexec.mainClass=com.oldratlee.fucking.concurrency.HashMapHangDemo
```

:beer: Combination status read invalid combination
----------------------------------

When programming, multiple status records are needed (the status can be a `POJO` object or an `int`, etc.). It is often seen that there is no synchronized code for multi-state reading and writing, and students who write will naturally ignore the problem of thread safety.

Invalid combinations are combinations that have never been set.

### Demo description

The main thread modifies multiple states. In order to facilitate inspection, each write has a fixed relationship: the second state is twice the value of the first state. Read multiple states in the task thread.
Demo class [`com.oldratlee.fucking.concurrency.InvalidCombinationStateDemo`](src/main/java/com/oldratlee/fucking/concurrency/InvalidCombinationStateDemo.java).

### Problem description

The task thread reads that the second state is not twice the value of the first state, which is an invalid value.

### Quick run

```bash
mvn compile exec:java -Dexec.mainClass=com.oldratlee.fucking.concurrency.InvalidCombinationStateDemo
```

:beer: `long` variable read invalid value
----------------------------------

Invalid values ​​are values ​​that have never been set.

Reading and writing of `long` variables is not atomic and will be divided into two 4-byte operations.
Demo class [`com.oldratlee.fucking.concurrency.InvalidLongDemo`](src/main/java/com/oldratlee/fucking/concurrency/InvalidLongDemo.java).

### Demo description

The main thread modifies the `long` variable. To facilitate checking, the upper 4 bytes and lower 4 bytes of the `long` value written each time are the same. Read the `long` variable in the task thread.

### Problem description

A `long` variable with different high 4 bytes and low 4 bytes read in the task thread is an invalid value.

### Quick run

```bash
mvn compile exec:java -Dexec.mainClass=com.oldratlee.fucking.concurrency.InvalidLongDemo
```

:beer: The result of unsynchronized concurrency counting is wrong
--------------
