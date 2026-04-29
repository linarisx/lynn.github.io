## 世界坐标系转本地坐标系
### 点的转换
受缩放影响
`print("转换后的点" + this.transform.InverseTransformPoint(Vector3.forward));`

### 方向向量的转换
不受缩放影响
`print("转换后的方向" + this.transform.InverseTransformDirection(Vector3.forward));`
受缩放影响
`print("转换后的方向" + this.transform.InverseTransformVector(Vector3.forward));`

## 本地转世界
### 点的转换
受缩放影响
`print("本地转世界的点" + this.transform.TransformPoint(Vector3.forward));
`
### 方向
不受缩放影响
`print("本地转世界的方向" + this.transform.TransformDirection(Vector3.forward));`
受缩放影响
`print("本地转世界的方向" + this.transform.TransformVector(Vector3.forward));`