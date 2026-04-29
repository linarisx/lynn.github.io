# 场景切换 游戏退出 光标 随机数 委托
## 场景切换和游戏退出
### 改变场景
`SceneManager.LoadScene("Scene2");`

### 退出游戏
`Application.Quit();`

## 隐藏鼠标改变图片
`public Texture2D txt;`

Escape可以退出

### 隐藏光标
`Cursor.visible = false;`

### 上锁隐藏 鼠标，位置屏幕中间
隐藏鼠标
`Cursor.lockState = CursorLockMode.None;`
上锁鼠标
`Cursor.lockState = CursorLockMode.Locked;`

### 限制鼠标在屏幕范围
`Cursor.lockState = CursorLockMode.Confined;`

### 设置光标图片
（图片，相对于鼠标图片左上角的位置，自动模式(一般不更改)）
`Cursor.SetCursor(txt, Vector2.zero, CursorMode.Auto);`

## 随机数和unity自带委托
### 随机数
Unity
整数 左包含右不包含
`int i = Random.Range(0, 101);`
小数 左右都包含
`float f = Random.Range(1.1f, 9.9f);`

C#
```
System.Random r = new System.Random();
r.Next(0, 101);
```
Random在两个命名空间都有，所以只能指明

### 委托
Unity 
只有无返回值的
```c#
UnityAction ac = () => { };
UnityAction<int> ac1 = (int i) => { };
```

C#
```c#
//无参无返回值
System.Action action = () => { };
//有参无返回值
System.Action<int> action1 = (int i) => { };

//无参有返回值
System.Func<string> fun = () => { return ""; };
//有参有返回值<参数类型，返回值类型>
System.Func<string, int> func = (string i) => { return 1; };
```