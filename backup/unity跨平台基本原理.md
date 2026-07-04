<img width="1615" height="809" alt="Image" src="https://github.com/user-attachments/assets/1607844a-dffd-4dfe-8739-0004eea4d0a9" />
unity如何利用Mono实现跨平台？
Unity中C#脚本先被编译成IL中间语言，然后由Mono运行时加载这些程序集。在运行时，Mono根据不同平台选择JIT或AOT方式将IL转换为当前设备的机器码执行，从而实现跨平台。

Mono在其中的作用
Mono可以理解为 Unity 早期/经典的 .NET 运行时实现，它负责：

1️⃣ C# → IL（中间语言）
你写的 C# 代码会先被编译成：
IL（Intermediate Language）
存在于 Assembly-CSharp.dll 之类的程序集里

这一步是“跨平台的关键”

2️⃣ Mono Runtime 负责执行 IL
Mono有两种执行方式：
✔ JIT（即时编译）
运行时把 IL 转成当前平台的机器码
优点：性能好、动态
缺点：某些平台（如 iOS）禁止 JIT
✔ AOT（提前编译）
在发布前直接把 IL 编译成机器码
iOS / 主机平台通常用这个