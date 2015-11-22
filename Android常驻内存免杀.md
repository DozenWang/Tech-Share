####Android 常驻内存的方案总结
当系统内存非常紧张并且轮到 Service 进程被杀的时候，这是无可避免的。在系统的限制下我们可以从两个方面考虑
  - 尽量提高进程的优先级，保证不被轻易的Kill
  - 被系统回收后, 等待系统资源充足的时候重新启动进程
  
 前者可以通过startForgroundService 把service置为前台进程，独立service进程，尽量降低service进程的内存占用**Android LowMemoryKiller机制在同一优先级的情况下回优先回收内存占用高的进程**

 后者可以通过onStartCommand 返回START_STICKY 实现 同时还可以监听系统的状态，比如网络状态，使用AlarmManager定时的唤醒

