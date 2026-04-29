# 缩放和看向
## 缩放
### 相对世界坐标系
` print(this.transform.lossyScale);`
### 相对本地（父对象）
` print(this.transform.localScale);`

 缩放世界坐标系不能改 只能得
 只能改相对父对象的
` this.transform.localScale = new Vector3(3, 3, 3);`

缩放没有API只能自己写
`this.transform.localScale += Vector3.one * Time.deltaTime;`
 
## 看向
一直看向原点 相对于世界坐标系
` this.transform.LookAt(Vector3.zero);`
看向一个对象
` this.transform.LookAt(lookAtObj);`
