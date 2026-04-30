# 三角函数
## 三角
### 角度转弧度
(30° = π/180° * 30 = π/6) 
π/6 -> 30° - > sin30° = 0.5
`Mathf.Sin(30 * Mathf.Deg2Rad)`

π/3 -> 60° -> cos60° = 0.5
`Mathf.Cos(60 * Mathf.Deg2Rad)`

## 反三角
### 弧度转角度
默认算出的是弧度制
0.5 -> 30的弧度制 -> 30°
```c#
float s = Mathf.Asin(0.5f) 
print(s * Mathf.Rad2Deg);
```

0.5 -> 60的弧度制 -> 60°
```c#
float c = Mathf.Acos(0.5f);
print(c * Mathf.Rad2Deg);
```