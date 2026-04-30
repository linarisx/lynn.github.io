# Debug
不用继承MonoBehaviour

## 打印
`Debug.Log("打印的信息");`

`Debug.LogError("出错误了！");`

`Debug.LogWarning("警告！");`

## 绘制射线 线段
画射线 起点 方向 颜色
`Debug.DrawRay(this.transform.position, this.transform.forward, Color.red);`

画线段 起点 终点 颜色
`Debug.DrawLine(this.transform.position, target.transform.position, Color.red);`