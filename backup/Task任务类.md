 # 概念

Task的本质是对线程Thread的封装 它的创建遵循线程池的优点并且可以更方便的让我们控制线程
一个Task对象就是一个线程

# 三种创建无返回值线程的方式
如果要返回值直接加泛型在后面 可省略
``` c#
private bool isRuning = true;
Task<int> t1;
Task<float> t2;
Task<string> t3;
void Start()
{

    t1 = new Task<int>(() =>
    {
        int i = 0;
        while (isRuning)
        {
            print("t1" + i);
            i++;
            Thread.Sleep(1000);
        }
        return 1;
    });

    t2 = Task.Run<float>(() =>
    {
        int i = 0;
        while (isRuning)
        {
            print("t2" + i);
            i++;
            Thread.Sleep(1000);
        }
        return 1.2f;
    });

    t3 = Task.Factory.StartNew<string>(() =>
    {
        int i = 0;
        while (isRuning)
        {
            print("t2" + i);
            i++;
            Thread.Sleep(1000);
        }
        return "123";
    });
}
private void OnDestroy()
{
    isRuning = false;
    //注意：如果result写在while循环还在运行的地方会卡主，因为副线程的while还没result返回出来，主线程会一直等
    print(t1.Result);
    print(t2.Result);
    print(t3.Result);
} 
```

# 同步执行
执行完线程再执行主线程，按顺序同步执行
Run和newStart在创建时就启动了所以没有同步执行
 ``` c#
Task t = new Task(() =>
 {
     print("hhh");
 });
 //t.Start();异步执行，各执行各的
 t.RunSynchronously();
 print("主线程");
```
# 线程阻塞的方法
1. t1.Wait();
t1线程执行完执行后面的
2. Task.WaitAny(t1,t2);
t1/t2其中一个执行完就执行主线程
3. Task.WaitAll(t1 ,t2);
等执行完全部 继续执行
``` c#
Task t1 = Task.Run(() =>
{
    for (int i = 0; i < 10; i++)
    {
        print("一"+i);
    }
});
Task t2 = Task.Run(() =>
{
    for (int i = 0; i < 20; i++)
    {
        print("二"+i);
    }
});
t1.Wait();//等待t1这个线程执行完才执行主线程

//WaitAny
Task.WaitAny(t1,t2); //t1/t2其中一个执行完就执行主线程
//WaitAll
Task.WaitAll(t1 ,t2); //等执行完全部
print("主线程");
```