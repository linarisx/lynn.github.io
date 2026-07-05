<img width="1350" height="372" alt="Image" src="https://github.com/user-attachments/assets/3ba8a3b7-2de6-4f81-865c-e5dc5e0a6060" />

<img width="1408" height="531" alt="Image" src="https://github.com/user-attachments/assets/25b7c934-24ac-474f-be68-c82f3d03e461" />

# 解决办法
``` c#
class A { }
class B { }
class C { }
class IL2CPP_Info
{
    List<A> a;
    List<B> b;
    List<C> c;//在这里就代表调用过了 不会被剔除

    //泛型 有什么需求就提前声明
    Dictionary<int, string> dic = new Dictionary<int, string>();

    //泛型方法 在静态方法中调用一下就能解决
    public void Test<T>(T i)
    {

    }
    public static void stTest()
    {
        IL2CPP_Info info = new IL2CPP_Info();
        info.Test<int>(10);
        info.Test<float>(10f);
        info.Test<bool>(true);
    }
}
```