# 使用方法
## 新建空物体并挂在LineRenderer组件
GameObject obj = new GameObject();
obj.name = "line";
LineRenderer lineRenderer = obj.AddComponent<LineRenderer>();

## 首尾相连
lineRenderer.loop = true;

## 开始结束宽
`lineRenderer.startWidth = 0.2f;`
`lineRenderer.endWidth = 1;`

## 开始结束颜色
`lineRenderer.startColor = Color.red;`
`lineRenderer.endColor = Color.white;`

## 设置材质
```c#
Material material = Resources.Load<Material>("M");
lineRenderer.material = material;
```

## 设置位置
不设置默认为000

### 点的个数
`lineRenderer.positionCount = 4;`
### 设置每个点的位置
```c#
lineRenderer.SetPositions(new Vector3[]
{ new Vector3(0, 0, 0) ,
  new Vector3(0, 0, 5),
  new Vector3(5, 0, 5),
   }
);
```
### 设置单个点的位置 （索引3的点的位置）
`lineRenderer.SetPosition(3, new Vector3(5, 0, 0));`

## 是否使用世界坐标系
`lineRenderer.useWorldSpace = true;`

## 是否受光源影响
`lineRenderer.generateLightingData = true;`

## 注意
一个物体只能有一个LineRenderer