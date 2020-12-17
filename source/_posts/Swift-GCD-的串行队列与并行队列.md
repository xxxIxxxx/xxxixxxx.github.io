---
title: Swift GCD 的串行队列与并行队列
categories: [Swift]
tags: [GCD,多线程]
+ sticky:  #9999
---

队列|异步是否阻塞当前线程|同步是否阻塞当前线程|执行顺序
-|-|-|-
串行队列|否|是|按添加顺序
并行队列|否|是|同时执行，但会被同步阻塞

# 串行队列异步任务不会阻塞线程，同步会阻塞当前线程，执行顺序按添加顺序


# 并行队列异步任务不会阻塞线程，同步会阻塞当前线程，同时执行，但会被同步阻塞
---
# 串行队列
```
let queue = DispatchQueue(label: "queue")
print("------ 开始 -------")
queue.async {
    Thread.sleep(forTimeInterval: 3)
    print("------ async 1 -------")
}

print("------ async 1 不阻塞 -------")

queue.async {
    print("------ async 2 -------")
}

queue.sync {
    Thread.sleep(forTimeInterval: 3)
    print("------ sync 1 -------")
}

print("------ 被 sync 1 阻塞 -------")

queue.async {
    print("------ async 3 -------")
}

------ 开始 -------
------ async 1 不阻塞 -------
------ async 1 -------
------ async 2 -------
------ sync 1 -------
------ 被 sync 1 阻塞 -------
------ async 3 -------
```
# 并行队列
```
let queue = DispatchQueue(label: "queue", attributes: DispatchQueue.Attributes.concurrent)
print("------ 开始 -------")
queue.async {
    Thread.sleep(forTimeInterval: 3)
    print("------ async 1 -------")
}

print("------ async 1 不阻塞 -------")

queue.async {
    print("------ async 2 -------")
}

queue.sync {
    Thread.sleep(forTimeInterval: 5)
    print("------ sync 1 -------")
}

print("------ 被 sync 1 阻塞 -------")

queue.async {
    print("------ async 3 -------")
}

------ 开始 -------
------ async 1 不阻塞 -------
------ async 2 -------
------ async 1 -------
------ sync 1 -------
------ 被 sync 1 阻塞 -------
------ async 3 -------
```
