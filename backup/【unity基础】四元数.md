# 四元数
## 为何使用四元数
四元数可以解决的问题
普通旋转会出现万向节死锁，也就是三位变成只有二维旋转
一个物体方向能有多个欧拉角角度 比如90,450,等等

## 四元数的使用

<img width="265" height="169" alt="Image" src="https://github.com/user-attachments/assets/2d22f2e6-b661-46c9-9bc3-f0306c3b9ff6" />

<img width="492" height="251" alt="Image" src="https://github.com/user-attachments/assets/afaaf22d-78a2-4143-b537-7f03f3e2e620" />


###  四元数初始化

<img width="383" height="181" alt="Image" src="https://github.com/user-attachments/assets/e5d18617-fe1e-4b10-bdcd-f15cc8302e07" />

`Quaternion q = new Quaternion(0, Mathf.Sin(30 * Mathf.Deg2Rad) * 1, 0, Mathf.Cos(30 * Mathf.Deg2Rad));`
**`Quaternion q = Quaternion.AngleAxis(60, Vector3.up);`**

```c#
GameObject obj = GameObject.CreatePrimitive(PrimitiveType.Cube);
obj.transform.rotation = q;
```

### 四元数欧拉角的转换
欧拉转四元
```c#
Quaternion q2 = Quaternion.Euler(60, 0, 0);
GameObject obj2 = GameObject.CreatePrimitive(PrimitiveType.Cube);
obj2.transform.rotation = q2;
```
四元转欧拉
`print(q2.eulerAngles);`

## 四元数的常用用法
### 单位四元数
旋转角度(0,0,0) 标量1/-1
`print(Quaternion.identity);`

### 插值运算
让一个物体旋转成跟目标物体一样的角度
**1. 缓速**
`A.rotation = Quaternion.Slerp(A.rotation, target.transform.rotation, Time.deltaTime);`
**2. 匀速**
```
time += Time.deltaTime;
B.rotation = Quaternion.Slerp(startB, target.transform.rotation, time);
```

### LookRotation
传入一个向量，让一个物体旋转至那个向量的方向，以至于一直看向那个物体
返回的是一个旋转角度
`C.rotation = Quaternion.LookRotation(D.position - C.position);`

## 四元数的计算
### 旋转
相对于自己坐标系旋转30度
`this.transform.rotation *= Quaternion.AngleAxis(60, Vector3.up);`

### 旋转向量
旋转后的向量 = 四元数 * 向量
```c#
Vector3 v = Vector3.forward;
v = Quaternion.AngleAxis(45, Vector3.up) * v; 
```