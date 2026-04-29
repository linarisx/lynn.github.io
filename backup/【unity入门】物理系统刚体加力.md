# 物理系统刚体加力
`Rigidbody rigidBody;`
### 获取刚体组件
` rigidBody = GetComponent<Rigidbody>();`
### 增加力
**1.相对世界坐标系 第二个参数：力的模式**
```c#
rigidBody.AddForce(Vector3.forward * 10);
rigidBody.AddForce(this.transform.forward * 10); ;//相对自己坐标系
```

**2.相对本地坐标系 第二个参数：力的模式**
` rigidBody.AddRelativeForce(Vector3.forward * 10);`

### 扭矩的力
**1.相对世界坐标系 第二个参数：力的模式**
`rigidBody.AddTorque(Vector3.up * 10);`
**2.相对本地坐标系 第二个参数：力的模式**
`rigidBody.AddRelativeTorque(Vector3.up * 10);`

### 改变速度
相对世界坐标系
`rigidBody.velocity = Vector3.forward * 5;`

### 爆炸效果
(力的大小，爆炸中心，爆炸半径)
`rigidBody.AddExplosionForce(100, Vector3.zero, 10);`

## 力的模式
动量定理
Ft = mv
v = Ft / m

### Force 持续的力
与时间 质量有关
v = 10 * 0.02 / 2 = 0.1m / s
每物理帧移动：0.1m / s * 0.02 = 0.002m

###Acceleration 持续加速度
忽略质量(默认m = 1)
v = (0, 0, 10) * 0.02 / 1 = 0.2m / s
每物理帧移动：0.2m / s * 0.02 = 0.004m

### Impulse 瞬间的力
忽略时间(默认t = 1)
v = 10 * 1 / 2 = 5m / s
每物理帧移动：5m / s * 0.02 = 0.1m

### VelocityChange 瞬时速度
忽略质量 时间
v = 10 * 1 / 1 = 10m / s
每物理帧移动：10m / s * 0.02 = 0.2m

```c#
rigidBody.AddForce(Vector3.forward * 10, ForceMode.Acceleration);
rigidBody.AddForce(Vector3.forward * 10, ForceMode.Force);
rigidBody.AddForce(Vector3.forward * 10, ForceMode.Impulse);
rigidBody.AddForce(Vector3.forward * 10, ForceMode.VelocityChange);
```

unity自带组件Constant Force控制物体
控制力和扭矩力，位移和旋转
constant force 自动加刚体

## 刚体的休眠
```c#
if (rigidBody.IsSleeping())
{
 rigidBody.WakeUp();
}
```