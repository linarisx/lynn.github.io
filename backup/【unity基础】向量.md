# 向量模长和单位向量
## 基础概念

1. 两点之间得到向量
2. 一个点可以是和原点的向量

**向量模长：两点距离，向量长度
单位向量：单位为1的方向线路，与移动相关**

模长计算公式：根号下(x² + y² + z²)
单位向量计算：（x/模长， y/模长， z/模长）

## 代码相关
可以是点 也可以是向量
`Vector3 C = new(1,2,3);`

```c#
Vector3 A = new(1,7,3);
Vector3 B = new(4,2,3);
Vector3 AB = B - A;
Vector3 BA = A - B;
```

AB模长
`print(AB.magnitude);`

AB距离
`print(Vector3.Distance(A, B));`

OC模长（原点到C的模长）
`print(C.magnitude);`

AB单位向量
`print(AB.normalized);`

单位向量=向量/模长
`print(AB / AB.magnitude);`

# 向量的加减乘除
## 概念
向量 + 向量 = 向量（首尾相连连首尾）
位置 + 向量 = 位置（平移位置）

位置 - 位置 = 向量（终点 - 起点）
向量 - 向量 = 向量（头连头，尾指尾）
位置 - 向量 = 位置（平移位置）

向量乘除：用于模长的放大缩小

```c#
this.transform.localScale *= 2;
this.transform.localScale /= 2;
```

# 向量的点乘
## 基本概念
向量点乘 ： 另一个向量在该向量上的投影长度
公式：A·B = Xa * Xb + Ya * Yb + Za * Zb

点乘结果 > 0 夹角为锐角
点乘结果 = 0 夹角为直角
点乘结果 < 0 夹角为钝角

可以通过点乘结果来判断敌人是否在玩家前方
```c#
 result = Vector3.Dot(this.transform.forward, (target.position - this.transform.position));
 if(result >= 0)
 {
     print("敌人在前方");
 }
 else
 {
     print("敌人在后方");
 }
```

# 计算两个向量之间的角度
## 公式：
β = Acos(A单位向量 点乘 B单位向量) 0 - 180
## 代码：
```c#
result = Vector3.Dot(this.transform.forward, (target.position - this.transform.position).normalized);
print(Mathf.Acos(result) * Mathf.Rad2Deg);
```
另一种写法
`Vector3.Angle(this.transform.position, target.position - this.transform.position);`

# 叉乘
## 基本概念
A叉乘B得到一个新向量（新向量是AB平面的法向量）
X = YaZb - ZaYb   Y = ZaXb - XaZb   Z = XaYb - YaXb

<img width="609" height="273" alt="Image" src="https://github.com/user-attachments/assets/9ccf50db-bc4d-4bd5-8027-46f8596dca28" />

## 几何意义
这个新向量同时垂直于AB
A×B = -(B×A)

A×B
判断的是向量
y > 0 B在A右侧
y < 0 B在A左侧

<!-- Failed to upload "Snipaste_2026-04-30_15-46-59.png" -->
<img width="719" height="332" alt="Image" src="https://github.com/user-attachments/assets/0875a201-9fdc-4ba7-8def-6c17033bf2b7" />

## 代码
```c#
Vector3 C = Vector3.Cross(A.position, B.position);//叉乘
if(C.y > 0)
{
 print("B在A右侧");
}
else
{
 print("B在A左侧");
}
```

# 向量插值运算
## 基本概念
让一个位置移动到另一个位置（缓速/匀速）
result = start + (end-start)*t

和Mathf的区别：
Mathf.lerp是一个数字(二维)
vector3.lerp是向量(三位)

## 代码
### 缓速
`A.position = Vector3.Lerp(A.position, target.position, Time.deltaTime);`

### 匀速
当time>=1时，相当于与目标重合，或超出终点
```c#
if(nowTarget != target.position)//target改变了就会进这里
{           
    nowTarget = target.position;
    time = 0;
    startPos = B.position;
}
time += Time.deltaTime;
B.position = Vector3.Lerp(startPos, nowTarget, time);
```

### 球形差值
弧形轨迹（第三个参数区间是0~1的值）
`C.position = Vector3.Slerp(Vector3.right*10, Vector3.forward*10, time*0.1f);`