# Mono
<img width="1615" height="809" alt="Image" src="https://github.com/user-attachments/assets/1607844a-dffd-4dfe-8739-0004eea4d0a9" />

### **unity如何利用Mono实现跨平台？**

**Unity中C#脚本先被编译成IL中间语言，然后由Mono运行时加载这些程序集。在运行时，Mono根据不同平台选择JIT或AOT方式将IL转换为当前设备的机器码执行，从而实现跨平台。**

**Mono在其中的作用**
Mono可以理解为 Unity 早期/经典的 .NET 运行时实现，它负责：

**1️⃣ C# → IL（中间语言）**
你写的 C# 代码会先被编译成：
IL（Intermediate Language）
存在于 Assembly-CSharp.dll 之类的程序集里

这一步是“跨平台的关键”

**2️⃣ Mono Runtime 负责执行 IL**
Mono有两种执行方式：
✔ JIT（即时编译）
运行时把 IL 转成当前平台的机器码
优点：性能好、动态
缺点：某些平台（如 iOS）禁止 JIT
✔ AOT（提前编译）
在发布前直接把 IL 编译成机器码
iOS / 主机平台通常用这个

<img width="1693" height="742" alt="Image" src="https://github.com/user-attachments/assets/e222339b-d56c-422b-94ff-d8f5f91e4699" />


# IL2CPP
<img width="1740" height="735" alt="Image" src="https://github.com/user-attachments/assets/01e529ad-92d9-488c-a6be-5c198fd81359" />

## uinty是如何利用IL2CPP进行跨平台的
Unity使用IL2CPP实现跨平台时，首先将C#代码编译为IL中间语言，然后通过IL2CPP工具把IL转换为C++代码，最后由各个平台的原生C++编译器生成对应机器码执行。由于不同平台只需要支持C++编译器，因此实现了一次开发、多平台发布。同时IL2CPP采用AOT方式，避免了JIT限制，提高了安全性和性能。

## 虚拟机的作用
主要用来完成GC管理和线程管理等服务工作， 和C#里面的工作点的是一样的。通过模拟c#的垃圾回收机制来管理通过C++编译成的机器码

<img width="1679" height="696" alt="Image" src="https://github.com/user-attachments/assets/75f15bdf-dadf-4f40-b5ea-67a556e9d3f9" />

<img width="1622" height="711" alt="Image" src="https://github.com/user-attachments/assets/26e1a468-3a14-4c06-a8a4-754a6a464420" />

## IL2CPP执行效率高的原因
1. 提前编译AOT，代码提前编译好，不需要边编译边执行
2. c++代码比中间语言代码效率高

**IL2CPP 通常比 Mono 更高效，因为它是 AOT 模式，提前将 IL 编译为本地机器码，避免了 JIT 运行时编译开销，并且可以利用更强的 C++ 编译器优化。但 Mono 在运行时可以做动态优化，因此在某些场景下也可能接近甚至优于 IL2CPP。**

<img width="1232" height="439" alt="Image" src="https://github.com/user-attachments/assets/5413a8a3-b484-42ff-9a9d-0723b55dbe44" />