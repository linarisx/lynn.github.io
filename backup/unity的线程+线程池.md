# 线程
不能使用主线程的对象
必须关闭
``` c#
Thread t;        
        t = new Thread(() =>
        {
            while (true)
            {
                print("副线程");
                Thread.Sleep(1000);
            }
        });
        t.Start();
        print("主线程");
    private void OnDestroy()
    {
        t.Abort();
    }
```
# 线程池
一个装线程的缓存池
从线程池中取线程使用，当线程池中的线程都忙碌，才会新开线程处理新任务
如果线程数量达到最大，任务排队，等待到其他任务释放线程后再执行

减少GC，但无法获得执行顺序和线程状态的通知

<img width="1114" height="511" alt="Image" src="https://github.com/user-attachments/assets/f3ec5927-3009-4a1e-89df-20cb8ccf476c" />

``` c#
 int num1;
 int num2;
//工作线程数和I/O线程数
 ThreadPool.GetAvailableThreads(out num1, out num2);
 print(num1);
 print(num2);


 if (ThreadPool.SetMaxThreads(50, 50))
 {
     print("更改可用于活动的最大线程数量");
 }
 ThreadPool.GetMaxThreads(out num1, out num2);
 print(num1);
 print(num2);


 if (ThreadPool.SetMinThreads(5, 5))
 {
     print("更改可用于活动的最小线程数量");
 }
 ThreadPool.GetMinThreads(out num1, out num2);
 print(num1);
 print(num2);

 for(int i = 0; i < 10; i++)
 {
     //将方法排入队列，当线程池中的线程可用之后执行
     ThreadPool.QueueUserWorkItem((obj) =>
     {
         //obj的值是i的值，无顺序
         print("第" + i + "个任务线程");
     }, i);
 }
 print("主线程");
```