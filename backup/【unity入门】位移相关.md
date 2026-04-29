# 位移相关
## Vector3基础
三维坐标的一个点，向量
### 申明一个点
```c#
Vector3 v = new Vector3();
v.x = 10;
v.y = 10;
v.z = 10;
```
只传xy，默认z为零
`Vector3 v2 = new Vector3(10, 10);`
一步到位
`Vector3 v3 = new Vector3(10, 10, 10);`

```c#
Vector3 v4;
v4.x = 10;
v4.y = 10;
v4.z = 10;
```

### 加减乘除
```c#
Vector3 v1 = new Vector3(1, 1, 1);
Vector3 v12 = new Vector3(2, 2, 2);
print(v1 + v12);
print(v1 - v12);

print(v1 * 10);
print(v12 / 2);

print(Vector3.zero);//000

print(Vector3.right);//100
print(Vector3.left);//-100

print(Vector3.forward);//001
print(Vector3.back);//00-1

print(Vector3.up);//010
print(Vector3.down);//0-10
```

### 计算两点之间的距离
`print(Vector3.Distance(v1,v12));
`

## 位置
### 相对世界坐标系
`print(this.transform.position);`
### 相对父对象
`print(this.transform.localPosition);`

位置不能单独修改一个，只能整体三个数值都一起改变
```c#
this.transform.position = new Vector3(10, 10, 10);
this.transform.localPosition = Vector3.up * 10;
```

如果想只改变一个值
`this.transform.position = new Vector3(10, this.transform.position.y, this.transform.position.z);`
取出来再改
```c#
Vector3 vv = this.transform.localPosition;
vv.x = 100;
```

### 获取当前对象的方向
```c#
print(this.transform.forward);
print(this.transform.up);
print(this.transform.right);
```

## 位移
`this.transform.position += this.transform.forward * 1 * Time.deltaTime;
`
API
第一个参数：路程 = 方向*速度*时间
第二个参数：相对于世界/自己的坐标系

世界的世界 = 世界
`this.transform.Translate(Vector3.forward * 1 * Time.deltaTime, Space.World);`

世界的自己 = 自己
`this.transform.Translate(this.transform.forward * 1 * Time.deltaTime, Space.World);`

自己世界坐标下的自己坐标系 （十分的奇怪，不会这样让物体动）
`this.transform.Translate(this.transform.forward * 1 * Time.deltaTime, Space.Self);`

自己的世界 = 自己面朝向
`this.transform.Translate(Vector3.forward * 1 * Time.deltaTime, Space.Self);`