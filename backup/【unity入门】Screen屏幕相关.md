# Screen屏幕相关
## 当前屏幕分辨率 （整个电脑的）
```c#
Resolution r = Screen.currentResolution;
print("当前屏幕分辨率宽：" + r.width + "高：" + r.height);
```

## 游戏窗口的分辨率
```c#
print(Screen.width);
print(Screen.height);
```

##屏幕休眠模式
`Screen.sleepTimeout = SleepTimeout.NeverSleep;`

## 静态方法
设置分辨率 移动设备不用
`Screen.SetResolution(1920, 1080, false);//是否全屏`