# 【unity入门】生命周期函数

## 基本概念
unity会按顺序执行以下生命周期函数
`Awake()`
`OnEnable()`
`Start()`
`FixedUpdate()`
`Update()`
`LateUpdate()`
`OnDisable()`
`OnDestroy()`


### Awake和Start的区别
1.当物体失活，脚本激活时Awake仍然执行，只要对象创建并且脚本激活就会执行
2.Start必须在物体处于激活状态才会执行

### 物理帧更新`FixedUpdate()`
可以在ProjectSetting中的Time设置，代表间隔几秒执行一次

### 其他
只要脚本失活所有函数都不执行

```c#
private void Awake()
{
    print("Awake 该类的对象被创建时");       
}
private void OnEnable()
{
    print("OnEnable 激活时调用");
}
private void Start()
{
    print("Start");
}
private void FixedUpdate()
{
    print("FixedUpdate");
}
private void Update()
{
    print("Update");
}
private void LateUpdate()
{
    print("LateUpdate");
}
private void OnDisable()
{
    print("OnDisable失活");
}
private void OnDestroy()
{
    print("OnDestroy删除");
}
```