# 线程池核心线程数的估计

1. 一般说来，大家认为线程池的大小经验值应该这样设置：（其中N为CPU的个数）  


   * 如果是CPU密集型应用，则线程池大小设置为N+1
   * 如果是IO密集型应用，则线程池大小设置为2N+1

   如果一台服务器上只部署这一个应用并且只有这一个线程池，那么这种估算或许合理，具体还需自行测试验证。  
   但是，IO优化中，这样的估算公式可能更适合：  
   最佳线程数目 = （（线程等待时间+线程CPU时间）/线程CPU时间 ）\* CPU数目  
   因为很显然，**线程等待时间所占比例越高，需要越多线程。线程CPU时间所占比例越高，需要越少线程。**  
   下面举个例子：  
   比如平均每个线程CPU运行时间为0.5s，而线程等待时间（非CPU运行时间，比如IO）为1.5s，CPU核心数为8，那么根据上面这个公式估算得到：\(\(0.5+1.5\)/0.5\)\*8=32。这个公式进一步转化为：  
   **最佳线程数目 = （线程等待时间与线程CPU时间之比 + 1）\* CPU数目**

**CPU密集型（CPU-bound）**

* CPU密集型也叫计算密集型，指的是系统的硬盘、内存性能相对CPU要好很多，此时，系统运作大部分的状况是CPU Loading 100%，CPU要读/写I/O\(硬盘/内存\)，I/O在很短的时间就可以完成，而CPU还有许多运算要处理，CPU Loading很高。
* 在多重程序系统中，大部份时间用来做计算、逻辑判断等CPU动作的程序称之CPU bound。例如一个计算圆周率至小数点一千位以下的程序，在执行的过程当中绝大部份时间用在三角函数和开根号的计算，便是属于CPU bound的程序。
* CPU bound的程序一般而言CPU占用率相当高。这可能是因为任务本身不太需要访问I/O设备，也可能是因为程序是多线程实现因此屏蔽掉了等待I/O的时间

**IO密集型（I/O bound）**

* IO密集型指的是系统的CPU性能相对硬盘、内存要好很多，此时，系统运作，大部分的状况是CPU在等I/O \(硬盘/内存\) 的读/写操作，此时CPU Loading并不高。
* I/O bound的程序一般在达到性能极限时，CPU占用率仍然较低。这可能是因为任务本身需要大量I/O操作，而pipeline做得不是很好，没有充分利用处理器能力。
