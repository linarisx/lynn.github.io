 # 角度相关
相对世界坐标角度
`print(this.transform.eulerAngles);`
相对父对象角度
`print(this.transform.localEulerAngles);`
不能单独改变一个坐标 三个一起
`this.transform.localEulerAngles = new Vector3(10, 10, 10);`

# 旋转
第一个参数 旋转的角度
第二个参数 默认不填围绕自己旋转
```
this.transform.Rotate(new Vector3(0, 10, 0) * Time.deltaTime);
this.transform.Rotate(new Vector3(0, 10, 0) * Time.deltaTime, Space.World);
```

相对于轴转多少度
参数一：相对于哪个轴转动
参数二：角度
参数三：默认自己坐标系
`this.transform.Rotate(Vector3.right, 10 * Time.deltaTime);`

相对于某一个点转
参数一：相对于哪一个点转圈圈
参数二：相对于那一个点的 哪一个轴转圈圈
参数三：转的度数 旋转速度*时间
`this.transform.RotateAround(Vector3.zero, Vector3.right, 10 * Time.deltaTime);`
