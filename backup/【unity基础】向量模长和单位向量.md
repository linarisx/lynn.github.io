# 单位模长和单位向量
## 基础概念

1. 两点之间得到向量
2. 一个点可以是和原点的向量

向量模长：两点距离，向量长度
单位向量：单位为1的方向线路，与移动相关

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