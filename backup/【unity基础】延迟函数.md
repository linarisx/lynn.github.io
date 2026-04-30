# 延迟函数
## 延迟函数
### 延迟两秒执行
`Invoke("Delay", 2);`
### 第一次两秒后执行，之后每一秒执行一次
`InvokeRepeating("RepeatingDaley", 2, 1);`

延迟函数只能是无参或该类里的函数，其他得包裹才能执行

## 取消延迟函数
取消没有执行的延迟函数，不会报错
### 取消所有延迟函数
`CancelInvoke();`

### 取消指定延迟函数
同名全部一起取消
`CancelInvoke("Delay");
`
### 判断是否有延迟函数
```c#
if (IsInvoking())
{
    print("存在延迟函数");
}
if (IsInvoking("RepeatingDaley"))
{
    print("存在延迟函数RepeatingDaley");
}
```

## 注意
失活该脚本挂载的对象和 该脚本，延迟函数仍然执行
删除脚本和该对象，延迟函数不再执行

所以可以通过生命周期函数来控制失活时的延迟函数是否执行
```c#
private void OnEnable()
{
   InvokeRepeating("RepeatingDaley", 2, 0.5f);
}
private void OnDisable()
{
   CancelInvoke("RepeatingDaley");
}
```