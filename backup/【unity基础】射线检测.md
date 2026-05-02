# 射线检测
## 射线的定义
### 定义一个3d射线，（原点，方向）
```c#
Ray r = new Ray(Vector3.zero, Vector3.forward);
print(r.origin);//原点
print(r.direction);//方向
```

### 摄像机发出的射线（屏幕发射）
`Ray r2 = Camera.main.ScreenPointToRay(Input.mousePosition);
`
## 射线检测
`Ray r3 = new Ray(Vector3.zero, Vector3.forward);`
### 传入一个射线
返回值bool 判断是否有检测到对象
（射线，检测距离，层级，是否忽视碰撞器）
```c#
if (Physics.Raycast(r3, 1000, 1 << LayerMask.NameToLayer("Monster"), QueryTriggerInteraction.UseGlobal))
{
    print("检测到");
}
```
### 直接传入起点和方向
```c#
if (Physics.Raycast(Vector3.zero, Vector3.forward, 1000, 1 << LayerMask.NameToLayer("Monster"), QueryTriggerInteraction.UseGlobal))
{
    print("检测到");
}
```

## 获取检测到的对象信息
### 传入射线
物体信息
`RaycastHit rayInfo;`
（射线， out进去赋值传出来， 距离， 层级， 是否检测碰撞器）
```c#
if (Physics.Raycast(r3, out rayInfo, 1000, 1 << LayerMask.NameToLayer("Monster"), QueryTriggerInteraction.UseGlobal))
{
    print("碰撞到物体检测到信息");

    print("碰撞到物体的名字" + rayInfo.collider.gameObject.name);

    print("碰撞到物体的点" + rayInfo.point);

    //射到的点和平面的法线
    print("法线信息" + rayInfo.normal);

    print("碰撞的对象位置" + rayInfo.transform.position);

    print("碰撞的对象离射线起点的距离" + rayInfo.distance);
    //时间 = 距离 / 速度
    //可以计算自由下落的距离 = 时间 * 重力加速度
}
```
### 直接传入起点和方向
`if (Physics.Raycast(Vector3.zero, Vector3.forward, out rayInfo, 1000, 1 << LayerMask.NameToLayer("Monster"), QueryTriggerInteraction.UseGlobal)) { }`

## 获取相交的多个物体对象(穿透)
### 传入
```c#
RaycastHit[] objs = Physics.RaycastAll(r3, 1000, 1 << LayerMask.NameToLayer("Monster"), QueryTriggerInteraction.UseGlobal);
for (int i = 0; i < objs.Length; i++)
{
    print("碰到的物体名" + objs[i].collider.gameObject.name);
}
```
### 直接传入起点和方向
`RaycastHit[] objs2 = Physics.RaycastAll(Vector3.zero, Vector3.forward, 1000, 1 << LayerMask.NameToLayer("Monster"), QueryTriggerInteraction.UseGlobal);`

## 返回碰撞的数量
```c#
if (Physics.RaycastNonAlloc(r3, objs, 1000, 1 << LayerMask.NameToLayer("Monster"), QueryTriggerInteraction.UseGlobal) > 0)
{
    print("碰撞数量");
}
```