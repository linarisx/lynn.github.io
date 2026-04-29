#Input输入相关
## 鼠标键盘检测输入 
```c#
if (Input.GetMouseButton(0))
 {
     print("左键长按");
 }
 print(Input.mouseScrollDelta * 10);

 if (Input.GetKeyDown(KeyCode.Space))
 {
     print("空格按下");
 }
 if (Input.GetKey("escape"))
 {
     print("esc按下");
 }

```
## 通过wasd获取-1~1的值
```c#
 print(Input.GetAxis("Horizontal"));
 print(Input.GetAxis("Vertical"));
```
## 通过鼠标移动获取-1~1的值
```c#
 print(Input.GetAxis("Mouse X"));
 print(Input.GetAxis("Mouse Y"));
```

 GetAxisRaw无小数