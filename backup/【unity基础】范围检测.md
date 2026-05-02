# 范围检测
用于检测一个范围，一般瞬时检测
## 立方体检测
参数：
（中心点，立方体长宽高大小(以中心点向各个方向延伸的距离)，旋转角度，层级(默认检测所有层)，是否忽略检测触发器(默认全局)）
```c#
Collider[] colliders = Physics.OverlapBox(Vector3.zero, Vector3.one * 0.5f,
                       Quaternion.identity,
                       1 << LayerMask.NameToLayer("UI") | 1 << LayerMask.NameToLayer("Default"),
                       QueryTriggerInteraction.UseGlobal);
for (int i = 0; i < colliders.Length; i++)
{
    //这里的colliders是得到该对象身上的碰撞器
    print("检测到" + colliders[i].gameObject.name);
}
```

### 检测碰撞器数量
第三个参数传个数组接收检测到的碰撞器
```c#
if (Physics.OverlapBoxNonAlloc(Vector3.zero, Vector3.one * 0.5f, colliders) != 0)
{

}
```
## 球形检测
参数：中心点，半径
```c#
Physics.OverlapSphere(Vector3.zero, 5, 1 << LayerMask.NameToLayer("Default"), QueryTriggerInteraction.UseGlobal);
if (Physics.OverlapSphereNonAlloc(Vector3.zero, 5, colliders) != 0) { }
```

## 胶囊体检测
参数：第一个圆的中心点，第二个圆的中心点，半径
```c#
Physics.OverlapCapsule(Vector3.zero, Vector3.forward, 2);
if(Physics.OverlapCapsuleNonAlloc(Vector3.zero, Vector3.forward,2, colliders) != 0) { }
```

## 层级相关内容
左移 代表32位中每一位都是一个层级编号，刚好int就是32位，一共有32个层级
编号 -> 1左移n位
0 —— 1 << 0000 0000 0000 0000 0000 0000 0000 0001 = 1 
1 —— 1 << 0000 0000 0000 0000 0000 0000 0000 0010 = 2
2 —— 1 << 0000 0000 0000 0000 0000 0000 0000 0100 = 4 
3 —— 1 << 0000 0000 0000 0000 0000 0000 0000 1000 = 8 
4 —— 1 << 0000 0000 0000 0000 0000 0000 0001 0000 = 16 
5 —— 1 << 0000 0000 0000 0000 0000 0000 0010 0000 = 32 

### 表示同时检测这两层层级
`1 << LayerMask.NameToLayer("UI") | 1 << LayerMask.NameToLayer("Default"),`
0010 0000 = 32
0000 0001 = 1
**进行或(|)运算 有一则一**
计算结果 0010 0001 = 33 //代表两层
unity内部将每一层与0010 0001进行与(&)运算 同为1就取1
只要结果不为0，那就代表有这一层

### 检测除了该层以外的所有层

1. 用该层进行异或位运算(**异或 ^ 相同为0 不同为1**)
`LayerMask mask = ~0 ^ (1 << LayerMask.NameToLayer("Default"));`//~0：32个1，代表检测所有层
1111 1111 1111 1111 1111 1111 1111 1111//~0
0000 0000 0000 0000 0000 0000 0000 0001//1 << LayerMask.NameToLayer("UI"))
1111 1111 1111 1111 1111 1111 1111 1110//异或的结果

2 直接取反 
`mask = ~(1 << LayerMask.NameToLayer("Default"));`