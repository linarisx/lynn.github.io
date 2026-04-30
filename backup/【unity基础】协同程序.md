# 协同程序
## 基本使用
### 开启协程
`StartCoroutine(MyCoroutine(1, "小林"));`
`IEnumerator ie = MyCoroutine(1, "小林");`
可以一次开多个
```
Coroutine c1 = StartCoroutine(MyCoroutine(1, "小林"));
Coroutine c2 = StartCoroutine(MyCoroutine(1, "小林"));
Coroutine c3 = StartCoroutine(MyCoroutine(1, "小林"));
```

### 关闭所有协程
`StopAllCoroutines();`

### 关闭一个指定协程
`StopCoroutine(c1);
`
### 协程相关代码
```c#
IEnumerator MyCoroutine(int i, string str)
{
  print(i);
  yield break;//跳出协程（相当于停止了）
  print(i);
  yield return new WaitForSeconds(2);//等2秒执行下部分
  print(str);
  yield return new WaitForSeconds(2);//等2秒执行下部分
  print("2");
  yield return new WaitForSeconds(2);//等2秒执行下部分
  print("3");

  //可以写循环
  while (true)
  {
      print("5");
      yield return new WaitForSeconds(1);//每隔一秒打印一次5（每个一秒执行一次这个循环）
  }
}

```
### 类型

1. 等2秒执行下部分
yield return new WaitForSeconds(2);
在Update和LateUpdate之间执行

2. 下一帧执行
yield return null; /yield return 数字;
在Update和LateUpdate之间执行

3. 等待下一个固定物理帧更新时执行
yield return new WaitForFixedUpdate();
在FixedUpdate和碰撞检测相关函数之后执行

4. 等待摄像机和GUI渲染完成后执行
yield return new WaitForEndOfFrame();

5. 在LateUpdate之后的渲染相关处理完毕后执行
yield return new WaitForEndOfFrame();
截图

6. 一些特殊类型的对象，比如异步加载相关函数返回的对象
一般在Update和LateUpdate之间执行

### 注意
挂载的对象和脚本被删除，失活对象，协程不执行
失活脚本协程仍然执行

## 协程原理
迭代器
```c#
IEnumerator ie = MyCoroutine();
print(ie.Current);
ie.MoveNext(); //1
print(ie.Current); //11
ie.MoveNext();
print(ie.Current); //12
ie.MoveNext();
print(ie.Current); //Test;
Test t = ie.Current as Test;
print(t.time); //10

while (ie.MoveNext())//返回true代表还有下一个值
{
   print(ie.Current);
}
```
```c#
IEnumerator MyCoroutine()
{
   print("1");
   yield return 11;
   yield return 12;
   yield return new Test(10);
}
```