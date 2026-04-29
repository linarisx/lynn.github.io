# Camera摄像机相关
## 重要静态成员
如果有两个主摄像机就无法准确得到的是哪个
### 获取主摄像机
`print(Camera.main.name);`

### 取摄像机数量
`print(Camera.allCamerasCount);
`
### 得到所有摄像机
```c#
Camera[] arr = Camera.allCameras;
print(arr.Length);

```
### 渲染相关委托
摄像机剔除前处理的委托函数
`Camera.onPreCull += (c) => { };`
摄像机渲染前处理的委托
`Camera.onPreRender += (c) => { };`
摄像机渲染后处理的委托
`Camera.onPostRender += (c) => { };`

## 重要成员
获取界面上的参数
### 设置深度
`Camera.main.depth = 10;`

### 世界坐标转屏幕坐标
z轴是物体与摄像机的距离
做血条
`Vector3 v = Camera.main.WorldToScreenPoint(this.transform.position);`