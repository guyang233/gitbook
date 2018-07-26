# 线程池的好处

## 1、合理利用线程池带来的好处

1. 降低资源消耗：通过重复零以创建的线程，降低线程和销毁造成的消耗
2. 提高响应速度：当任务到达时，任务可以不需要等待线程创建就能立即执行
3. 提高线程的可管理性：线程池可以统一的分配、调优和监控。
4. 防止服务器过载：形成内存溢出，或者CPU耗尽。

## 2、如何提高服务器程序的性能

1. 多线程技术主要解决处理器单元内多个线程执行的问题，可以显著的减少处理器单元的闲置时间，增加处理器单元的吞吐能力。但是如果使用不当，会增加对单个任务的处理时间。

## 3、线程池的应用范围

1. 需要大量的线程来完成任务、且完成任务的时间比较短
2. 对性能要求苛刻的应用，比如要求服务器迅速的响应客户请求
3. 接收突发性的大量的请求，但不至于是服务器因此产生大量线程的应用。

## 


