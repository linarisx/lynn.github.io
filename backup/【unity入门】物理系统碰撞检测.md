# 物理系统碰撞检测
物理帧更新后检测物理碰撞触发相关函数 然后再执行逻辑帧更新
## 碰撞检测相关
### 碰撞触发接触（参数是碰自己的碰撞体）
```c#
private void OnCollisionEnter(Collision collision)
{
    //碰撞器
    collision.collider
    //对象
    collision.gameObject
    //位置
    collision.transform
    碰撞点数
    collision.contactCount
    碰撞点的坐标
    ContactPoint[] pos = collision.contacts;
    print(this.gameObject.name + "被" + collision.gameObject.name + "撞到了");
}
```
### 一直接触 有摩擦力
```c#
private void OnCollisionStay(Collision collision)
{
    print(this.gameObject.name + "和" + collision.gameObject.name + "一直接触");
}
```
### 退出接触
```c#
private void OnCollisionExit(Collision collision)
{
    print(this.gameObject.name + "被" + collision.gameObject.name + "结束碰撞");
}
```

## 触发器相关
### 开始触碰触发
```c#
private void OnTriggerEnter(Collider other)
{
    print(this.gameObject.name + "被" + other.gameObject.name + "接触到了");
}
```
### 重叠触发
```c#
private void OnTriggerStay(Collider other)
{
    print(this.gameObject.name + "一直在和" + other.gameObject.name + "重叠");
}
```
### 结束触碰触发
```c#
private void OnTriggerExit(Collider other)
{
    print(this.gameObject.name + "被" + other.gameObject.name + "结束接触了");
}
```
可以写虚函数来重写
重写的话写成projected就行了
unity自动通过反射帮我们调用