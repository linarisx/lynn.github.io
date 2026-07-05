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

## IL2CPP 模式打包是， 代码剥离可能造成的问题，如何解决
IL2CPP 是 AOT 模式，Unity 在打包时会进行代码裁剪（Stripping），删除静态分析认为未使用的代码。但反射、字符串调用、泛型实例化等运行时行为无法被静态分析识别，可能导致类或方法被错误剥离，从而出现 MissingMethod 或 Type not found 等问题。解决方法通常是使用 link.xml、[Preserve] 特性或增加显式引用来避免代码被裁剪。