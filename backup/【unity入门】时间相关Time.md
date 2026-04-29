# 时间相关Time
## 时间缩放比例
时间暂停
`Time.timeScale = 0;`
恢复正常
`Time.timeScale = 1;`
两倍速
`Time.timeScale = 2;`

# 帧间隔时间
一般用来位移
路程 = 时间 * 速度

最近一帧，用了多少时间
### 受Scale影响
`print("受Scale影响"+Time.deltaTime);`
### 不受Scale影响
`print("不受Scale影响" + Time.unscaledDeltaTime);`

为什么时间速度都要乘Time.deltaTime？（当前帧移动距离=每秒速度*这一帧时间）
因为高帧设备帧数多，每一帧时间短距离小（10*0.016 = 0.16m）一帧移动的距离
低帧设备帧数少，每一帧时间长距离大（10*0.033 = 0.33m）一帧移动的距离
这样相同时间移动的距离就是一样的


# 游戏开始到现在的时间
一般用在单机游戏 计时

### 受Scale影响
`print("受Scale影响" + Time.time);`
不受Scale影响
`print("受Scale影响" + Time.unscaledTime);`

### 从开始到现在游戏跑了多少帧
`print(Time.frameCount);`

# 物理帧间隔时间
### 受Scale影响
print(Time.fixedDeltaTime);
### 不受Scale影响
print(Time.fixedUnscaledDeltaTime);